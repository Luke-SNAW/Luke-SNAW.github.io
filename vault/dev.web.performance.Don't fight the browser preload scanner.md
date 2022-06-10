---
id: xi1xolh4wi6ojnrrxxz5tz7
title: Don't fight the browser preload scanner
desc: ""
updated: 1654936336664
created: 1654936305014
---

https://web.dev/preload-scanner/

One overlooked aspect of optimizing page speed involves knowing a bit about browser internals. Browsers make certain optimizations to improve performance in ways that we as developers can't—but only so long as we don't thwart those optimizations unintentionally.

One internal browser optimization to understand is the browser preload scanner. In this post, we'll talk a bit about how the preload scanner works—and more importantly, how you can avoid getting in its way.

## What's a preload scanner? [#](https://web.dev/preload-scanner/#what's-a-preload-scanner)

Every browser has a primary HTML parser that [tokenizes](https://en.wikipedia.org/wiki/Lexical_analysis#Tokenization) raw markup and processes it into [an object model](https://developer.mozilla.org/docs/Web/API/Document_Object_Model). This all merrily goes on until the parser pauses when it finds a [blocking resource](https://web.dev/render-blocking-resources/), such as a stylesheet loaded with a `<link>` element, or script loaded with a `<script>` element without an `async` or `defer` attribute.

![HTML parser diagram.](https://web-dev.imgix.net/image/jL3OLOhcWUQDnR4XjewLBx4e3PC3/mXRoJneD6CbMAqaTqNZW.svg)

**Fig. 1:** A diagram of how the browser's primary HTML parser can be blocked. In this case, the parser runs into a `<link>` element for an external CSS file, which blocks the browser from parsing the rest of the document—or even rendering any of it—until the CSS is downloaded and parsed.

In the case of CSS files, both parsing and rendering are blocked in order to prevent a [flash of unstyled content (FOUC)](https://en.wikipedia.org/wiki/Flash_of_unstyled_content), which is when an unstyled version of a page can be seen briefly before styles are applied to it.

![The web.dev home page in an unstyled state (left) and the styled state (right).](https://web-dev.imgix.net/image/jL3OLOhcWUQDnR4XjewLBx4e3PC3/8LkMd46pUlwgfYvmTBrO.png?auto=format)

**Fig. 2:** A simulated example of FOUC. At left is the front page of web.dev without styles. At right is the same page with styles applied. The unstyled state can occur in a flash if the browser doesn't block rendering while a stylesheet is being downloaded and processed.

The browser also blocks parsing and rendering of the page when it encounters `<script>` elements without a `defer` or `async` attribute.

Scripts loaded from `<script>` elements with a [`type=module` attribute](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Modules#applying_the_module_to_your_html) are deferred by default.

The reason for this is that the browser can't know for sure if any given script will modify the DOM while the primary HTML parser is still doing its job. This is why it's been a common practice to load your JavaScript at the end of the document so that the effects of blocked parsing and rendering become marginal.

These are good reasons for why the browser _should_ block both parsing and rendering. Yet, blocking either of these important steps is undesirable, as they can hold up the show by delaying the discovery of other important resources. Thankfully, browsers do their best to mitigate these problems by way of a secondary HTML parser called a _preload scanner_.

![A diagram of both the primary HTML parser (left) and the preload scanner (right), which is the secondary HTML parser.](https://web-dev.imgix.net/image/jL3OLOhcWUQDnR4XjewLBx4e3PC3/6lccoVh4f6IJXA8UBKxH.svg)

**Fig. 3:** A diagram depicting how the preload scanner works in parallel with the primary HTML parser to speculatively load assets. Here, the primary HTML parser is blocked as it loads and processes CSS before it can begin processing image markup in the `<body>` element, but the preload scanner can look ahead in the raw markup to find that image resource and begin loading it before the primary HTML parser is unblocked.

[A preload scanner's role is speculative](https://html.spec.whatwg.org/multipage/parsing.html#speculative-html-parsing), meaning that it examines raw markup in order to find resources to opportunistically fetch before the primary HTML parser would otherwise discover them.

## How to tell when the preload scanner is working [#](https://web.dev/preload-scanner/#how-to-tell-when-the-preload-scanner-is-working)

The preload scanner exists _because_ of blocked rendering and parsing. If these two performance issues never existed, the preload scanner wouldn't be very useful. The key to figuring out whether a web page benefits from the preload scanner depends on these blocking phenomena, and to do that, we can introduce an artificial delay for requests to find out where the preload scanner is working.

Let's take [a page](https://preload-scanner-fights.glitch.me/artifically-delayed-requests.html) of basic text and images with a stylesheet. Because CSS files block both rendering and parsing, we can introduce an artificial delay of two seconds for the stylesheet through a proxy service. This delay makes it easier to see in the network waterfall where the preload scanner is working.

![The WebPageTest network waterfall chart illustrates an artificial delay of 2 seconds imposed on the styleesheet.](https://web-dev.imgix.net/image/jL3OLOhcWUQDnR4XjewLBx4e3PC3/Gtw08XaoFETKEauBBbBl.png?auto=format)

**Fig. 4:** A [WebPageTest](https://www.webpagetest.org/) [network waterfall chart](https://developer.chrome.com/docs/devtools/network/reference/#waterfall) of [a web page](https://preload-scanner-fights.glitch.me/artifically-delayed-requests.html) run on Chrome on a mobile device over a simulated 3G connection. Even though the stylesheet is artificially delayed through a proxy by two seconds before it begins to load, the image located later in the markup payload is discovered by the preload scanner.

As you can see in the waterfall, the preload scanner discovers the `<img>` element _even while rendering and document parsing is blocked_. Without this optimization, the browser can't fetch things opportunistically during the blocking period, and more resource requests would be consecutive rather than concurrent.

With that toy example out of the way, let's take a look at some real-world patterns where the preload scanner can be defeated—and what can be done to fix them.

This smattering of patterns isn't an exhaustive list, just some common ones.

## Injected `async` scripts [#](https://web.dev/preload-scanner/#injected-async-scripts)

Let's say you've got HTML in your `<head>` that includes some inline JavaScript like this:
