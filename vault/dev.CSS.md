---
id: 14ndat1u737ts8fzosspizp
title: CSS
desc: ""
updated: 1762221967878
created: 1646129148306
---

## Collections

- [The Guide To Responsive Design In 2023 and Beyond](https://ishadeed.com/article/responsive-design/)
- [When to Avoid the text-decoration Shorthand Property](https://css-tricks.com/when-to-avoid-css-text-decoration-shorthand/)
- [CSS underline bugs in Chrome](https://css-tricks.com/css-underlines-are-too-thin-and-too-low-in-chrome/)
- [revert](https://developer.mozilla.org/en-US/docs/Web/CSS/revert)
- [Dynamic CSS Secrets](https://projects.verou.me/talks/dynamic-css-secrets/#intro)
- The [env()](https://developer.mozilla.org/en-US/docs/Web/CSS/env) [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) [function](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions) can be used to insert the value of a user-agent defined environment variable into your CSS, in a similar fashion to the [`var()`](https://developer.mozilla.org/en-US/docs/Web/CSS/var) function and [custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*).
- Claymorphism
- [The evolution of scalable CSS](https://frontendmastery.com/posts/the-evolution-of-scalable-css/)
- [Document Object Model (DOM) Geometry: A Beginner’s Introduction And Guide](https://www.smashingmagazine.com/2022/11/document-object-model-geometry-guide/)
- [Let’s Make A Better “Light / Dark” Toggle](https://medium.com/codex/lets-make-a-better-light-dark-toggle-760499a8bc82)
- [Guide to image overlays in CSS](https://blog.logrocket.com/guide-image-overlays-css/)
- [12 CSS Tricks You Might Not Know](https://medium.com/@pythonlearn1024/12-css-tricks-you-might-not-know-3054475e861e)
- [Deploying CSS Logical Properties On Web Apps](https://www.smashingmagazine.com/2022/12/deploying-css-logical-properties-on-web-apps/)
  ```css
  margin-inline: auto;
  margin-block: 0;
  inset: 0;
  inset-inline: 10%;
  ```
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
- [Styling External Links with Attribute Selectors](https://css-irl.info/styling-external-links-with-attribute-selectors/)
  - Class contains the word 'link' - `a[class~='link']`
  - Case sensitive - `a[href*='css-irl' s]`
  - Case insensitive - `a[href*='css-irl' i]`
- [CSS Wrapped: 2023!](https://developer.chrome.com/blog/css-wrapped-2023?hl=en)
- [Essential Tips and Tricks for Coding HTML Emails](https://www.sitepoint.com/html-email-tips-tricks/)
- [Using the CSS contain property: A deep dive](https://blog.logrocket.com/using-css-contain-property-deep-dive/)
  > to decrease the burden on browsers for layout calculations, paints, repaints, and reflows.
- [A Guide To Designing For Older Adults](https://www.smashingmagazine.com/2024/02/guide-designing-older-adults/)
  > Today, one billion people are 60 years or older. That’s 12% of the entire world population, and the age group is growing faster than any other group. Yet, online, the needs of older adults are often overlooked or omitted.
  - Avoid **disappearing messages**: let users close them.
  - Avoid long, fine drag gestures and **precision**.
  - Avoid **floating labels** and use static field labels instead.
  - Don’t rely on **icons** alone: add descriptive labels.
  - Ask for **explicit confirmation** for destructive actions.
  - Add a **“Back” link** in addition to the browser’s “Back” button.
  - In forms, present one question or **one topic per screen**.
  - Use sufficient **contrast** (particularly shades of blue/purple and yellow/green can be hard to distinguish).
  - Make **error messages** helpful and forgiving.
- [Blur radius comparison](https://bjango.com/articles/blurradiuscomparison/)
  > the three Sketch blur types, scaled to the equivelent CSS box-shadow value. They now all match!
- [CSS :has() Interactive Guide](https://ishadeed.com/article/css-has-guide)
- [CSS scoping from What You Need to Know about Modern CSS (Spring 2024 Edition)](https://frontendmasters.com/blog/what-you-need-to-know-about-modern-css-spring-2024-edition/#scoping)
- [Old CSS, new CSS](https://eev.ee/blog/2020/02/01/old-css-new-css/)
  > > `<H1><FONT COLOR=red>...</FONT></H1>` …every single goddamn time.
  >
  > is in fashion again! Only now it’s called class="text-red-500" [:o)](https://news.ycombinator.com/item?id=40029373)
- [Hardest Problem in Computer Science: Centering Things](https://tonsky.me/blog/centering/)
  > STOP. USING. FONTS. FOR. ICONS.
- [Gap is the new Margin](https://frontendmasters.com/blog/gap-is-the-new-margin/)
  > > [Margin breaks component encapsulation.](https://mxstbr.com/thoughts/margin/) A well-built component should not affect anything outside itself.  
  > > [Prediction](https://dev.to/argyleink/5-css-predictions-for-2020-pl3): margins in stylesheets will decline as gap in stylesheets climb
- [CSS: Specificity](https://thevalleyofcode.com/css/4-specificity)
- [Double your specificity with this one weird trick](https://cirrus.twiddles.com/blog/2024/08/21/double-your-specificity-with-this-one-weird-trick/)
  - `.checkbox__icon.checkbox__icon`
    > "Repeated occurrences of the same simple selector are allowed and do increase specificity." — [CSS Selectors Level 4](https://www.w3.org/TR/selectors-4/#specificity-rules)
- [The Times You Need A Custom @property Instead Of A CSS Variable](https://www.smashingmagazine.com/2024/05/times-need-custom-property-instead-css-variable/)
  > CSS custom properties allow developers to specify the syntax, initial value, and inheritance behavior of CSS variables.
  > This provides more control over how variables are used, enabling advanced animations that were previously only possible with JavaScript.
- [CSS Length Units](https://css-tricks.com/css-length-units/)
- [CSS display contents](https://ishadeed.com/article/display-contents/)
- [CSS margin-trim and line height units](https://12daysofweb.dev/2024/css-margin-trim-line-height-units/)
- [KRDS v1.0.0](https://www.krds.go.kr/html/site/index.html) - 대한민국 정부 디자인 시스템
- [Relative Colors](https://ishadeed.com/article/css-relative-colors/) - An interactive guide to learn CSS Relative Colors.
  - [OKLCH in CSS: why we moved from RGB and HSL](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl)
- [How to have the browser pick a contrasting color in CSS](https://webkit.org/blog/16929/contrast-color/)
- [Animating zooming using CSS: transform order is important… sometimes](https://jakearchibald.com/2025/animating-zooming/)
- [Use Cases for Field Sizing](https://ishadeed.com/article/field-sizing/)

## Pseudo-class

- [Understanding the Difference Between : and :: in CSS](https://medium.com/@islizeqiang/understanding-the-difference-between-and-in-css-64c9d36c21af)
  > :: are used to create additional elements within an element
- [CSS Features We’re Thankful For and CSS Features We Need](https://www.lullabot.com/articles/css-features-were-thankful-and-css-features-we-need)
  - OK - :is(), :where(), grid
  - not yet - :has(), subgrid
- [Three important things you should know about CSS :is()](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/)
  - [The selector list of :is() is forgiving](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#forgiving): Invalid CSS selectors will simply be ignored.
  - [The specificity of :is() is that of its most specific argument](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#specificity)
  - [:is() does not work with pseudo-element selectors (for now)](https://www.bram.us/2021/03/19/three-important-things-you-should-know-about-css-is/#simple-selectors)
- [4 ways CSS :has() can make your HTML forms even better](https://austingil.com/css-has-with-html-forms/?utm_campaign=Frontend%2BWeekly&utm_medium=email&utm_source=Frontend_Weekly_337)
- [How to Kill the Cascade](https://robinrendle.com/the-cascade/017-how-to-kill-the-cascade/)
- [My Modern CSS Reset](https://jakelazaroff.com/words/my-modern-css-reset/)

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

### [Understanding SVG Paths](https://www.nan.fyi/svg-paths)

### [Have It All: External, Styleable, & Scalable SVG](https://scottjehl.com/posts/svgtopia/)

### [SVG triangle of compromise (resolved)](https://me.micahrl.com/blog/svg-triangle-of-compromise/)

Displaying an external SVG with the `<use>` tag

- stylable
- cacheable
- dimensional

### [Simulating Hand-Drawn Motion with SVG Filters](https://camillovisini.com/coding/simulating-hand-drawn-motion-with-svg-filters)

## Functions

### [CSS Image fragments - image()](https://12daysofweb.dev/2022/css-image/#image-fragments)

```css
.hero {
  background-image: image("images/my-image.jpg#xywh=150,50,500,300");
}
```

## Grid

- [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [How To Build A Magazine Layout With CSS Grid Areas](https://www.smashingmagazine.com/2023/02/build-magazine-layout-css-grid-areas/)
- [CSS Grid Areas](https://ishadeed.com/article/css-grid-area/)

## Styles

- [linear-gradient()](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/linear-gradient)
- [Web Design in 4 minutes](https://jgthms.com/web-design-in-4-minutes/)
- [The `hanging-punctuation` property in CSS](https://chriscoyier.net/2023/11/27/the-hanging-punctuation-property-in-css/)
- [Spicing up text with text-emphasis in CSS](https://www.amitmerchant.com/spicing-up-text-with-text-emphasis-in-css/)
  ```css
  .text-emphasis-dollar {
    text-emphasis: "$" lime;
    text-emphasis-position: under;
  }
  ```
- [What is safe alignment in CSS?](https://frontendmasters.com/blog/what-is-safe-alignment-in-css/)
  ```css
  .flex {
    display: flex;
    align-items: safe center;
  }
  ```
- [The power of CSS Variables 💪: A flexible solution for spacing utilities](https://dev.to/karsten_biedermann/the-power-of-css-variables-a-flexible-solution-for-spacing-utilities-4bch)

  ```html
  <div style="--space-top: 30px; --space-bottom: 100px;"></div>
  ```

  ```css
  @media (min-width: 992px) {
    [style*="--space-bottom"] {
      margin-bottom: var(--space-bottom);
    }
    [style*="--space-top"] {
      margin-top: var(--space-top);
    }
  }
  ```

- [CSS Button Styles You Might Not Know](https://dbushell.com/2024/03/10/css-button-styles-you-might-not-know/)
  > The manipulation value disables gestures like ‘double-tap to zoom’. Other gestures like ‘panning’ and ‘pinch to zoom’ are unaffected. An extra benefit is that the browser no longer needs to delay the click event waiting for a second tap.
  ```css
  .button,::file-selector-button {
    inline-size: fit-content;
    touch-action: manipulation;
    user-select: none;
  }
  *:focus-visible {
      outline: 2px solid magenta;
      outline-offset: 2px;
    }
  }
  ```
- [1fr 1fr vs auto auto vs 50% 50%](https://frontendmasters.com/blog/1fr-1fr-vs-auto-auto-vs-50-50/)

### [columns](https://developer.mozilla.org/en-US/docs/Web/CSS/columns)

- [The True Power Of CSS Columns](https://medium.com/codex/the-true-power-of-css-columns-2e620ad66282)
