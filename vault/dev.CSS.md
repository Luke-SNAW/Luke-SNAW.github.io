---
id: 14ndat1u737ts8fzosspizp
title: CSS
desc: ""
updated: 1697782476531
created: 1646129148306
---

## Collections

- [The Guide To Responsive Design In 2023 and Beyond](https://ishadeed.com/article/responsive-design/)
- [When to Avoid the text-decoration Shorthand Property](https://css-tricks.com/when-to-avoid-css-text-decoration-shorthand/)
- [CSS underline bugs in Chrome](https://css-tricks.com/css-underlines-are-too-thin-and-too-low-in-chrome/)
- [revert](https://developer.mozilla.org/en-US/docs/Web/CSS/revert)
- [media query: hover](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/hover)
- [media query: pointer](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/pointer)
- [Dynamic CSS Secrets](https://projects.verou.me/talks/dynamic-css-secrets/#intro)
- The [env()](https://developer.mozilla.org/en-US/docs/Web/CSS/env) [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) [function](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions) can be used to insert the value of a user-agent defined environment variable into your CSS, in a similar fashion to the [`var()`](https://developer.mozilla.org/en-US/docs/Web/CSS/var) function and [custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*).
- Claymorphism
- [The evolution of scalable CSS](https://frontendmastery.com/posts/the-evolution-of-scalable-css/)
- [Document Object Model (DOM) Geometry: A Beginner’s Introduction And Guide](https://www.smashingmagazine.com/2022/11/document-object-model-geometry-guide/)
- [Let’s Make A Better “Light / Dark” Toggle](https://medium.com/codex/lets-make-a-better-light-dark-toggle-760499a8bc82)
- [CSS Style Queries](https://ishadeed.com/article/css-container-style-queries/)
- [Guide to image overlays in CSS](https://blog.logrocket.com/guide-image-overlays-css/)
- [12 CSS Tricks You Might Not Know](https://medium.com/@pythonlearn1024/12-css-tricks-you-might-not-know-3054475e861e)
- [Deploying CSS Logical Properties On Web Apps](https://www.smashingmagazine.com/2022/12/deploying-css-logical-properties-on-web-apps/)
  ```css
  margin-inline: auto;
  margin-block: 0;
  inset: 0;
  inset-inline: 10%;
  ```
- [How To Build A Magazine Layout With CSS Grid Areas](https://www.smashingmagazine.com/2023/02/build-magazine-layout-css-grid-areas/)
- [CSS Named Colors: Groups, Palettes, Facts, & Fun](https://austingil.com/css-named-colors/)
- [Easy implemented dark mode](https://twitter.com/flaviocopes/status/1627609246014619649)
  - Invert all colors, set a nice background, and invert again images and emojis so they look correctly.
  ```css
  @media (prefers-color-scheme: dark) {
    body {
      filter: invert(100%);
      background-color: rgb(29, 32, 31) !important;
    }
    img,
    .emoji {
      filter: invert(100%);
    }
  }
  ```
- [Resizing with CSS](https://css-irl.info/resizing-with-css/)
- [Everything You Need to Know About the Gap After the List Marker](https://css-tricks.com/everything-you-need-to-know-about-the-gap-after-the-list-marker/)
- [Laying Out a Print Book With CSS](https://iangmcdowell.com/blog/posts/laying-out-a-book-with-css/)
  - https://pagedjs.org/documentation/
  - https://www.print-css.rocks/
  - https://doc.courtbouillon.org/weasyprint/stable/
- [CSS Masking - Ahmad Shadeed](https://ishadeed.com/article/css-masking/)
- [Improving CSS Shapes with Trigonometric Functions](https://danielcwilson.com/posts/css-shapes-with-trig-functions/)
- [Understanding ITCSS: Real case using ITCSS](https://www.carloscaballero.io/understanding-itcss-real-case-using-itcss-https-carloscaballero-io/)
  - font가 settings에 들어가는게 맞아? 다른 articles에선 CSS generate 하는 곳이 아니라는데...
- [Resume and pause animations in CSS](https://www.amitmerchant.com/run-and-pause-animations-in-css/)
  - `animation-play-state` property. - `running` and `paused`
- [Tailwind, and the death of web craftsmanship](https://pdx.su/blog/2023-07-26-tailwind-and-the-death-of-craftsmanship/)
  > While Tailwind may help with initial development speed, it can reduce craftsmanship and make code harder to work with over time.
- [Understanding the Difference Between : and :: in CSS](https://medium.com/@islizeqiang/understanding-the-difference-between-and-in-css-64c9d36c21af)
  > :: are used to create additional elements within an element
- [Styling External Links with Attribute Selectors](https://css-irl.info/styling-external-links-with-attribute-selectors/)
  - Class contains the word 'link' - `a[class~='link']`
  - Case sensitive - `a[href*='css-irl' s]`
  - Case insensitive - `a[href*='css-irl' i]`

## Pseudo-class

- [CSS Features We’re Thankful For and CSS Features We Need](https://www.lullabot.com/articles/css-features-were-thankful-and-css-features-we-need)
  - OK - :is(), :where(), grid
  - not yet - :has(), subgrid
- [Three important things you should know about CSS :is()](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/)
  - [The selector list of :is() is forgiving](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#forgiving): Invalid CSS selectors will simply be ignored.
  - [The specificity of :is() is that of its most specific argument](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#specificity)
  - [:is() does not work with pseudo-element selectors (for now)](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#simple-selectors)
- [4 ways CSS :has() can make your HTML forms even better](https://austingil.com/css-has-with-html-forms/?utm_campaign=Frontend%2BWeekly&utm_medium=email&utm_source=Frontend_Weekly_337)

## Cascade Precedence

- [The Entire Cascade (as a funnel)](https://codepen.io/miriamsuzanne/pen/gOXRzBa)

### Layers

#### [Hello, CSS Cascade Layers](https://ishadeed.com/article/cascade-layers/)

To overcome the fights with the cascade and specificity issues, we need to be careful about where to write a specific CSS block. In small projects, this can be okay, but for large ones, it’s a time-consuming task. As a result, we started to see different methods to help us organize our CSS better and thus reducing the cascade issues. The first three that came to my mind are the [BEM](http://getbem.com/introduction/) (Block, Element, Modifier), [Smacss](http://smacss.com/) by Jonathan Snook and [Inverted Triangle CSS](https://itcss.io/) by Harry Roberts.

In this article, we’ll explore how cascade layers work, and how they will help us write CSS with more confidence, along with use-cases and examples.

## History

### [!important](https://twitter.com/stevenpemberton/status/1505839184287870981)

> CSS co-designer here.  
> !important was added for one reason only: laws in the US that require certain text to be in a given font-size. !important stops the cascade from changing it.  
> Anything else is probably misuse, and a sign you may not understand the cascade properly.

## SVG

### [Where, When, And When NOT To Use SVG!](https://medium.com/codex/where-when-and-when-not-to-use-svg-150d5a5d7592)

- When Shouldn’t We Use SVG?
  - Presentational monochrome images such as flat icons. Webfonts can be cached, the two modern formats of WOFF and WOFF2 compress much smaller than gzipping minified SVG.
- Is It Presentational And/Or Decoration? Then Don’t Put It In The Markup!
- If Not In The Markup, Where?
  - Your stylesheet. As a background-image.

## Styles

- [linear-gradient()](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/linear-gradient)
- [Web Design in 4 minutes](https://jgthms.com/web-design-in-4-minutes/)

### [columns](https://developer.mozilla.org/en-US/docs/Web/CSS/columns)

- [The True Power Of CSS Columns](https://medium.com/codex/the-true-power-of-css-columns-2e620ad66282)

## Functions

### [CSS image()](https://12daysofweb.dev/2022/css-image/#image-fragments)

```css
.hero {
  background-image: image("images/my-image.jpg#xywh=150,50,500,300");
}
```
