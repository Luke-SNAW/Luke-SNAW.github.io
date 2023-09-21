---
id: 3y12i7xrbl8hk7yneo0d5ra
title: Get All That Network Activity Under Control with Priority Hints
desc: ""
updated: 1695267424965
created: 1695267290514
---

> https://www.macarthur.me/posts/priority-hints

The browser is very good at prioritizing resources requests on its own. But it's not always great. Priority hints makes it easy to provide explicit instructions as to how and in what network activity occurs.

Open up the browser's network tab and you'll see a lot of activity. Assets are being downloaded, information's being submitted, events are being logged, and more.

With so much going on, effectively managing the priority of that traffic is pretty critical. Bandwidth contention is real, and some HTTP requests simply don't rank as highly as others when they're all firing at once. For example, if you _had_ to choose, you'd probably prefer someone's payment request successfully complete vs. an analytics request simply indicating they tried. And having your hero image show up as quickly as possible is arguably more important than your logo rendering in the footer of your page.

Fortunately, the browser has a growing collection of tools to help prioritize all this network activity. These "[priority hints](https://github.com/WICG/priority-hints/blob/main/EXPLAINER.md?ref=alex-macarthur)" help the browser make fewer assumptions and clearer decisions about which requests to favor over others when resources are limited.

It's a useful suite of tools, and they can make a tangible impact to page performance when leveraged well, including those increasingly important core web vitals. Let's explore a few of them, along with some scenarios in which they're most helpful.

## [Prioritizing Preloaded Assets](https://www.macarthur.me/posts/priority-hints#prioritizing-preloaded-assets)

Modern browsers have a well-supported means of being told about resources that'll _eventually_ be needed on the current page: `<link rel="preload" ... />`. When placed in the `<head>` of the document, the browser is instructed to begin downloading it as soon as possible with "high" priority.

