---
id: hy0p54y75phy5p47r4buhf7
title: Optimizing third-party script loading in Next.js
desc: ""
updated: 1646819469838
created: 1646819166781
---

https://web.dev/script-component/

# Third-party scripts and their impact on performance

# Aurora’s focus on third-party scripts

# Sequencing third-party scripts without a framework component

The [available guidance](https://web.dev/efficiently-load-third-party-javascript/) to reduce the impact of render-blocking scripts provides the following methods for efficiently loading and sequencing third-party scripts:

1. Use the `async` or `defer` attribute with `<script>` tags that tell the browser to load non-critical third-party scripts without blocking the document parser. Scripts not required for initial page load or the first user interaction may be considered non-critical.

   - ```html
     <script src="https://example.com/script1.js" defer></script>
     <script src="https://example.com/script2.js" async></script>
     ```

2. [Establish early connections to required origins](https://web.dev/preconnect-and-dns-prefetch/) using preconnect and dns-prefetch. This allows critical scripts to start downloading earlier.

   - ```html
     <head>
       <link rel="preconnect" href="http://PreconnThis.com" />
       <link rel="dns-prefetch" href="http://PrefetchThis.com" />
     </head>
     ```

3. [Lazy-load](https://web.dev/embed-best-practices/#lazy-loading) third-party resources and embeds after the main page content has finished loading or when the user scrolls down to the part of the page where they are included.

# The Next.js Script component

The [Next.js Script component](https://nextjs.org/docs/basic-features/script) implements the above methods for sequencing scripts and provides a template for developers to define their loading strategy. Once the suitable strategy is specified, it will load optimally without blocking other critical resources.

The Script component builds on the HTML <script> tag and provides an option to set the loading priority for third-party scripts using the strategy attribute.

```jsx
// Example for beforeInteractive:
<Script
  src="https://polyfill.io/v3/polyfill.min.js?features=IntersectionObserverEntry%2CIntersectionObserver"
  strategy="beforeInteractive"
/>
// Example for afterInteractive (default):
<Script src="https://example.com/samplescript.js" />
// Example for lazyonload:
<Script src="https://connect.facebook.net/en_US/sdk.js" strategy="lazyOnload" />
```

The strategy attribute can take three values.

1. `beforeInteractive`: This option may be used for critical scripts that should execute before the page becomes interactive. Next.js ensures that such scripts are injected into the initial HTML on the server and executed before other self-bundled JavaScript. Consent management, bot detection scripts, or helper libraries required to render critical content are good candidates for this strategy.

2. `afterInteractive`: This is the default strategy applied and is equivalent to loading a script with the defer attribute. It should be used for scripts that the browser can run after the page is interactive—for example, analytics scripts. Next.js injects these scripts on the client-side, and they run after the page is hydrated. Thus, unless otherwise specified, all third-party scripts defined using the Script component are deferred by Next.js, thereby providing a strong default.

3. `lazyOnload`: This option may be used to lazy-load low-priority scripts when the browser is idle. The functionality provided by such scripts is not required immediately after the page becomes interactive—for example, chat or social media plug-ins.

# [Measuring the impact](https://web.dev/script-component/#measuring-the-impact)

# What’s next for the Script component

## Using web workers

[Web workers](https://developer.mozilla.org/docs/Web/API/Web_Workers_API/Using_web_workers) can be used to run independent scripts on background threads which can free up the main thread to handle processing user interface tasks and improve performance. Web Workers are best suited for offloading JavaScript processing, rather than UI work, off the main thread. Scripts used for customer support or marketing, which typically do not interact with the UI, may be good candidates for execution on a background thread. A lightweight third-party library—[PartyTown](https://github.com/BuilderIO/partytown)—may be used to isolate such scripts into a web worker.

With the current implementation of the Next.js script component, we recommend deferring these scripts on the main thread by setting the strategy to `afterInteractive` or `lazyOnload`. In the future, we propose introducing a new strategy option, `'worker'`, which will allow Next.js to use PartyTown or a custom solution to run scripts on web workers.

## Minimizing CLS

Third-party embeds like advertisements, video, or social media feed embeds can cause layout shifts when lazy-loaded. This affects the user experience and the [Cumulative Layout Shift (CLS)](https://web.dev/cls/) metric for the page. CLS can be minimized by specifying the size of the container where the embed will load.

## Wrapper components
