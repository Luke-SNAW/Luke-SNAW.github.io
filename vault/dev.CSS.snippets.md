---
id: g05lfgv5zmp5zwv7c40j8n1
title: CSS snippets
desc: ""
updated: 1712646857029
created: 1646129148295
---

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
