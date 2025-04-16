---
id: h9cbej0h6u45ebffps7xolh
title: Tailwind’s @apply Feature is Better Than it Sounds
desc: ""
updated: 1744452682511
created: 1744450131167
---

> https://css-tricks.com/tailwinds-apply-feature-is-better-than-it-sounds/

## Tailwind utilities are much better than Sass mixins

Tailwind’s utilities can be used directly in the HTML, so you don’t have to write a CSS rule for it to work.

On the contrary, for Sass mixins, you need to create an extra selector to house your @includes before using them in the HTML. That’s one extra step. Many of these extra steps add up to a lot.

```scss
@mixin some-mixin() {
  color: red;
  background: blue;
}

.selector {
  @include some-mixin();
}

/* Output */
.selector {
  color: red;
  background: blue;
}
```

Tailwind’s utilities can also be used with their responsive variants. This unlocks media queries straight in the HTML and can be a superpower for creating responsive layouts.

```css
@utility horizontal {
  display: flex;
  flex-direction: row;
  gap: 1rem;
}

@utility vertical {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
```

```html
<div class="vertical sm:horizontal">...</div>
```

## Tailwind’s utilities are a little less powerful compared to Sass mixins

Sass mixins are more powerful than Tailwind utilities because:

1. They let you use multiple variables.
2. They let you use other Sass features like @if and @for loops.

## Let’s go through another example

A second example I often like to showcase is the grid-simple utility that lets you create grids with CSS Grid easily.

We can declare a simple example here:

```css
@utility grid-simple {
  display: grid;
  grid-template-columns: repeat(var(--cols), minmax(0, 1fr));
  gap: var(--gap, 1rem);
}
```

By doing this, we have effectively created a reusable CSS grid (and we no longer have to manually declare minmax everywhere).

After we have defined this utility, we can use Tailwind’s arbitrary properties to adjust the number of columns on the fly.

```html
<div class="grid-simple [--cols:3]">
  <div class="item">...</div>
  <div class="item">...</div>
  <div class="item">...</div>
</div>
```

To make the grid responsive, we can add Tailwind’s responsive variants with arbitrary properties so we only set --cols:3 on a larger breakpoint.

```html
<div class="grid-simple sm:[--cols:3]">
  <div class="item">...</div>
  <div class="item">...</div>
  <div class="item">...</div>
</div>
```
