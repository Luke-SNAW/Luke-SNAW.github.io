---
id: id1umwb0k8k7exk0589tae9
title: Making the Web Faster with Service Workers and Performance Research
desc: ""
updated: 1672708357794
created: 1672707051806
---

> https://calendar.perfplanet.com/2022/making-the-web-faster-with-service-workers-and-performance-research/)

## TLDR;

- We have conducted web performance research at the University of Hamburg since 2010.
- We came up with a approach to cache dynamic website resources like HTML and APIs which can be plugged into websites via Service Workers
  - automatically dealing with personalization in HTML
  - keeping caches up-to-date by crowdsourcing cache checks
  - caching dynamic resources in the complete web cache hierarchy including browser cache through Bloom filter-based cache coherence algorithms
  - adding lots of other optimizations like predictive preloading, 3rd-party caching and image optimization
- Impact on Core Web Vitals can be A/B tested and measured via RUM on production traffic
- Large-scale e-commerce pages show best performance improvements

## Targeting large gains in web performance

Twelve years ago we started our research on web performance and caching of dynamic content with the goal to make the web a much faster place.

In this post we share the results of this journey and explain how the approach enables large performance gains A/B tested and measured with Real User Monitoring like the one in the chart below.

[Largest Contentful Paint comparison from an A/B test measured via Real User Monitoring (RUM).](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/Untitled.png)

References to scientific publications are scattered throughout the article but for a comprehensive list you can scroll down to our publications list at the very end.

## Bottlenecks in modern web performance

On a high level, all pages on the web load in the same way and experience the same sources of performance bottlenecks.

Let’s start with the basics here, to better highlight what changes about the page loading process when Service Worker is used. If you are a web expert feel free to skip to the next section.

On a high level, loading a website is very simple:

1. The client requests the HTML resource.
2. The server generates a response and sends it to the client.
3. The client loads linked resources like CSS, JS, images and other assets.
4. The browser compiles and executes JavaScript code and renders the page.

[A simplified diagram of how web pages are loaded](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/Untitled%201.png)

These steps also make up the main performance bottlenecks; or to frame it more positively, they highlight the common areas of optimization:

1. Improve the first request with protocol optimizations (fast DNS, 0 round-trip TLS, OCSP stapling, HTTP/3).
2. On the backend, try to keep processing overhead to a minimum, optimize database queries and slow code paths, and use caching wherever possible.
3. Keep your critical rendering path (CRP) as short as possible by reducing the number of bytes sent over the network and avoiding render- or parser-blocking resources.
4. Keep the frontend “lean”, render the page without executing JavaScript, use efficient CSS and avoid layout shift.

Most likely any company operating a website has lots of optimizations like these in their backlog, some being harder to implement than others.

**With our research we went a slightly different route and did not try to solve all of a website’s bottlenecks individually. Instead we use a Service Worker and special caching mechanisms to change how the browser loads the page**.

## Accelerating Dynamic Resources: How it works

In contrast to traditional caching solution implemented on an infrastructural or backend level, we will come in on the client side and optimize how the browser loads the page and how it makes use of available caches. This also means there are no changes to the backend, frontend or infrastructure required at all.

The optimisation can be applied just by hosting and installing a special Service Worker. Once activated, the service worker runs in a background thread in the user’s browser and acts as a network proxy, seeing every request that the browser sends to the network. Service workers are supported in 97% of browsers, do not require permission to be used, and are completely invisible to users.

We will use the service worker to reroute requests to a distributed caching network, shown as Caching _service_ in the graph below. The unique part here is that not only static files like JS, CSS and images are cached, but also **dynamic resources like APIs or HTML** that can change at any point in time.

For HTML resources, we need to ensures that personalized content (e.g. login state, recommendations, cart) is still loaded from the original website servers. We also need to automatically keep the cached content up-to-date and finally enables caching of these dynamic resources on every level of the cache hierarchy including the user’s device itself.

[Caching Architecture](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/Untitled%202.png)

Caching HTML resources of websites in a generic way is quite a complex task — for e-commerce pages in particular — and we are faced with three main challenges:

1. How can HTML be cached if it is personalized?
2. How can caches be kept up to date for millions of pages when content changes unpredictably?
3. How can dynamic content be cached in the client without an API to purge it?

The next three sections cover how we tackle those three challenges.

### Challenge 1: Caching personalized content

