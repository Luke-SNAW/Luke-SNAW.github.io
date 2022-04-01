---
id: 14ndat1u737ts8fzosspizp
title: CSS
desc: ""
updated: 1648775957302
created: 1646129148306
---

- [Three important things you should know about CSS :is()](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/)

  - [The selector list of :is() is forgiving](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#forgiving): Invalid CSS selectors will simply be ignored.
  - [The specificity of :is() is that of its most specific argument](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#specificity)
  - [:is() does not work with pseudo-element selectors (for now)](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#simple-selectors)

- [When to Avoid the text-decoration Shorthand Property](https://css-tricks.com/when-to-avoid-css-text-decoration-shorthand/) - [CSS underline bugs in Chrome](https://css-tricks.com/css-underlines-are-too-thin-and-too-low-in-chrome/)
- [revert](https://developer.mozilla.org/en-US/docs/Web/CSS/revert)

# Cascade Precedence

- [The Entire Cascade (as a funnel)](https://codepen.io/miriamsuzanne/pen/gOXRzBa)

## Layers

### [Hello, CSS Cascade Layers](https://ishadeed.com/article/cascade-layers/)

To overcome the fights with the cascade and specificity issues, we need to be careful about where to write a specific CSS block. In small projects, this can be okay, but for large ones, it’s a time-consuming task. As a result, we started to see different methods to help us organize our CSS better and thus reducing the cascade issues. The first three that came to my mind are the [BEM](http://getbem.com/introduction/) (Block, Element, Modifier), [Smacss](http://smacss.com/) by Jonathan Snook and [Inverted Triangle CSS](https://itcss.io/) by Harry Roberts.

In this article, we’ll explore how cascade layers work, and how they will help us write CSS with more confidence, along with use-cases and examples.

# History

## [!important](https://twitter.com/stevenpemberton/status/1505839184287870981)

> CSS co-designer here.  
> !important was added for one reason only: laws in the US that require certain text to be in a given font-size. !important stops the cascade from changing it.  
> Anything else is probably misuse, and a sign you may not understand the cascade properly.
