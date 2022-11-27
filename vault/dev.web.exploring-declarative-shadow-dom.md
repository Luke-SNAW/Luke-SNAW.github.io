---
id: 0ohvsoricpxchkjku83k1pb
title: Exploring Declarative Shadow DOM
desc: ""
updated: 1669533912340
created: 1669533763271
---

> https://www.wiktorwisniewski.dev/blog/exploring-declarative-shadow-dom

Shadow DOM is part of Web Component feature, that allows to completely isolate separate DOM tree (shadow tree) and its CSS from the rest of the document. The benefit of that is performance because we are running code that is closer to the native API rather than framework abstraction layer. The second benefit is portability of the given component across multiple projects - even these that use frameworks like React / Angular / Vue under the hood. Side note: it's not supported out of the box. Check [Custom Elements Everywhere](https://custom-elements-everywhere.com/) for more details. Simply write once, reuse everywhere or safely distribute your component to third party pages, without worrying about speed.

Here's the most basic example:

```js
const specialDiv = document.getElementById("shadow-element")
const shadow = specialDiv.attachShadow({ mode: "open" })
const divElement = document.createElement("p")

divElement.innerHTML = "Paragraph contents"

shadow.appendChild(divElement)
```

```html
<div id="shadow-element"></div>
```

will become:

```html
<div id="shadow-element">
  #shadow-root (open)
  <p>Paragraph contents</p>
</div>
```

## Pitfalls

There are drawbacks that one needs to keep in mind when planning the use of web components:

- Doesn't work in JavaScript-less environments. JS is mandatory even if your component's logic doesn't require it.
- Web Components usually are deferred, which means they will be causing Content Layout Shift
- Rendering ShadowDOM on server is not possible because there are no declarative primitives for it\*

I want to emphasize here that the lack of support for server environments is a big issue. If you are a front-end developer you are probably aware of the (well justified) hype around Server Side Rendering. If you can't use your component on the server, the natural choice is to go with react-like components and not worry about limited use cases. What's the benefit of using components if you can use it only in some projects?

## Why Web Components do not work well in server environment?

Quick explanation on what is Server Side Rendering:

