---
id: oimbwesaxcmy18o4ox870jp
title: CSS about scroll
desc: ""
updated: 1735542841357
created: 1712295949951
---

## Collections

- [Solved by CSS Scroll-Driven Animations: hide a header when scrolling down, show it again when scrolling up.](https://www.bram.us/2024/09/29/solved-by-css-scroll-driven-animations-hide-a-header-when-scrolling-up-show-it-again-when-scrolling-down/)

```css
* {
  scrollbar-width: thin;
  scrollbar-gutter: stable both-edges; // body에만 scroll을 두고 header와 body 영역이 차이나면 header에 활용할 수 있다.
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

```css
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

## [Chill Scroll Snapping: Article Headers](https://frontendmasters.com/blog/chill-scroll-snapping-article-headers/)

```css
html {
  scroll-snap-type: y mandatory;
}

main {
  h2,
  h3 {
    scroll-snap-stop: normal;
    scroll-snap-align: start;
  }
}
```

```css
main {
  max-width: 60ch;
  margin-inline: auto;
  h1,
  h2,
  > h1 + * {
    scroll-snap-stop: normal;
    scroll-snap-align: start;
  }
  > h1 + *,
  h2 {
    scroll-margin-block-start: 0.5rem;
  }
}

html {
  scroll-snap-type: y mandatory;
}
```

## [12 Modern CSS One-Line Upgrades](https://moderncss.dev/12-modern-css-one-line-upgrades/)

- Stable Enhancements: `accent-color`, `scroll-margin-top/bottom`
- progressive enhancement: `overscroll-behavior: contain`, `scrollbar-gutter`
- https://news.ycombinator.com/item?id=39176717

### scroll-margin-top/bottom

I like to include a generic starting rule in my reset for any element with an `[id]` attribute given it has the potential to become an anchor link.

```css
[id] {
  scroll-margin-top: 2rem;
}
```
