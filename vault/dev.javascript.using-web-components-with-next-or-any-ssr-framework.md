---
id: 0m8435q6gimt4pabubowi7m
title: Using Web Components With Next (or Any SSR Framework)
desc: ""
updated: 1668495759949
created: 1668473370396
---

> https://css-tricks.com/using-web-components-with-next-or-any-ssr-framework/

One serious shortcoming of Web Components is their current lack of support for server-side rendering (SSR). There is something called the Declarative Shadow DOM (DSD) in the works, but current support for it is pretty minimal, and it actually requires buy-in from your web server to emit special markup for the DSD. There’s currently work being done for [Next.js](https://nextjs.org/) that I look forward to seeing. But for this post, we’ll look at how to manage Web Components from any SSR framework, like Next.js, _today_.

## [The problem](https://css-tricks.com/using-web-components-with-next-or-any-ssr-framework/#aa-the-problem)

Before we dive in, let’s take a moment and actually explain the problem. Why don’t Web Components work well with server-side rendering?

Application frameworks like Next.js take React code and run it through an API to essentially “stringify” it, meaning it turns your components into plain HTML. So the React component tree will render on the server hosting the web app, and that HTML will be sent down with the rest of the web app’s HTML document to your user’s browser. Along with this HTML are some `<script>` tags that load React, along with the code for all your React components. When a browser processes these `<script>` tags, React will re-render the component tree, and match things up with the SSR’d HTML that was sent down. At this point, all of the effects will start running, the event handlers will wire up, and the state will actually… contain state. It’s at this point that the web app becomes _interactive_. The process of re-processing your component tree on the client, and wiring everything up is called **hydration**.

…React (or honestly _any_ JavaScript framework) will see those tags and simply pass them along. React (or Svelte, or Solid) are not responsible for turning those tags into nicely-formatted tabs. The code for that is tucked away inside of whatever code you have that defines those Web Components. In our case, that code is in the Shoelace library, but the code can be anywhere. What’s important is _when the code runs_.

Normally, the code registering these Web Components will be pulled into your application’s normal code via a JavaScript `import`. That means this code will wind up in your JavaScript bundle and execute during hydration which means that, between your user first seeing the SSR’d HTML and hydration happening, these tabs (or any Web Component for that matter) will not render the correct content. Then, when hydration happens, the proper content will display, likely causing the content around these Web Components to move around and fit the properly formatted content. This is known as a **flash of unstyled content**, or FOUC. In theory, you could stick markup in between all of those `<sl-tab-xyz>` tags to match the finished output, but this is all but impossible in practice, especially for a third-party component library.

## [Moving our Web Component registration code](https://css-tricks.com/using-web-components-with-next-or-any-ssr-framework/#aa-moving-our-web-component-registration-code)

So the problem is that the code to make Web Components do what they need to do won’t actually run until hydration occurs. For this post, we’ll look at running that code sooner; immediately, in fact. We’ll look at custom bundling our Web Component code, and manually adding a script directly to our document’s `<head>` so it runs immediately, and blocks the rest of the document until it does. _This is normally a terrible thing to do._ The whole point of server-side rendering is to _not_ block our page from processing until our JavaScript has processed. But once done, it means that, as the document is initially rendering our HTML from the server, the Web Components will be registered and will both immediately and synchronously emit the right content.

In our case, we’re _just_ looking to run our Web Component registration code in a blocking script. This code isn’t huge, and we’ll look to significantly lessen the performance hit by adding some cache headers to help with subsequent visits. **This isn’t a perfect solution.**

## [Custom bundling Web Component code](https://css-tricks.com/using-web-components-with-next-or-any-ssr-framework/#aa-custom-bundling-web-component-code)

## Loading the script

## [Improving performance](https://css-tricks.com/using-web-components-with-next-or-any-ssr-framework/#aa-improving-performance)

We could leave things as they are but let’s add caching for our Shoelace bundle. We’ll tell Next.js to make these Shoelace bundles cacheable by adding the following entry to our Next.js config file:

```javascript
async headers() {
  return [
    {
      source: "/shoelace/shoelace-bundle-:hash.js",
      headers: [
        {
          key: "Cache-Control",
          value: "public,max-age=31536000,immutable",
        },
      ],
    },
  ];
}
```

Now, on subsequent browses to our site, we see the Shoelace bundle caching nicely!

If our Shoelace bundle ever changes, the file name will change (via the `:hash` portion from the source property above), the browser will find that it does not have that file cached, and will simply request it fresh from the network.
