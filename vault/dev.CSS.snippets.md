---
id: g05lfgv5zmp5zwv7c40j8n1
title: CSS snippets
desc: ""
updated: 1701308062246
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

## [Preventing Scroll “Bounce” with CSS](https://css-irl.info/preventing-overscroll-bounce-with-css/)

```css
:root {
  overscroll-behavior: none;
}
```