Personalization and caching are usually not compatible since multiple users cannot receive the same cached response without losing their personalization. So HTML that contains personalization is generally considered uncacheable.

That said, in most scenarios only parts of a page’s content are personalized and large sections look the same for all users. A good example for this is product detail pages on e-commerce platforms where prices, recommendations or the cart icon may be personalized, but the product image, title and description are the same for all users.

We are using this fact to our advantage and load personalized (non-cachable) and common (cacheable) parts separately by changing how the browser loads the initial HTML. In e-commerce in particular, the common part usually contains important information for the user that needs to be loaded as fast as possible.

The loading process works like this and is shown here:

[The Service Worker requests two versions of the HTML document](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/new_perso.gif)

1. A user navigates to a page
2. The Service Worker issues two requests in parallel that race each other:
   1. One request is sent to the Caching service, loading an anonymous version of the page. The request does not include any cookies or session information and the page is the same for all users and therefore cacheable. It is the one you would see if you opened the page in an Incognito or private tab.
   2. The other request is sent to the origin backend. It contains all usual cookies and returns the personalized page tailored to the exact user.
3. Usually, the cached HTML response is much faster and wins the race. The browser receives the HTML and can immediately start loading all the dependencies and render the anonymous page.
4. Once the backend response from the origin server with the personalized HTML is received, it is merged with the already-rendered HTML and the personalized sections of the page become visible. To the user, the personalized parts are progressively rendered.

While the process does incur the overhead of loading two full HTML files containing redundant information, it usually renders personalized content faster than loading it via `fetch` requests from JavaScript since the request for personalized content is issued in parallel to the initial HTML request.

There are a lot of important details to how this merging of two HTMLs in the browser works and how it can be tweaked which goes beyond the scope of this blog post. For example, content merging can introduce flickers and shifts which can then be fixed via CSS.

The most important challenge of how this works with JavaScript or even modern frontend frameworks however will be addressed in the next section.

> ???? Note: The approach of using two parallel HTML requests is a means to enable caching of those resources at all. Pages that do not contain any personalized content in the HTML, do not require this logic. For them the solutions to challenge two and three are the important optimizations.

#### Challenge 1.1: Delaying JS to avoid problems from merging personalized content

As explained in the previous section, applying personalization requires to merge the personalized HTML into the already rendered anonymous HTML in the browser which involves exchanging DOM nodes.

While the browser is very efficient in only rendering things that have changed, JavaScript is not so forgiving of sudden changes in the DOM nodes. Event listeners might break, click listeners might not be attached any longer, client-side-rendered elements might disappear and the shadow DOM of frameworks like React or Vue adds another layer of complexity.

To prevent JavaScript from breaking, the only option is to delay it until the personalized HTML is merged and no unexpected DOM changes can appear. Afterwards the JS execution can continue.

The following gif shows how requesting and merging two HTML files plays together with delaying the JS execution.

[We need to delay JS execution to avoid breakage after merging anonymous and personalized HTML](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/js.gif)

The details on how JS is delayed are very important to ensure correct execution and good performance. This is how we deal with this challenge:

1. The cached HTML needs a few preparations that are applied automatically:
   1. The code responsible for merging the personalized HTML document is inserted at the end of the `body`.
   2. Since the code insertion happens asynchronously, we then place a blocking external script after that to pause JS execution until after the document merge.
   3. Next, all external scripts are re-inserted after the blocking script, preserving their order. All inline scripts are removed (they tend to contain personalization and need to be executed from the personalized HTML).
   4. An inline script is placed before each external `script` tag that executes all inline scripts from the personalized HTML.
2. Once the cached HTML is handled by the browser and the parser get towards the end of the body it will detect the blocking script and request it. As long as that request is pending, JS execution cannot continue.
3. The Service Worker will receive that special JS request and withhold the response.
4. Once the code for merging the personalized HTML into the rendered document has completed, it sends a message to the Service Worker.
5. On receiving the message, the Service Worker responds to the pending script request with an empty script causing the JS execution to continue normally.
6. The inline script between the external script now have access to the personalized HTML and can simply insert and execute the inline script in the correct order.

Delaying JS execution through this approach has some important advantages. Firstly, it prevents DOM events like `domInteractive` or `domContentLoaded` from firing before the actual JS is executed. Secondly, since the external scripts are in the cached document already, the preload scanner of the browser will discover them early, then download and compile them for faster execution. Thirdly, personalized or dynamic inline scripts that are very common in e-commerce applications are easily covered by this.

