
> https://www.stefanjudis.com/notes/say-goodbye-to-resource-caching-across-sites-and-domains/

When I started doing web development, we all loaded jQuery from the official global jQuery CDN.

The idea was straightforward: if everybody loads the same jQuery script file (`cdn.jquery.com/jquery.latest.js` – or whatever URL it was back then), then the script file would be cached by the browsers, and other sites requesting the same script would benefit from the speedup of already cached resources. Users would have popular libraries like jQuery already sitting in their browser cache because earlier visited sites requested them.

This caching behavior was possible because, at the time, the browser's HTTP caches used the asset URL (`cdn.jquery.com/jquery.latest.js`) as a single cache key. Browsers use cache keys to figure out if and how to cache a resource. If these keys only consist of the resource URL, it allows the reuse of resources across sites and domains.

All this worked great, but as it is with many great inventions in web technology, **cross-site resource caching enabled new ways to track users across different sites**.

As an example, let's assume Facebook loads a unique file in their logged-in area (`fb-logo-ajgdmaks839–as.svg` – I made that file path up); if I would know the file path to such a file, request it on `stefanjudis.com` and see a rapid response coming from the browser cache, I can almost be sure that the user has logged into Facebook lately.

## [New HTTP cache keys in Google Chrome](https://www.stefanjudis.com/notes/say-goodbye-to-resource-caching-across-sites-and-domains/#new-http-cache-keys-in-google-chrome)

[Webkit (Safari) changed its caching strategy already in 2013](https://bugs.webkit.org/show_bug.cgi?id=110269) to prevent user tracking via the browser cache. Its cache keys are a combination of the requested resource URL and the top-level domain requesting the resource.

_☝️ Big thanks to [Thomas Steiner, who gave input on that matter](https://twitter.com/tomayac/status/1317861511784792067?s=20)._

On the bright side, this cache key structure prevents the mentioned tracking possibilities; unfortunately, it leads to duplicated resources in the browser cache.

And... it hinders third-party resource sharing across the internet.

```
Browsers duplicate resources with different keys:

cdn.jquery.com/jquery.latest.js-amazon.co.uk
cdn.jquery.com/jquery.latest.js-www.stefanjudis.com
```

Starting with v86, Chrome will be using combined cache keys, too. This change means that it's time to say goodbye to third-party resource-sharing across the web. [With Chrome's market share of roughly 70%](https://www.statista.com/statistics/544400/market-share-of-internet-browsers-desktop/), most browsers hitting our sites will use partitioned browser caches from now on. Chrome went for combining the top-level site URL, the current frame site URL, and the resource URL. This approach is more granular than what Safari does, but the result is the same.

If your sites request the global jQuery, modules from [unpkg.com](https://unpkg.com/), font files from [Google fonts](https://fonts.google.com/) or GA's (Google Analytics) `analytics.js`, **users will redownload the resources no matter if they downloaded and cached them for other sites already.**

What does this change mean for you? If your sites live on modern hosting that provides a CDN and supports HTTP/2, you should drop the third-parties and ship all resources yourself. Relying on a third party resources offers little value in 2020.

I have mixed feelings about these changes. It's excellent that browsers consider privacy, but it looks like anything can be misused for tracking purposes these days. I wonder where we're going with this... 😢

---

If you're interested in learning more on this topic, give [Terence Eden's post "Please stop using CDNs for external Javascript libraries"](https://shkspr.mobi/blog/2020/10/please-stop-using-cdns-for-external-javascript-libraries/) or [Andy Davies' post "Safari, Caching and Third-Party Resources"](https://andydavies.me/blog/2018/09/06/safari-caching-and-3rd-party-resources/) a read, too.

And hey, this post was trending on Hacker News. 🎉 If you're interested, [here are the Hacker News comments](https://news.ycombinator.com/item?id=24894135).

Update: [Firefox shipped partitioned HTTP caching in January 2021, too](https://developer.mozilla.org/en-US/docs/Web/Privacy/State_Partitioning#network_partitioning).
