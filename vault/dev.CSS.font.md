---
id: ujxz1y7bdvpazo3rn5yyr1c
title: CSS about font
desc: ""
updated: 1706851082557
created: 1647930628665
---

## Collections

- [The relative font weight axis — how variable fonts ease font weight transitions](https://www.stefanjudis.com/today-i-learned/the-relative-font-weight-axis-how-variable-fonts-ease-font-weight/)
- [Variable Fonts](https://v-fonts.com/)
- [Generally speaking, you’ll want to use `text-wrap: balance` for headings and `text-wrap: pretty` for body text.](https://codersblock.com/blog/nicer-text-wrapping-with-css-text-wrap/)

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