This approach enables caching even of personalized HTML pages. The next two challenges are important optimizations independent of whether the HTML is personalized.

### Challenge 2: Automatic cache sync via Change Detection

Not only is personalization a challenge when caching dynamic resources like HTMLs or API responses; even the anonymous version of the main document can change at any point in time, making it necessary to update caches accordingly. With potentially millions of cache entries necessary, this is a big challenge.

We will tackle this challenge with a concept called _Change Detection_. It builds on the mechanism used for personalization to detect changes to the page.

Since every user loads both the anonymous cached version of the HTML as well as the personalized version from origin, we already have everything we need to validate the cache entry on the client side. If something in the cached version has changed, we inform the Cache service, which refreshes the resource and updates the caches only if the content has actually changed.

As an example: let’s say someone changes the product title for a product detail page in the CMS. The cached version of the page will contain the old product title and is no longer up-to-date. When a user navigates to the product page, they receive the stale cache entry with the old title. Once the personalized HTML with the new product title arrives in the browser, the versions are merged and the new product title appears. As both HTML versions are compared, a cache refresh is triggered because of the changed title.

The first user to detect the change will experience a flicker of the title when the up-to-date title appears upon merge. All other users and even the first user upon reload will not experience that flicker and receive an up-to-date cached version. This effectively crowdsources the challenge of discovering outdated cache entries among millions of cache entries without increasing the origin server load.

Additionally, we use the “cache hotness” information from our shared caches to sample the change detection on frequently-visited pages to reduce overhead.

[Cache synchronization is crowdsourced through “Change Detection”](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/Untitled%203.png)

Deployments of the whole application are treated separately from page-level difference because they can result in structural changes that make it impossible to merge the cached version with the new original version. We can handle new deployments in a process called _Deployment Detection_: If the site links new JS and CSS versions, the Cache services infers that a deployment was rolled out so it can purge the entire cache and rebuild it asynchronously.

The Cache service also has an option to define periodic refreshes (mostly used for dynamic 3rd-party scripts) and a Purge API for deeper integration. Whenever content is updated and caches are purged, the Cache service automatically pre-warms cache PoPs in regions with a lot of traffic to prevent cache misses.

With this automated approach to cache updates we keep the integration as easy as possible. The approach works great in production and can always be extended by API-initialized cache updates if necessary.

### Challenge 3: Browser caching without staleness

In the previous sections we have established how we can deal with personalization and still cache HTML resources and how we enable the Cache service to detect changes and update its cache in near real time. The main open question is how can dynamic content be cached in the Browser without an API to purge it?

Standard HTTP caching is not equipped to deal with resource changing irregularly. The standard procedure with HTTP caching is:

1. The client sends a request to the server.
2. The server responds with a resource and attaches a `Cache-Control` header, which contains a time-to-live (TTL).
3. On the way to the client, the resource is stored by caches. We distinguish between two kinds of caches:
   1. Invalidation-based caches which have APIs to remove (purge) content from them. This is your standard CDN or server side cache that is shared by all users. It will generally hold on to your cache entry until the TTL expires but you can send purge requests to evict cache entries immediately.
   2. Expiration-based caches that hold on to resources until their TTL expires without an API to purge them. This is your client side caches like browser cache or service worker cache storage.
4. On subsequent requests these caches serve the stored content as long as the TTL permits.

It is so hard to cache HTML file in the client because issues arise when the cached content changes before the TTL expires. While invalidation-based caches can be purged, expiration-based caches will continue to send stale content back to clients.

#### Dynamic Browser Caching: The Bloom filter-based cache sketch