To be fair, the preload scanner in the browser is already _really good_ at this sort of thing ([I've previously written](https://www.macarthur.me/posts/effective-preloading?ref=alex-macarthur) about it in a little more depth). For that reason, preloading is best used on _late-discovered_ assets – anything not loaded directly by your HTML. Think: a font file loaded within some CSS, or a background image loaded via an inline `style` attribute.

Consider a font that's loaded exclusively through a CSS `@font-face` rule:

```css
@font-face {
  font-family: "Inter Variable";
  src: url("./font.woff2") format("woff2");
}
```

On load, that font gets the lowest download priority, despite it being pretty important for the visual experience of the page.

[image showing low download priothe font file is given low download priority when loaded just through CSSrity of fonts](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-12-highlighted.png)

Now, let's preload that resource:

```html
<head>
  <!-- Other stuff... -->
  <link rel="preload" href="/font.woff2" as="font" />
</head>
```

It's now far more favored:

[the font is given higher download priority after being preloaded](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-12.png)

But you can get [even more explicit](https://developer.mozilla.org/en-US/docs/Web/API/HTMLLinkElement/fetchPriority?ref=alex-macarthur) using the `fetchpriority` directly on the `link` tag. It'll let you signal relative priority when preloading multiple assets at once.

Here's a contrived scenario in which you'd like to preload two fonts, but give one priority over the other:

```html
<link rel="preload" href="./font-1.woff2" as="font" fetchpriority="low" />
<link rel="preload" href="./font-2.woff2" as="font" fetchpriority="high" />
```

The resulting network activity reflects these instructions (I included a third, non-preloaded font in there too, just because).

![](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-14.png)

### [When to Use It](https://www.macarthur.me/posts/priority-hints#when-to-use-it)

In general, use preloading when an asset isn't loaded by your HTML directly, but it's critical to the experience of the page (fonts, CSS background images, etc.). And include the `fetchpriority` attribute when preloading several resources of the same type and you're clear about which is most important.

## [Prioritizing `fetch()` Requests](https://www.macarthur.me/posts/priority-hints#prioritizing-fetch-requests)

In my opinion, the Fetch API is one of the most ergonomic offerings of the modern web. And it has some nice features that `XMLHttpRequest` lacked, like the ability to [signal priority](https://developer.mozilla.org/en-US/docs/Web/API/fetch?ref=alex-macarthur) on an outgoing request.

The most top-of-mind use case is one I've already mentioned: analytics requests. When bandwidth is slim and multiple requests are in play, the browser will make its own priority decisions. But we as engineers (should) know that your typical analytics requests ought to take a back seat to others more critical to the page's purpose. Modern `fetch()` makes that easy.

Here's a simple setup with two requests being queued at (virtually) the same time:

```javascript
fetch("http://localhost:8000/pay", {
  method: "POST",
  body: paymentBody,
})

fetch("http://localhost:8000/log", {
  method: "POST",
  body: loggingBody,
})
```

By default, the browser will automatically consider them both "high" priority:

[both requests will have high priority by default](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-16.png)

Now, we'll explicitly tell the browser how each request should be prioritized:

```diff
fetch("http://localhost:8000/pay", {
	method: "POST",
	body: paymentBody,
+	priority: "high"
});

fetch("http://localhost:8000/log", {
	method: "POST",
	body: loggingBody,
+	priority: "low"
});
```

This time around, the priorities are different:

[one request now has higher priority than the other](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-17.png)

#### [Useful counterpart: `keepalive: true`](https://www.macarthur.me/posts/priority-hints#useful-counterpart-keepalive-true)

A possible concern here is that "low" priority requests may be lost to the void – cancelled if the user navigates away from the page too soon. That's a legitimate issue. Depending on a few factors, either closing the tab or moving onto the next page may cause an important, but _relatively_ low-priority request to be aborted.

Fortunately, `fetch()` also accepts a `keepalive` option. When set to `true`, the browser will carry that request to completion even when the page is terminated. If you'd like to dig into it more, take a gander at [what I wrote for for CSS-Tricks](https://css-tricks.com/send-an-http-request-on-page-exit/?ref=alex-macarthur) a while back.

### [When to Use It](https://www.macarthur.me/posts/priority-hints#when-to-use-it-1)

Indicate `fetch()`priority when you know multiple requests are executing concurrently, and it's clear to you which is most important (or which can safely be deprioritized).

## [Prioritizing `<img />` Requests](https://www.macarthur.me/posts/priority-hints#prioritizing-img-requests)

Without us doing anything special, the browser attempts to do its best at determining the most important images on a page. To illustrate this, I loaded the following images, spaced a good distance apart, so only one would be "above the fold."

```html
<img src="./cat-1.jpeg" />
<div style="height: 5000px"></div>
<img src="./cat-2.jpeg" />
<div style="height: 5000px"></div>
<img src="./cat-3.jpeg" />
```

The browser picked up on which was most important, but it took a second. When downloading began, all three were "low" priority. But shortly after, the one above the fold switched to "high."

[priority for images shifts when loading begins](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/loading-priority.gif)

Things became more predictable when I added a `fetchpriority` attribute to the first image:

```html
<img src="./cat-1.jpeg" fetchpriority="high" />
```

After that, `cat-1.jpeg`loaded at the highest priority right out of the gate. While initially head-tilting, it makes sense. The browser is smart at determining resource criticality, but it benefits from clear instructions. If you know an image is important, be explicit about it.

This feature, by the way, pairs very nicely with native image lazy loading, a very well-supported feature these days.

```html
<img src="./cat-1.jpeg" fetchpriority="high" />
<div style="height: 5000px"></div>
<img src="./cat-2.jpeg" loading="lazy" />
<div style="height: 5000px"></div>
<img src="./cat-3.jpeg" loading="lazy" />
```

With that in place, the browser knows exactly how (and if) to load images, only when appropriate. In my case, it won't even begin the request for off-screen images on initial load. Instead, it'll wait until they're closer to the viewport.

[priority for images shifts](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-18.png)

### [When to Use It](https://www.macarthur.me/posts/priority-hints#when-to-use-it-2)

Use an explicit `fetchpriority` on images when you know they're very important to page experience. Hero images are a great place to start, and it can even have an impact on a page's core web vitals – [specifically, LCP](https://addyosmani.com/blog/fetch-priority/?ref=alex-macarthur) (largest contentful paint).

## [Prioritizing `<script />` Tags](https://www.macarthur.me/posts/priority-hints#prioritizing-script-tags)

Any plain `<script />` with a `src` attribute on a page will get `high` priority as it's being fetched, but there's a trade-off: it blocks parsing of the rest of the page until it's loaded and executed. For that reason, the `async` attribute is helpful. It'll request the script in the background at `low` priority, and execute as soon as it's ready. Knowing this, the following setup behaves predictably:

```html
<script src="/script-async.js" async onload="console.log('async')"></script>
<script src="/script-sync.js" onload="console.log('sync')"></script>
<script>
  console.log("inline")
</script>
```

The asynchronous script is demoted in priority:

[asynchronous script is downloaded with "low" priority](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-22.png)

And the console confirms that subsequent scripts were allowed to parse and execute as the `async` script was loading.

[script loaded asynchronously](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/async-1.gif)

### [Non-Blocking, but High-Priority Scripts](https://www.macarthur.me/posts/priority-hints#non-blocking-but-high-priority-scripts)

Most of the time, that behavior's fine. But sometimes, you might want a script to load both asynchronously _and_ with "high" priority.

A possible scenario is a small SPA mounted in the hero of a landing page. In order to preserve the page's core web vitals, specifically LCP and FID (first input delay, soon to be replaced by [interaction to next paint](https://developers.google.com/search/blog/2023/05/introducing-inp?ref=alex-macarthur)), you'll need that script to be highly prioritized (after all, it's responsible for building and powering your application). But at the same time, you don't want it to block the rest of the page from parsing.

So, let's give it a `fetchpriority`:

```diff
+ <script src="/script-async.js" async onload="console.log('async')" fetchpriority="high"></script>
<script src="/script-sync.js" onload="console.log('sync')"></script>
<script>console.log("inline");</script>
```

And now, it's downloaded with elevated priority, while still not blocking the rest of the page:

[asynchronous script downloaded with high priority](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/image-23.png)

And the console verifies this. With that higher priority, the async script loads more quickly. In this case, even before the synchronous and inline ones.

[log asynchronous script downloaded](https://picperf.dev/https://cms.macarthur.me/content/images/2023/09/prioritized-async.gif)

While I didn't toy with it specifically here, yes, `fetchpriority` works with deferred scripts as well.

### [When to Use It](https://www.macarthur.me/posts/priority-hints#when-to-use-it-3)

Place `fetchpriority` on your scripts when you know their priorities up front, and if you suspect the browser won't have enough information to determine on its own. As I mentioned, it's particularly helpful for prioritizing scripts that you'd also like to load in non-blocking, asynchronous way.

## [To Be Used Intentionally](https://www.macarthur.me/posts/priority-hints#to-be-used-intentionally)

It's easy to become a little overzealous about tools like this, leading to overuse. So, be careful – doing so may come at a cost. As the adage goes: "emphasizing everything = emphasizing nothing." In fact, overuse may actually make it _more difficult_ for the browser to manage against network contention, _harming_ a page's performance.

MDN even makes a point to call it out in some of their [priority hint documentation](https://developer.mozilla.org/en-US/docs/Web/API/HTMLLinkElement/fetchPriority?ref=alex-macarthur):

> Use it sparingly for exceptional cases where the browser may not be able to infer the best way to load the resource automatically. Over use can result in degrading performance.

So, don't feel obligated to reach for these tools just because they exist. Wield them with care.

## [Reviewing: When to Hint](https://www.macarthur.me/posts/priority-hints#reviewing-when-to-hint)

There's a lot here, so let's quickly review some times you might choose to leverage priority hints. They're not exhaustive. Just some good places to start.

- Hint **preloaded assets** when you want the browser to be aware of multiple late-discovered resources, some of which bring more critical to the page than others.
- Hint **`fetch()` requests** that you know are either a crucial part of a user's experience, or can safely be deprioritized to make way for more important ones.
- Hint above-the-fold **images** you want to be loaded & visible as soon as possible.
- Hint **scripts** that are key to the function of a page, but you don't want to block the rest of the page (including other assets) from being parsed and downloaded.

## [Make the Browser Guess Less](https://www.macarthur.me/posts/priority-hints#make-the-browser-guess-less)

The browser is incredibly smart about figuring out how and when to download the stuff that makes our pages tick. But it's not always _great._ It doesn't know why a page exists or the intent behind its individual parts. And so occasionally, it could use some extra help.

That's why these priority hints exist: to make instructions clear, and to leave the browser very little chance to get those decisions wrong. Keep them in mind the next time you're digging through your own application's network activity, and when it makes sense, reach for them to help make your page performance just a little more intelligent.
