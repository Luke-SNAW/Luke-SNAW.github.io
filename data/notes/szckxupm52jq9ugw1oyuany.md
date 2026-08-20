
> https://www.smashingmagazine.com/2022/03/new-css-features-2022/

2022 is shaping up to be a pretty great year for CSS, with a plethora of new features on the horizon. Some are already starting to land in browsers, others are likely to gain widespread browser support in 2022, while for one or two the process may be a little longer. In this article we’ll take a look at a few of them.

---

## Container Queries

Container queries enable us to style an element depending on the size of its parent — a crucial difference from media queries, which only query the viewport.

## :has()

Often known as the “parent selector”, this pseudo-class enables us to select an element depending on its descendants.

## @when/@else

```css
@when media(min-width: 30em) and supports(display: subgrid) {
  /* Styles for viewports over 30em, where the browser also supports subgrid */
} @else {
  /* Styles for browsers that do not meet the condition */
}
```

## accent-color

## New CSS Color Functions

- hwb(): Hue, Whiteness, Blackness.
- lab(): Lightness, along with a and b values, which determine the hue.
- lch(): Lightness, Chroma, Hue.
- color-mix(): Mix two colors together.
- color-contrast(): From a list of colors, output the one with the highest contrast compared to the first argument.
- color(): Specify a color in a different color space (e.g.display-p3).

## Cascade Layers

## Subgrid

## Scroll Timeline

You’ve probably seen a lot of cool websites that implement fancy scroll-linked animations. There are plenty of JS libraries to help us implement this kind of thing — I’m a big fan of [Greensock]’s ScrollTrigger plugin. Imagine if we could do all of that within CSS? With `@scroll-timeline` we can!

## Nesting
