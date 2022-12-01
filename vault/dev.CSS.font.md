---
id: ujxz1y7bdvpazo3rn5yyr1c
title: font
desc: ""
updated: 1669852896790
created: 1647930628665
---

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
