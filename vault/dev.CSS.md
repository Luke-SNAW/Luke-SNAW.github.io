---
id: 14ndat1u737ts8fzosspizp
title: CSS
desc: ""
updated: 1646179098071
created: 1646129148306
---

- [Three important things you should know about CSS :is()](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/)
  - [The selector list of :is() is forgiving](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#forgiving): Invalid CSS selectors will simply be ignored.
  - [The specificity of :is() is that of its most specific argument](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#specificity)
  - [:is() does not work with pseudo-element selectors (for now)](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#simple-selectors)

# Cascade Precedence

- [The Entire Cascade (as a funnel)](https://codepen.io/miriamsuzanne/pen/gOXRzBa)

## Layers

### [Hello, CSS Cascade Layers](https://ishadeed.com/article/cascade-layers/)

To overcome the fights with the cascade and specificity issues, we need to be careful about where to write a specific CSS block. In small projects, this can be okay, but for large ones, it’s a time-consuming task. As a result, we started to see different methods to help us organize our CSS better and thus reducing the cascade issues. The first three that came to my mind are the [BEM](http://getbem.com/introduction/) (Block, Element, Modifier), [Smacss](http://smacss.com/) by Jonathan Snook and [Inverted Triangle CSS](https://itcss.io/) by Harry Roberts.

In this article, we’ll explore how cascade layers work, and how they will help us write CSS with more confidence, along with use-cases and examples.
