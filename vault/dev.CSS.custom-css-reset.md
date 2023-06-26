---
id: 485cilvluui6obotpvdb8x7
title: My Custom CSS Reset
desc: ""
updated: 1687160569328
created: 1687160203890
---

> https://www.joshwcomeau.com/css/custom-css-reset/

```css
/*
  1. Use a more-intuitive box-sizing model.
*/
*,
*::before,
*::after {
  box-sizing: border-box;
}
/*
  2. Remove default margin
*/
* {
  margin: 0;
}
/*
  Typographic tweaks!
  3. Add accessible line-height
  4. Improve text rendering
*/
body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
}
/*
  5. Improve media defaults
*/
img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}
/*
  6. Remove built-in form typography styles
*/
input,
button,
textarea,
select {
  font: inherit;
}
/*
  7. Avoid text overflows
*/
p,
h1,
h2,
h3,
h4,
h5,
h6 {
  overflow-wrap: break-word;
}
/*
  8. Create a root stacking context
*/
#root,
#__next {
  isolation: isolate;
}
```

## 3. Tweaking line-height

Here's the problem: for those who are dyslexic, these lines are packed too closely together, making it harder to read. The WCAG criteria states that [line-height should be at least 1.5](https://www.w3.org/WAI/WCAG21/Understanding/text-spacing.html).

```css
/* Proceed with caution. I'm still in the process of experimenting with this one.x */
* {
  line-height: calc(1em + 0.5rem);
}
```

## 4. Font smoothing

```css
body {
  -webkit-font-smoothing: antialiased;
}
```

Alright, so this one is a bit controversial.

On MacOS computers, the browser will use “subpixel antialiasing” by default. This is a technique that aims to make text easier to read, by leveraging the R/G/B lights within each pixel.

In the past, this was seen as an accessibility win, because it improved text contrast. You may have read a popular blog post, [Stop “Fixing” Font Smoothing](https://usabilitypost.com/2012/11/05/stop-fixing-font-smoothing/), that advocates _against_ switching to “antialiased”.

Here's the problem: that article was written in 2012, before the era of high-DPI “retina” displays. Today's pixels are much smaller, invisible to the naked eye.

The physical arrangement of pixel LEDs has changed as well. If you look at a modern monitor under a microscope, you won't see an orderly grid of R/G/B lines anymore.

In MacOS Mojave, released in 2018, Apple disabled subpixel antialiasing across the operating system. I'm guessing they realized that it was doing more harm than good on modern hardware.

Confusingly, MacOS browsers like Chrome and Safari still use subpixel antialiasing by default. We need to explicitly turn it off, by setting `-webkit-font-smoothing` to `antialiased`.

## 8. Root stacking context

```css
#root,
#__next {
  isolation: isolate;
}
```

This last one is optional. It's generally only needed if you use a JS framework like React.

As we saw in [“What The Heck, z-index??”](https://www.joshwcomeau.com/css/stacking-contexts/), the `isolation` property allows us to create a new stacking context without needing to set a `z-index`.

This is beneficial since it allows us to guarantee that certain high-priority elements (modals, dropdowns, tooltips) will always show up above the other elements in our application. No weird stacking context bugs, no z-index arms race.

You should tweak the selector to match your framework. We want to select the top-level element that your application is rendered within. For example, create-react-app uses a `<div id="root">`, so the correct selector is `#root`.
