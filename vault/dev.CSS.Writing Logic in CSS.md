---
id: 88lzfool1v87yc2nzb1zojd
title: Writing Logic in CSS
desc: ""
updated: 1646871467352
created: 1646871370588
---

https://iamschulz.com/writing-logic-in-css/

# Control Structures

## Variables

```css
:root {
  --color: red;
}
span {
  color: var(--color, blue);
}
```

## Conditions

### Attribute Selectors:

```css
[data-attr="true"] {
  /* if */
}
[data-attr="false"] {
  /* elseif */
}
:not([data-attr]) {
  /* else */
}
```

### Pseudo Classes:

```css
:checked {
  /* if */
}
:not(:checked) {
  /* else */
}
```

### Media Queries:

```css
:root {
  color: red; /* else */
}
@media (min-width > 600px) {
  :root {
    color: blue; /* if */
  }
}
```

## Loops

```css
main {
  counter-reset: section;
}

section {
  counter-increment: section;
  counter-reset: section;
}

section > h2::before {
  content: "Headline " counter(section) ": ";
}
```

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
}
```

```css
section:nth-child(2n) {
  /* selects every even element */
}

section:nth-child(4n + 2) {
  /* selects every fourth, starting from the 2nd */
}
```

```css
section:nth-child(3n):not(:nth-child(6)) {
  /* selects every 3rd element, but not the 6th */
}
```

# [Logic Gates](https://css-tricks.com/logical-operations-with-css-variables/)

# Techniques

## The Owl Selector

```css
* + * {
  margin-top: 1rem;
}
```

## Conditional Styling

```css
.box {
  padding: 1rem 1rem 1rem calc(1rem + var(--s) * 4rem);
  color: hsl(0, calc(var(--s, 0) * 100%), 80%);
  background-color: hsl(0, calc(var(--s, 0) * 100%), 15%);
  border: calc(var(--s, 0) * 1px) solid hsl(0, calc(var(--s, 0) * 100%), 80%);
}

.icon {
  opacity: calc(var(--s) * 100%);
  transform: scale(calc(var(--s) * 100%));
}
```

## Automatic contrast colors

```css
:root {
  --theme-hue: 210deg;
  --theme-sat: 30%;
  --theme-lit: 20%;
  --theme-font-threshold: 51%;

  --background-color: hsl(var(--theme-hue), var(--theme-sat), var(--theme-lit));

  --font-color: hsl(
    var(--theme-hue),
    var(--theme-sat),
    clamp(
      10%,
      calc(100% - (var(--theme-lit) - var(theme-font-threshold)) * 1000),
      95%
    )
  );
}
```

## Setting Variables in JavaScript

```javascript
	// set --s on :root
	document.documentElement.style.setProperty('--s', e.target.value);

	// set --s scoped to #myID
	const el = document.querySelector('#myID');
	el.style.setProperty('--s', e.target.value);

	// read variables from an alement
	const switch = getComputedStyle(el).getPropertyValue('--s');
```
