---
id: xhw8n20kdyb7ymqntazh1eb
title: "How the CSS :is, :where and :has Pseudo-class Selectors Work"
desc: ""
updated: 1661901765786
created: 1661901394289
---

> https://www.sitepoint.com/css-is-where-has-pseudo-class-selectors/

> The zero specificity of `:where()` could be practical for CSS resets.

---

[Pseudo-class selectors](https://www.sitepoint.com/getting-to-know-css3-selectors-structural-pseudo-classes/) target HTML elements based on their current state. Perhaps the most well known is `:hover`, which applies styles when the cursor moves over an element, so it’s used to highlight clickable links and buttons. Other [popular options include](https://developer.mozilla.org/docs/Web/CSS/Pseudo-classes):

- `:visited`: matches visited links
- `:target`: matches an element targeted by a document URL
- `:first-child`: targets the first child element
- `:nth-child`: selects specific child elements
- `:empty`: matches an element with no content or child elements
- `:checked`: matches a toggled-on checkbox or radio button
- `:blank`: styles an empty input field
- `:enabled`: matches [an enabled input field](https://www.sitepoint.com/atoz-css-enabled-pseudo-class/)
- `:disabled`: matches a disabled input field
- `:required`: targets a required input field
- `:valid`: matches a valid input field
- `:invalid`: matches an invalid input field
- `:playing`: targets a playing audio or video element

Browsers have recently received three more pseudo-class selectors…

## The CSS :is Pseudo-class Selector

_Note: this was originally specified as `:matches()` and `:any()`, but `:is()` has become the CSS standard._

You often need to apply the same styling to more than one element. For example, `<p>` paragraph text is black by default, but gray when it appears within an `<article>`, `<section>`, or `<aside>`:

```css
/* default black */
p {
  color: #000;
}

/* gray in <article>, <section>, or <aside> */
article p,
section p,
aside p {
  color: #444;
}
```

This is a simple example, but more sophisticated pages will lead to more complicated and verbose selector strings. A syntax error in any selector could break styling for all elements.

CSS preprocessors such as Sass permit nesting (which is also coming to [native CSS](https://www.w3.org/TR/css-nesting-1/)):

```scss
article,
section,
aside {
  p {
    color: #444;
  }
}
```

This creates identical CSS code, reduces typing effort, and can prevent errors. But:

- Until native nesting arrives, you’ll need a CSS build tool. You may want to use an option like Sass, but that can introduce complications for some development teams.
- Nesting can cause other problems. It’s easy to construct deeply nested selectors that become increasingly difficult to read and output verbose CSS.

`:is()` provides a native CSS solution which has [full support in all modern browsers](https://caniuse.com/css-matches-pseudo) (not IE):

```css
:is(article, section, aside) p {
  color: #444;
}
```

A single selector can contain any number of `:is()` pseudo-classes. For example, the following complex selector applies a green text color to all `<h1>`, `<h2>`, and `<p>` elements that are children of a `<section>` which has a class of `.primary` or `.secondary` and which isn’t the first child of an `<article>`:

```css
article section:not(:first-child):is(.primary, .secondary) :is(h1, h2, p) {
  color: green;
}
```

The equivalent code without `:is()` required six CSS selectors:

```css
article section.primary:not(:first-child) h1,
article section.primary:not(:first-child) h2,
article section.primary:not(:first-child) p,
article section.secondary:not(:first-child) h1,
article section.secondary:not(:first-child) h2,
article section.secondary:not(:first-child) p {
  color: green;
}
```

Note that `:is()` can’t match `::before` and `::after` pseudo-elements, so this example code will fail:

```css
/* NOT VALID - selector will not work */
div:is(::before, ::after) {
  display: block;
  content: "";
  width: 1em;
  height: 1em;
  color: blue;
}
```

## The CSS :where Pseudo-class Selector

`:where()` selector syntax is identical to `:is()` and is also [supported in all modern browsers](https://caniuse.com/mdn-css_selectors_where) (not IE). It will often result in identical styling. For example:

```css
:where(article, section, aside) p {
  color: #444;
}
```

The difference is _[specificity](https://developer.mozilla.org/docs/Web/CSS/Specificity)_. **Specificity** is the algorithm used to determine which CSS selector should override all others. In the following example, `article p` is more specific than `p` alone, so all paragraph elements within an `<article>` will be gray:

```css
article p {
  color: #444;
}
p {
  color: #000;
}
```

In the case of `:is()`, the specificity is the most specific selector found within its arguments. In the case of `:where()`, the specificity is zero.

Consider the following CSS:

```css
article p {
  color: black;
}

:is(article, section, aside) p {
  color: red;
}

:where(article, section, aside) p {
  color: blue;
}
```

Let’s apply this CSS to the following HTML:

```html
<article>
  <p>paragraph text</p>
</article>
```

The paragraph text will be colored red.

The `:is()` selector has the same specificity as `article p`, but it comes later in the stylesheet, so the text becomes red. It’s necessary to remove both the `article p` and `:is()` selectors to apply a blue color, because the `:where()` selector is less specific than either.

More codebases will use `:is()` than `:where()`. However, the zero specificity of `:where()` could be practical for CSS resets, which apply a baseline of standard styles when no specific styling is available. Typically, resets apply a default font, color, paddings and margins.

## The CSS :has Pseudo-class Selector

The `:has()` selector uses a similar syntax to `:is()` and `:where()`, but it targets an element which _contains_ a set of others.
