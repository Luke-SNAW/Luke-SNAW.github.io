
## Collections

- [SmolCSS](https://smolcss.dev): Minimal snippets for modern CSS layouts and components
- [Tree views in css](https://iamkate.com/code/tree-views/) - `details open`

## [Outlining The Page](https://ishadeed.com/article/threads-app-css-part-2/#outlining-the-page)

It’s important to remember that anything you see on the screen is a box, even if it’s a circle or a `1px` separator. Everything is a box.

```css
*,
*:before,
*:after {
  outline: solid 0.5px #db6a7d;
  border: 0;
}
```

An outline with `0.5px` width. I picked half a pixel so that it’s easier to look at the boxes. I also removed all borders as they cause confusion.

## [Image inside div has extra space below the image](https://stackoverflow.com/questions/5804256/image-inside-div-has-extra-space-below-the-image)

```css
img {
  display: block;
}
```

## [How to align the text of the last paragraph line](https://www.stefanjudis.com/today-i-learned/how-to-align-the-text-of-the-last-paragraph-line/)

> `text-align-last`

## [How to think about HTML responsive images](https://danburzo.ro/responsive-images-html/)

```html
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="macos-dark.png" />
  <source media="print" srcset="macos-contrast.png" />
  <img src="macos-light.png" alt="…" />
</picture>
```

## [The Power of :has() in CSS](https://css-tricks.com/the-power-of-has-in-css/)

```css
h1:has(+ h2) {
  color: blue;
}
```

## Default setting

```scss
// fonts
* {
  &:lang(ko) {
    word-break: keep-all;
  }
  &:lang(en) {
    word-break: keep-all;
  }
  &:lang(ja) {
    word-break: normal;
    word-break: auto-phrase; // From Chrome 119. https://developer.chrome.com/blog/css-i18n-features?hl=en
  }
}
*,
code,
kbd,
samp,
pre {
  // 따로 지정하지 않고 *만 쓰면 나머지 tag는 tailwind 기본 reset style이 적용됨.
  font-family: "Apple SD Gothic Neo", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
    "Segoe UI Symbol";
  word-break: keep-all;
  -webkit-font-smoothing: antialiased;
}

// #region text-wrap - https://codersblock.com/blog/nicer-text-wrapping-with-css-text-wrap/#in-closing
h1,
h2,
h3,
h4,
h5,
h6 {
  text-wrap: balance;
}
div,
p {
  text-wrap: pretty;
}
// #endregion

// reset
@layer reset {
  @tailwind base;

  body {
    @apply text-16 text-grey-900;
  }
}
```

## [Get The Screen Width & Height Without JavaScript](https://css-tip.com/screen-dimension/)

```css
@property --_w {
  syntax: "<length>";
  inherits: true;
  initial-value: 100vw;
}
@property --_h {
  syntax: "<length>";
  inherits: true;
  initial-value: 100vh;
}
:root {
  --w: tan(atan2(var(--_w), 1px)); /* screen width */
  --h: tan(
    atan2(var(--_h), 1px)
  ); /* screen height*/ /* The result is an integer without unit */
}
```

## [A guide to image overlays in CSS](https://blog.logrocket.com/css-overlay/)

```html
<div class="image-wrapper">
  <img src="" alt="Sample Image" width="800" height="600" />
  <div class="overlay-text">The Pros and Cons of Buying vs. Renting a Home</div>
</div>
```

```css
.image-wrapper::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.3);
}
```

```css
.image-wrapper {
  position: relative;
  /* Other styles */
}
```

## [adactio](https://adactio.com/journal/21896)

For instance, I’m a huge fan of view transitions and I enable them by default on every new project, but I do it like this:

```css
@media (prefers-reduced-motion: no-preference) {
  @view-transition {
    navigation: auto;
  }
}
```

```css
ul,
ol,
dl,
dt,
dd,
p,
figure,
blockquote {
  hanging-punctuation: first last;
  text-wrap: pretty;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  text-align: center;
  text-wrap: balance;
}
```

## [The Universal Focus Ring](https://css-tip.com/universal-focus/)

```css
html::after {
  content: "";
  position: fixed;
  position-anchor: --focus;
  inset: anchor(inside, 0);
  outline: 2px solid darkred;
  transition: 0.4s;
}
*:focus-visible {
  outline: none;
  anchor-name: --focus;
}
```
