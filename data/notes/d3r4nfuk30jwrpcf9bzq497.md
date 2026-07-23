
https://gomakethings.com/better-font-loading-with-the-font-displayswap-property/

# The font-display: swap property

```css
@font-face {
  font-display: swap;
  font-family: "PT Sans";
  font-style: normal;
  font-weight: 400;
  src: local("PT Sans"), local("PTSerif-Regular"),
    url("path/to/my/fonts/pt-sans-regular.woff2") format("woff2"), url("path/to/my/fonts/pt-sans-regular.woff")
      format("woff");
}
```

There are two main phases or periods in a font’s loading process:

1. Block Phase. If the font isn’t loaded yet, show invisible text.
2. Swap Phase. If the font isn’t loaded yet, use a fallback font until it’s ready.

The font-display property tells the browser what to do with a particular font file and how to display it. It has five values:

- auto - The browser uses the default behavior.
- block - Short block phase, infinite swap phase.
- swap - Extremely small block phase, infinite swap phase.
- fallback - Extremely small block phase, short swap phase.
- optional - Extremely small block phase, no swap phase.

A value of `auto` is the same as omitting the font-display property altogether.

The `block` and `swap` values will show a fallback font until custom typeface is ready. Of the two, swap is preferable, because it results in a shorter FOIT period.

With a value of `fallback`, if the font takes too long to load, it may never get displayed as the browser will just keep using the fallback font. And a value of optional only shows the custom font if its available right away.

# How to use this with your fonts

https://gomakethings.com/better-font-loading-with-the-font-displayswap-property/#how-to-use-this-with-your-fonts

# What if you use a CDN that doesn’t support font-display: swap?

Not all CDNs support the `font-display: swap` property.

If that’s the case for you, [the fonts.loaded() method](https://gomakethings.com/preventing-foit-with-web-fonts-using-the-vanilla-js-fonts.load-method/) is still a fantastic option that will create a better experience for your users.
