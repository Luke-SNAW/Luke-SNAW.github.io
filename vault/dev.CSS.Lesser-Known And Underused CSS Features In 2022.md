---
id: tagcstfxysvupps57sara53
title: Lesser-Known And Underused CSS Features In 2022
desc: ""
updated: 1655627394388
created: 1655626568565
---

https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/

After reading Louis Lazaris’ insightful article “[Those HTML Attributes You Never Use](https://www.smashingmagazine.com/2022/03/html-attributes-you-never-use/)”, I’ve asked myself ([and the community](https://twitter.com/AdrianBeceDev/status/1511312060780630019)) which properties and selectors are lesser-known or should be used more often.

## `all` Property [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#all-property)

This is a shorthand property which is often used for [resetting all properties](https://developer.mozilla.org/en-US/docs/Web/CSS/all) to their respective initial value by effectively stopping inheritance, or to enforce inheritance for all properties.

- `initial`  
   Sets all properties to their respective initial values.
- `inherit`  
   Sets all properties to their inherited values.
- `unset`  
   Changes all values to their respective default value which is either `inherit` or `initial`.
- `revert`  
   Resulting values depend on the stylesheet origin where this property is located.
- `revert-layer`  
   Resulting values will match a previous cascade layer or the next matching rule.

## `currentColor` [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#currentcolor)

Often referred to as “the first CSS variable”, `currentColor` is a value equal to the element’s `color` property. It can be used to [assign a value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value#currentcolor_keyword) equal to the value of the `color` property to any CSS property which accepts a color value. It forces a CSS property to inherit the value of the `color` property.

This value can be very useful to avoid assigning the same value to multiple CSS properties which accept color like `border-color`, `background`, `box-shadow`, etc. within the same selector.

## Custom Property Fallback Value [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#custom-property-fallback-value)

Custom properties brought significant improvements to CSS by allowing developers to create reusable values in their stylesheet without the need for CSS preprocessor like SASS. Custom properties were instantly adopted and are widely used today to great effect, especially in theming and interaction with JavaScript.

However, I feel like the [fallback value](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties#custom_property_fallback_values) was somewhat ignored. If you are unfamiliar with the fallback value, it’s the second value that can be assigned to `var` function which is applied if the first value is not set.

```css
color: var(--color-icon, #9eeb34);
```

We can also set another variable as a fallback.

```css
color: var(--color-icon-primary, var(--color-icon-default));
```

## Counters [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#counters)

CSS allows developers to define [named counters](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Counter_Styles/Using_CSS_counters) that can be incremented, decremented, and displayed using CSS `content` property.

- `counter-reset`  
   This property is used for initializing single or multiple counters. A default starting value can also be assigned.
- `reversed`  
   Function used when defining a counter with `counter-reset` to make the counter count down instead of up.
- `counter-increment`  
   Specify a counter to increment (or decrements if counter is defined as `reversed` or if a negative value is passed to `counter-increment`). Default increment value is 1, but a custom value value can also be passed to this property.
- `counter`  
   Used for accessing counter value. Usually used in `content` property.

## Interaction Media Queries [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#interaction-media-queries)

Cristian Díaz covered this topic in [his recent article](https://www.smashingmagazine.com/2022/03/guide-hover-pointer-media-queries/). When creating responsive websites, we often make assumptions about input mechanisms based on their screen size. We assume that the screen size of `1920px` belongs to a desktop computer or laptop and the user is interacting with the website using a mouse and keyboard, but what about laptops with touchscreen or smart TV screens?

This is where Interaction Media Features come in and allow us to fine-tune the usability of our components that users can interact with (inputs, offcanvas menus, dropdowns, modals, etc.) depending on the primary input mechanism — touch, stylus, mouse pointer, etc.

```css
@media (pointer: fine) {
  /* using a mouse or stylus */
}
@media (pointer: coarse) {
  /* using touch */
}
@media (hover: hover) {
  /* can be hovered */
}
@media (hover: none) {
  /* can't be hovered */
}
```

## `aspect-ratio` for Sizing Control [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#aspect-ratio-for-sizing-control)

When `aspect-ratio` was initially released, I thought I won’t use it outside image and video elements and in very narrow use-cases. I was surprised to find myself using it in a similar way I would use `currentColor` — to avoid unnecessarily setting multiple properties with the same value.

## Better Gradients [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#better-gradients)

We’ve been using gradients on the Web for a while, and they’ve become a staple in design. However, as [Josh W. Comeau points out](https://www.joshwcomeau.com/css/make-beautiful-gradients/), the middle part of the gradient can sometimes look gray and washed out, depending on the colors you are using.

In the following example, we are setting two gradients between the same two values (green and red). Notice in the first example how the colors in the middle part look muddy and washed out, because the browser is using RGB color interpolation by default. We cannot change that at the moment, but we might in the future with new CSS features. However, we can fix that by adding some midpoints to the gradient.

The second example uses an interpolation technique with multiple midpoints, which is generated using Josh W. Comeau’s [Gradient generator](https://www.joshwcomeau.com/gradient-generator/) tool. Notice how the middle part is now darker yellow and orange, and it looks much more vibrant and beautiful than in the first example.

## `:where` and `:is` Pseudo-selectors [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#where-and-is-pseudo-selectors)

These two pseudo-selectors gained wider browser support last year, and although there was much talk around them, I haven’t seen all those many uses around the Web. Stephanie Eckles has talked in-depth about these two pseudo-selectors in [her article](https://www.smashingmagazine.com/2021/04/guide-supported-modern-css-pseudo-class-selectors/#is).

## `scroll-padding` [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#scroll-padding)

One of my pet-peeves, when implementing a fixed page header, used to be how the on-page scroll links cause fixed page header to cover part of the content. We had to use JavaScript to fix this issue and implement custom scroll logic to take into account the fixed header offset. And things would only become more complicated if the header height changed on breakpoints, so we needed to cover those cases with JavaScript, too.

Luckily, we don’t have to rely on JavaScript for that anymore. We can specify `scroll-padding-top` and change its value using standard CSS media queries.

```css
html {
  scroll-padding-top: 6rem;
  scroll-behavior: smooth;
}
```

## Font Rendering Options [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#font-rendering-options)

I’ve recently worked on animating numeric values on a project where a value would increment from zero to a final value. I’ve noticed that the text kept jumping left and right during the animation due to individual characters having different widths.

[![Numeric values in Fira Sans font](https://res.cloudinary.com/indysigner/image/fetch/f_auto,q_80/w_400/https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643992dc-a2da-4f97-b6dd-cef517ea085e/2-lesser-known-underused-css-features-2022.png)](https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643992dc-a2da-4f97-b6dd-cef517ea085e/2-lesser-known-underused-css-features-2022.png)

Notice how Fira Sans font has different character widths for numeric values. (Second row has one extra character) ([Large preview](https://cloud.netlifyusercontent.com/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/643992dc-a2da-4f97-b6dd-cef517ea085e/2-lesser-known-underused-css-features-2022.png))

I assumed that this issue cannot be fixed, and I moved on. One of the tweets from the community poll suggested that I should look into `font-variant-numeric: tabular-nums`, and I was surprised to find a plethora of options that affect font rendering.

For example, `tabular-nums` fixed the aforementioned issue by setting the equal width for all numeric characters.

See the Pen [font-variant-numeric](https://codepen.io/smashingmag/pen/ZErpayJ) by [Adrian Bece](https://codepen.io/AdrianBece).

Please note that **available features depend on the font itself, and some features might not be supported.** For a complete list of options, consult the [documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric). There is also a `font-variant` [CSS property](https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant) that allows us to activate even more features for all characters, not just the numeric.

Here are a few more examples of `font-variant-numeric` that are available in the font Source Sans 3.

## Creating Stacking Context with `isolate` [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#creating-stacking-context-with-isolate)

This property may be confusing to developers, and I wasn’t aware of it until I read [Josh W. Comeau’s awesome article](https://www.joshwcomeau.com/css/stacking-contexts/#airtight-abstractions-with-isolation) on the topic of `z-index` and stacking contexts. In short, it allows us to compartmentalize our `z-index` stacks.

You probably ran into a case where you, for example, added a reusable tooltip component to your page, only to find out that the tooltip element has a `z-index` lower than some other adjacent element on the page, causing the tooltip to display below it. We would usually solve it by increasing the `z-index` value of the tooltip, but that could potentially cause regressions and similar issues somewhere else in the projects.

We could mess around with `z-index` values for title component and tooltip component or assign a `z-index` to their respective parent elements with `position: relative` to create a new stacking context, but we are relying on magic numbers!

Let’s think about the issue differently — what if we could create a new stacking context without relying on `z-index` magic numbers? This is exactly what `isolation: isolate` does! It creates a new stacking context or a group. It tells the browser not to mix these two stacking groups, not even if we increase title `z-index` value to highest possible value. So, we can keep the `z-index` values low and not worry if value should be 2, 10, 50, 100, 999999, etc.

## Render Performance Optimization [#](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#render-performance-optimization)

When it comes to rendering performance, it’s very rare to run into these issues when working on regular projects. However, in the case of large DOM trees with several thousands of elements or other similar edge cases, we can run into some performance issues related to CSS and rendering. Luckily, we have a direct way of dealing with these performance issues that cause lag, unresponsiveness to user inputs, low FPS, etc.

This is where `contain` property comes in. It tells the browser what won’t change in the render cycle, so the browser can safely skip it. This can have consequences on the layout and style, so make sure to test if this property doesn’t introduce any visual bugs.

```css
.container {
  /* child elements won't display outside of this container so only the contents of this container should be rendered*/
  contain: paint;
{
```