_On each request server is "rendering" HTML and serves it to a client with minimal JavaScript necessery for given document (based on that request). Well in fact it just prepares HTML string. On website load hydration happens and the page is fully interactive (lot's of buzzwords for good old-school style webdev)._

Now, the problem is, shadow root is highly dependent on browser environment and javascript initialization. We can't use `.attachShadow({mode: 'open' })` on the server and we can't write shadowDom declaritively as HTML string. For some APIs you just need a browser. In theory you could spin up a browser instance for build purposes but this strategy has plenty of downsides.

## Declarative ShadowDOM to the rescue!

It's a game changer not only because it challenges all server environment related problems. Declarative Shadow DOM addresses CLS issue as well and finally - we can benefit from ShadowDOM encapsulation without writing a single line of JavaScript. This is what I have used for my experiments:

🚀 Click Me[Source code at GitHub Gist](https://gist.github.com/wisniewski94/d28c1e8905c44b8b131c3bc472891e55)

The above example is quite easy to accomplish. The overall idea is to have a confetti button that stands as alternative to regular button element. I did not focus on forms and a11y this time as this article tries to aim for DSD only.

### HTML Markup

```html
<confetti-button>
  <template shadowroot="open">
    <style>
      ...;
    </style>
    <button>
      <slot></slot>
    </button>
    <canvas id="confetti"></canvas>
  </template>
  🚀 Click Me
</confetti-button>
<script>
  class ConfettiButton extends HTMLElement {
    ...
  }

  customElements.define('confetti-button', ConfettiButton);
</script>
```

Here we have a `confetti-button` custom element that wraps a template with shadowroot="open". That template is transfered into shadow dom when HTML parser finds it. We also have a canvas element that is used to draw confetti particles. The canvas element is positioned absolutely and covers the button element but using some css magic you can click through it. This way, the button element feels to be on top of the canvas element.

Button can be disabled as well by adding "disabled" property to it:

🚀 Click Me

### Styling custom elements

Just a brief example of most interesting parts:

```css
button { ... }
:host(:not([disabled])) button:hover { ... }
:host(:active) button:active, :host([disabled]) button { ... }

:host([disabled]) button {
  ...
  cursor: not-allowed;
}

canvas {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}
```

Template contains style tag with css that is used to style the button element. Note that I am placing large style tag inside web component on purpose. If I included it as a separate file, on slow connection I would risk getting FOUC or CLS. For more advanced styling that could be not the best approach as it comes at cost of larger HTML file, which takes more time to load.

The rule that I find the most interesting is `pointer-events: none;` because it makes clicking through canvas possible. Also you might notice that I'm using `:host([disabled])` selector instead of `:host(:disabled)`. The second one didn't work.

### JS in DSD - interesting parts

What's more important are gotchas that eventually you might encounter when working with Custom Elements. There are plenty of them but in terms of DSD, the one that took me quite a while to get over was accessing the shadowRoot. The "bug" that I was struggling with was trying to query shadowRoot inside constructor call:

```js
class ConfettiButton extends HTMLElement {
  constructor() {
    super();
    // DON'T DO THIS, shadowRoot probably is not available yet
    this.button = this.shadowRoot.querySelector('button');
  }
  ...
}
```

At the point of writing this component I was dead sure that you can do such things in constructor. If you can attach shadowRoot then why not access it, if it was created by DOM parser already, right? Well turns out this is not how it works. The constructor should be used to set up initial state, default values, event listeners and possibly a shadow root. What I have tried to accomplish here was fundamentally wrong and should be deferred to connectedCallback method according to [Custom Elements Comformance](https://html.spec.whatwg.org/#custom-element-conformance).

Another good point to make is that this custom element depends on its contents (template) so if you do:

```js
const myElement = document.createElement("confetti-button")
myElement.attachShadow({ mode: "open" })
document.body.append(myElement)
```

Then you will get an error because we are not using template that this custom element needs. It violates the rule of not using dependent elements. You won't be able to **imperatively** create a custom element that way. We could argue, that if you want to use regular element many times, you simply define it multiple times, but you might get a feeling that with element of this size and complexity we are heading in wrong direction. There is a way to store the element for the later use:

```html
<template id="chunk">
  <confetti-button>...</confetti-button>
</template>
<script>
  for (let i = 0; i < 10; i++)
    document.body.appendChild(chunk.content.cloneNode(true))
</script>
```

What if you can't use a template? This is where getInnerHTML() method comes in handy. It works similarly to innerHTML property but it returns a string that contains template with open shadowRoot

## Maybe you don't need Declarative Shadow DOM at all?

This is a great feature to use and understand but maybe it's not a must-have solution for you right now. Personally I consider it an interesting feature - a subset of great technologies yet to come. Questions and things to consider are:

1. Is your custom component visible above the fold?
2. If the nature of your component is interactive (e.g. datepicker) then SEO shouldn't be a concern.
3. For a small websites and high connection speeds the FOUC & CLS issue is not as visible as it is in slow devices and large projects.
4. You can still have a fallback in the light dom. That should work if component doesn't consume too much CSS.

Declarative Shadow DOM is available since Chrome 90 and Edge 91 (both running on Chromium so it counts as one). The great news is [Safari is prototyping.](https://github.com/WebKit/WebKit/pull/4693) Assuming Mozilla is interested in declarative solutions, it means we are closer to get DSD on all major browsers 👀...

WebComponents are improving over time thus solving current issues and bringing the perspective of landing newer frameworks and applications. There are already great frameworks built on top of WebComponents that will benefit from this implementation as well (e.g. StencilJS, Lit). Declarative Shadow DOM will finally solve the issue of Server Side Rendering and Web Components. It's one more step towards better specification!

References:

1. [https://html.spec.whatwg.org/#custom-element-conformance](https://html.spec.whatwg.org/#custom-element-conformance)
2. [https://github.com/whatwg/dom/issues/831](https://github.com/whatwg/dom/issues/831)
3. [https://github.com/mfreed7/declarative-shadow-dom/blob/master/README.md](https://github.com/mfreed7/declarative-shadow-dom/blob/master/README.md)
4. [https://web.dev/declarative-shadow-dom/](https://web.dev/declarative-shadow-dom/)
