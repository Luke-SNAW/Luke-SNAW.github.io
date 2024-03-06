---
id: b6u18z9o90yxv9ww6d2jd54
title: A practical guide to using shadow DOM
desc: ""
updated: 1709705872688
created: 1709705567431
---

> https://www.mayank.co/blog/declarative-shadow-dom-guide/

## [What the heck is “shadow DOM”?](https://www.mayank.co/blog/declarative-shadow-dom-guide/#what-the-heck-is-shadow-dom)

There have been hundreds of attempts at explaining shadow DOM, and it still remains confusing for many developers. I find that the [MDN page for shadow DOM](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) does a pretty decent job of explaining it, so I’d recommend reading it if you haven’t already. (Fun fact: When I started writing this post, MDN didn’t even document the [declarative syntax](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM#declaratively_with_html))

> Shadow DOM enables you to attach a DOM tree to an element, and have the internals of this tree hidden from JavaScript and CSS running in the page.

There is one frequently-misunderstood bit that I’d like to clear up though. Regular DOM content (commonly known as “light DOM”) can be [_slotted_](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/slot) inside shadow DOM. The shadow trees can be thought of as donuts, where the holes may be filled by light DOM content. This light DOM content continues to stay in the light DOM (rather than being somehow “transported” into the shadow DOM). The content from shadow DOM and light DOM is then interleaved to create the final DOM tree.

Visualization showing how light DOM and shadow DOM can be interleaved to create a combined final tree. Show separate trees

To really drive this point home, I recommend enabling “user-agent shadow DOM” in devtools. This will allow you to peek inside the shadow DOM of built-in DOM elements (such as `<details>`). The content that you pass into these elements stays in the light DOM, and only gets “revealed” by the user-agent shadow DOM.

[Screenshot of Chrome devtools showing the internal shadow DOM of the details element, containing two slots, one for the summary and another for the details content, both of which are revealed in the light DOM](https://www.mayank.co/_astro/details-shadow-dom.5qr6msYq_Z1kyELs.webp)

## [“Imperative” vs “declarative”](https://www.mayank.co/blog/declarative-shadow-dom-guide/#imperative-vs-declarative)

Previously, we had to rely on client-side JavaScript to _imperatively_ attach a shadow root to an element.

```js
element.attachShadow({ mode: "open" })
element.shadowRoot.innerHTML = `<p>Hello from the shadows!</p>`
```

This JavaScript requirement made shadow DOM a non-starter for the vast majority of use cases. I used it almost exclusively for optional enhancements that are not critical to the initial page load. Even then, the developer ergonomics of imperatively attaching a shadow root and populating its content felt awkward at best. And of course, it simply does not work when JavaScript isn’t available.

With _declarative_ shadow DOM, we can now express our shadow trees right in our HTML! The browser will attach the shadow root as soon as it encounters it, before any JavaScript even loads.

```html
<div>
  <template shadowrootmode="open">
    <p>This is "hidden" inside shadow DOM</p>
    <slot></slot>
  </template>
  <p>This is the regular ol' content</p>
</div>
```

The `<template>` will also be automatically removed from the DOM, so when you the inspect the element in dev tools, it feels as if the shadow root came pre-attached with the element.

(And yes, shadow DOM can be used with `<div>`, as well as some [other built-in elements](https://developer.mozilla.org/en-US/docs/Web/API/Element/attachShadow#elements_you_can_attach_a_shadow_to), including `<body>`, `<p>`, and `<span>`.)

[Screenshot of Chrome devtools showing an expanded shadow-root, with a slot revealing the light DOM content](https://www.mayank.co//_astro/shadowroot-devtools.ydyS5wmq_u5ffD.webp)

A couple more important things to note:

- Declarative shadow DOM is an [HTML parser feature](https://developer.chrome.com/docs/css-ui/declarative-shadow-dom#parser-only). It will not work if you try to set it inside `innerHTML`, for example. To create shadow trees from within JavaScript, the imperative `attachShadow` method should be used instead (at least until we get new DOM APIs like [`setHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/setHTML)).
- Be careful about newlines. Writing `<template>` in its own line makes sense for readability, but you might inadvertently end up slotting whitespace into the default `<slot>` (and thereby overriding the fallback slot content) if you have nothing else in the light DOM.

## [Use cases](https://www.mayank.co/blog/declarative-shadow-dom-guide/#use-cases)

I often get asked “Why should I care about shadow DOM?” Well, here’s a non-exhaustive list of ways in which shadow DOM can come in handy today:

- invisible [hover triangles](https://www.mayank.co/blog/hover-triangles)
- invisible rectangles for increasing [tap target size](https://ishadeed.com/article/target-size)
- ”handles” for resizing and dragging dialogs/panels/columns
- wrapper elements for [virtual scrolling/windowing](https://github.com/bvaughn/react-window)
- sibling elements for [focus trapping](https://react-spectrum.adobe.com/react-aria/FocusScope.html)
- ”overlapping”/duplicated elements (such as [GitHub’s code view](https://github.blog/2023-06-21-crafting-a-better-faster-code-view/#how-the-pieces-fit-together))
- decorative hover effects and animations for landing pages
- [visually-hidden](https://www.tpgi.com/the-anatomy-of-visually-hidden/) text for improved accessibility
- visual hints for drag-and-drop interfaces
- 3D objects and complex SVGs
- [out-of-order HTML streaming](https://lamplightdev.com/blog/2024/01/10/streaming-html-out-of-order-without-javascript/)
- changing or enforcing source order of slotted content
- ”passthrough”/noop shadow roots to access shadowDOM-specific features (such as [`slotchange`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLSlotElement/slotchange_event))

In almost all of the above cases, most of the critical content stays in the light DOM, and shadow DOM is only used for enhancing the baseline experience and/or hiding unimportant implementation details. Even if some of these things could be achieved using light DOM only, I find it valuable to hide the messy bits inside shadow DOM. It greatly improves the debugging experience, by reducing the amount of [div soup](https://css-tricks.com/twitters-div-soup-and-uglyfied-css-explained/) generated in the light DOM tree. It also allows me to opaquely make changes within shadow DOM without affecting any of the “outside” DOM selectors and such.

There are also some scenarios where complete encapsulation may be desired, in which case the content can be fully rendered (rather than slotted) inside shadow DOM:

- isolated iframe-like views (e.g. interactive demos, like the one above)
- third-party widgets and ads
- [microfrontends](https://microfrontend.dev/)

## [Style scoping and cascading](https://www.mayank.co/blog/declarative-shadow-dom-guide/#style-scoping-and-cascading)

It is very important to understand how styles work in shadow DOM.

Perhaps the easiest thing to understand is that styles inside a shadow tree do not affect anything outside it, and styles outside the shadow tree do not affect anything inside it. This is a stronger form of scoped styling (more accurately called “style encapsulation”), in that it allows you to write very weak selectors, at the expense of giving up the ability to use external styles.

```html
<head>
  <style>
    p {
      color: blue;
    }
  </style>
</head>
<body>
  <div>
    <template shadowrootmode="open">
      <style>
        p {
          color: red;
        }
      </style>
      <p>This is red.</p>
      <slot></slot>
    </template>
    <p>This is blue.</p>
  </div>
</body>
```

What may not be obvious is that [shadow DOM styles are cascaded _before_ document styles](https://knowler.dev/blog/a-mental-model-for-styling-the-shadow-dom). This means that `:host` styles will always lose to any “outside” styles, regardless of specificity (unless you use `!important`).

```html
<head>
  <style>
    :where(div) {
      color: blue;
    }
  </style>
</head>
<body>
  <div>
    <template shadowrootmode="open">
      <style>
        :host {
          color: red;
        }
      </style>
      <p>This is also blue!</p>
      <slot></slot>
    </template>
    <p>This is blue.</p>
  </div>
</body>
```

Lastly, [CSS shadow parts](https://css-tricks.com/styling-in-the-shadow-dom-with-css-shadow-parts/) can be used to selectively allow external styles into shadow DOM. I won’t bother explaining it, because there are many existing guides on the topic, and frankly, I’ve never needed to use it. Custom properties and slots can go pretty far already.

## [Shadow DOM is still problematic](https://www.mayank.co/blog/declarative-shadow-dom-guide/#shadow-dom-is-still-problematic)

I find it very strange that we didn’t have a declarative syntax for using shadow DOM until just now. Better late than never, I suppose. Still, it’s just a _syntax_. It does not really fix any of the larger [problems with shadow DOM](https://www.matuzo.at/blog/2023/pros-and-cons-of-shadow-dom/), most importantly around [styling](https://github.com/WICG/webcomponents/issues/909), [accessibility](https://alice.pages.igalia.com/blog/how-shadow-dom-and-accessibility-are-in-conflict/), and [form participation](https://kinsta.com/blog/web-components/#ignored-inputs). In fact, declarative shadow DOM introduces another problem of having to repeat the `<template>` for every single instance.

I’ve been able to work around the main styling issues by manually injecting my global stylesheets into all shadow trees. However, this is not a proper solution and only works for my own components (unless I rely on JavaScript, which… no thanks).

```html
<template shadowrootmode="open">
  <link rel="stylesheet" href="utilities.css" />
  <span class="visually-hidden">Utility classes work!</span>
  <slot></slot>
</template>
```

To get around the other issues, here’s my rule of thumb: do _not_ put any interactive form controls or semantically-important elements inside shadow DOM. As long as these stay in the light DOM and are slotted into shadow DOM, we can avoid most of the shadow nonsense. As a bonus, common patterns like `document.activeElement` and `:has(:focus-visible)` will work correctly, and the debugging experience will also be improved.

```
// ❌<my-input></my-input>
// ✅<my-input> <input /></my-input>
```

```
// ❌<my-button></my-button>
// ✅<my-button> <button>…</button></my-button>
```

## [Usage within frameworks](https://www.mayank.co/blog/declarative-shadow-dom-guide/#usage-within-frameworks)

Most of us are probably building websites using some kind of framework, or at least a templating engine. I think frameworks play a crucial role in using shadow DOM at scale, particularly because [web components are not components](https://www.mayank.co/blog/web-components-are-not-components). These frameworks can effectively serve as a polyfill for some of the missing web component APIs.

Broadly speaking, there are two kinds of web frameworks, and declarative shadow DOM interacts differently with them.

1. **Server-first frameworks** (e.g. Astro, WebC, Enhance): Since these frameworks are primarily concerned with producing HTML on the server, declarative shadow DOM generally works fine here (as long as you manage to produce the correct HTML).
2. **Client-first frameworks** (e.g. (P)react, Vue, Svelte): These frameworks support server-side rendering, but they tend to “hydrate” (recreate) the server-generated markup on the client, which does not play well with declarative shadow DOM. It’s possible to work around though, by using imperative code on the client.

I’ll have a more detailed follow-up post demonstrating how declarative shadow DOM can be used within various frameworks, so stay tuned. 👀

You may have noticed I didn’t mention custom elements anywhere in this article. That’s not an accident. Custom elements and shadow DOM are independent web component APIs that do not always need to be used together. Custom elements may be completely unnecessary when using a client-side JavaScript framework which already knows how to manage its own rendering lifecycle. In such cases, it totally makes sense to use shadow DOM without custom elements.
