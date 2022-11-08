---
id: k4r693vts8lh7ejabcayhgc
title: sass-the-map-merge-pattern
desc: ""
updated: 1667880013562
created: 1667879854774
published: false
---

> https://medium.com/the-code-less-travelled/sass-the-map-merge-pattern-b948dc518d29

```scss
// src/scss/color.scss
$dark: #222 !default;
$light: #fefefe !default;

// src/components/card.scss
@use '../scss/color' as clr with (
  $dark: #111,
  $light: #EFEFEF,
);
.card {
  background-color: clr.$dark,
  color: clr.$light,
}
```

```scss
@use 'sass:map';
$dark: #222;
$light: #FEFEFE;
$-default-colors: (
  dark: $dark,
  light: $light,
);
$colors: () !default;
$palette: map.merge($-default-colors, $colors);
@each $key, $value in $palette {
  .clr-#{$key} {
    color: $value;
  }
  .clr-#{$key}\! {
    color: $value !important;
  }
}}
```
