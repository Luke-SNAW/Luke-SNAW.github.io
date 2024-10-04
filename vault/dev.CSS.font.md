---
id: ujxz1y7bdvpazo3rn5yyr1c
title: CSS about font
desc: ""
updated: 1728021545323
created: 1647930628665
---

## Collections

- [The relative font weight axis — how variable fonts ease font weight transitions](https://www.stefanjudis.com/today-i-learned/the-relative-font-weight-axis-how-variable-fonts-ease-font-weight/)
- [Variable Fonts](https://v-fonts.com/)
- [Introducing four new international features in CSS](https://developer.chrome.com/blog/css-i18n-features?hl=en)
  - From Chrome 119: Japanese phrase line breaking with `word-break: auto-phrase`.
  - Behind a flag from Chrome 120: Inter-script spacing with the `text-autospace` property.
  - Under development: Chinese, Japanese, and Korean (CJK) punctuation kerning with the `text-spacing-trim` property.
- [Generally speaking, you’ll want to use `text-wrap: balance` for headings and `text-wrap: pretty` for body text.](https://codersblock.com/blog/nicer-text-wrapping-with-css-text-wrap/)
- [When to use CSS text-wrap: balance; vs text-wrap: pretty;](https://blog.stephaniestimac.com/posts/2023/10/css-text-wrap/)
  > Use text-wrap: balance; on headings and subheadings. And use text-wrap: pretty; on paragraphs of text to get rid of orphans on the last line. Despite the Chromium-only support, these would be a good candidate for progressive enhancement.
- [Cap Unit](https://ishadeed.com/article/css-cap-unit/)
- [Introducing TODS](https://clagnut.com/blog/2433/) – a typographic and OpenType default stylesheet
- [The problem with superscripts and subscripts](https://clagnut.com/blog/2434/)

## [Preventing layout shift with numbers using CSS](https://gomakethings.com/preventing-layout-shift-with-numbers-using-css/)

### An example

```html
<button data-count="down">Decrease</button>

<span class="count" aria-live="polite">
	0/5
</div>

<button data-count="up">Increase</button>
```

### The font-variant-numeric: tabular-nums property

```css
.count {
  font-variant-numeric: tabular-nums;
}
```