Our approach is to cache all resources in the browser and set high TTL values that are [dynamically estimated](https://medium.baqend.com/dynamic-cache-lifetime-with-immutable-cache-control-headers-db066cf60fea). So what happens when cached resources are changed before their TTL expires?

When the Cache service detects a resource change that is still cached by clients (e.g. an HTML file), it does two things:

1. It purges the content in the invalidation-based cache in the CDN and backend.
2. It adds the URL of the resource in a probabilistic set data structure called a counting [Bloom filter](https://en.wikipedia.org/wiki/Bloom_filter) for the remainder of the highest delivered TTL.

The counting Bloom filter is then flattened into a regular Bloom filter and transferred to every connecting client.

When the client loads a resource, the service worker first checks whether the URL is contained in the Bloom filter. If it is not, it can be safely taken from the browser cache. If it is, the worker forwards the request to the network, loads the resource from the CDN and updates the local cache with it.

The great thing about Bloom filters is that they are very compact by allowing for false positives: sometimes the Bloom filter will match a URL that was not inserted. False negatives on the other hand cannot happen — a URL that was inserted will always be matched by the Bloom filter.

To give an example of the compactness: A Bloom filter with a false positive rate of < 5% can store 20k different URLs in under 10kB. So it fits within the initial TCP congestion window and can usually be transferred to the client in a single round trip.

[Checking for cache hits using a Bloom filter](https://calendar.perfplanet.com/wp-content/uploads/2022/12/erik/Untitled%204.png)

Of course there are lots of intricate details and trade-offs involved — Bloom filter size, update cycles, TTL estimation, distributed server implementations to name a few — to make sure the performance is maximized.

### Trade-offs

The way our caching approach works makes it a very powerful tool but as with any technology there are trade-offs to consider that make it more suitable on some pages compared to others.

1. The way personalized content is loaded and rendered means that the biggest performance impact is on pages where the main content including the [largest contentful paint (LCP)](https://web.dev/lcp/) element is not personalized and can be rendered from the cached HTML. If the main content is personalized, performance is still improved by Speed Kit, but the optimization is less impactful. On e-commerce pages we therefore focus mostly on home, category and product pages and exclude fully personalized pages like cart or checkout.
2. Client-side rendered sites are a nightmare when it comes to web performance with their [core web vitals](https://web.dev/vitals/) ranging among the worst. On those sites, the approach can struggle to achieve a large performance impact since as long a the HTML is personalized, JS execution needs to be delayed which also delays rendering of the page. On the positive side, most e-commerce pages we deal with already use [server side rendering (SSR)](https://web.dev/rendering-on-the-web/) and we are testing ways to render above the fold content on our cache servers for page that cannot migrate easily.
3. First loads of a completely new user are not accelerated in this approach because the service worker needs to be installed on the first page load. It is very persistent afterwards so returning users and any navigation on the site are fully accelerated.
4. Change Detection is a great technology that works extremely well in product due to an important trade off in its design. It takes one user to load a stale cache entry to detect the change and update the cache. This means that one user will see a flicker from old content to new content when the fresh document from the original server is merged. The flicker is fixed for other users and further reloads due to the change detection. In many scenarios this is a worthwhile trade-off. Content where this is not acceptable needs to be hidden until after the merge.

## Advanced frontend optimizations

The use of Service Worker combined with access to Real User Monitoring (RUM) data enable other powerful optimizations:

1. **Predictive Preloads**: RUM data enables learning algorithms to predict where the user can navigate next. This means the cached HTML can already be preloaded before the navigation. Usually servers for shop systems cannot cope with the added load of such preloads, but cache servers do not mind the extra traffic.
2. **3rd-Party Caching**: 3rd-party resources can be cached by the Service Worker as well to optimize their caching, save on the additional TLS connection and use a connection that already has bigger bandwidth avoiding [TCP slow start](https://developer.mozilla.org/en-US/docs/Glossary/TCP_slow_start) for the new connection.
3. **Image Optimization**: By running on the user’s device, the service worker has access to the screen size and DPR of the user. It attaches this information to the image requests and uses an image service to transcode, resize and recompress images automatically.

## Evaluating performance with A/B tests and RUM

Of course, performance bottlenecks vary from site to site. That is why we constantly evaluate and test how this caching approach can improve performance on new websites using A/B tests and Real User Monitoring (RUM) data.

Since the integration is based on JavaScript in the client, you can easily run an A/B test to try out such a solution with 50% of users accelerated and the other 50% serving as the control group. In both group you can gather performance data with via a [RUM tool](https://aws.amazon.com/de/blogs/big-data/how-baqend-built-a-real-time-web-analytics-platform-using-amazon-kinesis-data-analytics-for-apache-flink/).

After a few weeks of data collection, you can compare the performance between the two groups and are able to prove the significant improvements to our customers. The RUM tool also stays in place after the A/B test to monitor performance and work with our clients to achieve optimal performance in the long run.

We also use the same methodology of A/B tests with RUM tracking to research and evaluate new features and optimizations. **Access to detailed RUM data from about 300 million users per month is what enabled us to perfect the approach and achieve great performance improvements.**
