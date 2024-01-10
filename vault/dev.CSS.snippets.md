---
id: g05lfgv5zmp5zwv7c40j8n1
title: CSS snippets
desc: ""
updated: 1704786053882
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

## [CSS Scroll Snapping Aligned With Global Page Layout: A Full-Width Slider Case Study](https://www.smashingmagazine.com/2023/12/css-scroll-snapping-aligned-global-page-layout-case-study/)

```scss
.slider {
  display: flex;
  gap: 24px;
  overflow-x: auto;
  scroll-snap-type: x mandatory;

  > * {
    flex: 0 0 300px;
    scroll-snap-align: start;
  }

  padding-inline: var(--offset-width);
  scroll-padding-inline-start: var(--offset-width);
}
```

## [6 CSS snippets every front-end developer should know in 2023](https://web.dev/articles/6-css-snippets-every-front-end-developer-should-know-in-2023?hl=en)

````css
.snaps {
  overflow-x: scroll;
  scroll-snap-type: x mandatory;
  overscroll-behavior-x: contain;
}

.snap-target {
  scroll-snap-align: center;
}

.snap-force-stop {
  scroll-snap-stop: always;
}
```
### [Why Techniques Like This Are Important](https://www.smashingmagazine.com/2023/12/css-scroll-snapping-aligned-global-page-layout-case-study/#why-techniques-like-this-are-important)

The best thing about using custom properties to handle calculations is that they are **lighter** and **more performant** than attempting to handle them in JavaScript.
````
