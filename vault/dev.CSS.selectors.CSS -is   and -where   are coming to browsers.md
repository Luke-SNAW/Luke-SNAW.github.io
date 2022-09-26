---
id: klj47rj1y5agwo2kfj1lngz
title: 'CSS :is() and :where() are coming to browsers'
desc: ''
updated: 1646131563404
created: 1646131275423
---

https://webplatform.news/issues/2020-06-04

# Use :is() to reduce repetition

```css
/* BEFORE */
.embed .save-button:hover,
.attachment .save-button:hover {
  opacity: 1;
}

/* AFTER */
:is(.embed, .attachment) .save-button:hover {
  opacity: 1;
}
```

The specificity of `:is()` is determined by its **most specific selector** argument. See [Stefan Judis’s short video](https://twitter.com/stefanjudis/status/1264628338397777921) for an annotated example of this behavior.

# Use :where() to keep specificity low

The `:where()` pseudo-class has the same syntax and functionality as `:is()`. The only difference between them is that `:where()` doesn’t increase the overall selector’s specificity.

This functionality is useful for **styles that should be easy to override**. For example, the base stylesheet [sanitize.css](https://github.com/csstools/sanitize.css) includes the following style rule, which sets the default fill color if the `<svg fill>` attribute is missing:

```css
svg:not([fill]) {
  fill: currentColor;
}
```

Because of its higher specificity (B = 1, C = 1), a website cannot override this declaration with a single class selector (B = 1) and is forced to add !important or artificially increase the selector’s specificity (e.g., .share-icon.share-icon).

```css
.share-icon {
fill: blue; /_ doesn’t apply because of lower specificity _/
}
```

CSS libraries and base stylesheets can avoid this issue by wrapping their attribute selectors in :where() to keep the overall selector’s specificity low (C = 1).

```css
/_ sanitize.css _/
svg:where(:not([fill])) {
fill: currentColor;
}

/_ author stylesheet _/
.share-icon {
fill: blue; /_ applies because of higher specificity _/
}
```
