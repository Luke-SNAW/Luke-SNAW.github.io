
> https://pepelsbey.dev/articles/conditionally-adaptive/

There’s a component structure behind every website or app these days, hundreds of small files. Though when it comes to delivering resources, we often serve just a single file for every resource type: styles, scripts, and even sprites for images. Everything gets squashed during the build process, including resources specific to certain resolutions or media conditions.

And resources aren’t equal! For example, CSS is a blocking resource, and there’s nothing for a browser to render until every last byte of every CSS file is loaded. Why? The last line of a CSS file could overwrite something that came just before that. That’s your “C” in the CSS, which stands for “cascade.”

## What if?

What if we’d take the CSS bundle we’ve just built out of dozens of files and split it back into multiple parts? But this time, based on conditions where these parts are applicable. For example, we could split it into four files:

- **Base:** universal styles with fonts and colors
- **Mobile:** styles only for narrow viewports
- **Tablet:** styles only for medium viewports
- **Desktop:** styles only for large viewports

```html
<link rel="stylesheet" href="base.css" />
<link rel="stylesheet" href="mobile.css" media="(max-width: 767px)" />
<link
  rel="stylesheet"
  href="tablet.css"
  media="(min-width: 768px) and (max-width: 1023px)"
/>
<link rel="stylesheet" href="desktop.css" media="(min-width: 1024px)" />
```

## Priorities

Another little detail in the Network panel made me realize what was going on: the Priority column. You might have to enable it by right-clicking the table heading and choosing it from the list of available columns.

---

It will also require you to write your CSS in a way that isolates styles for different viewports. That’s another idea for an article, by the way. The same goes for tooling: it’s not quite there yet. The closes thing I could find are [Media Query plugin for Webpack](https://github.com/SassNinja/media-query-plugin) and [Extract Media Query plugin for PostCSS](https://github.com/SassNinja/postcss-combine-media-query).

## Preferences

The list of [media features](https://developer.mozilla.org/en-US/docs/Web/CSS/@media#media_features) you can use in Media Queries extends beyond just viewport width and height. You can adapt your website to the user’s needs and preferences: color scheme, pixel density, reduced motion, etc. But not only that! With this new behavior in mind, we can make sure that only relevant styles are render-blocking.

### Color scheme

One of the most popular media features these days is `prefers-color-scheme`, which allows you to supply light and dark color schemes to match the user’s system preferences. In most cases, it’s used right in CSS as `@media`, but it can also be used to link relevant CSS files conditionally.

```html
<link rel="stylesheet" href="light.css" media="(prefers-color-scheme: light)" />
<link rel="stylesheet" href="dark.css" media="(prefers-color-scheme: dark)" />
```

And just like we’ve learned before, browsers will load _dark.css_ with the lowest priority in the case when the user prefers a light color scheme and vice versa. There’s a [good article by Thomas Steiner](https://web.dev/prefers-color-scheme/) diving deep into the dark mode, including a theme toggler that works with CSS files linked this way.

### Pixel density

Sometimes we have to deal not with [beautiful vector graphics](https://pepelsbey.dev/articles/svg-sprites/), but with raster images too. In this case, we often have different files for different pixel densities, for example, _icon.png_ and _icon@2x.png_.

```css
a {
  display: block;
  width: 24px;
  height: 24px;
  background-image: url("icon.png");
}
@media (min-resolution: 2dppx) {
  a {
    background-image: url("icon@2x.png");
    background-size: 24px 24px;
  }
}
```

These six lines of CSS specifically targeting high-density screens are usually bundled into the same file loaded for users with low-density screens. Fortunately, browsers are smart enough not to load high-density graphics. You guessed it, we can do it even better: split them into a separate file and load it with the lowest priority.

```html
<link rel="stylesheet" href="retina.css" media="(min-resolution: 2dppx)" />
```

This file will be loaded and applied immediately if the user decides to drag the browser window to a high-density screen. But it won’t block the initial rendering on a low-density screen.

### Reduced motion

Animations and smooth transitions could improve user experience, but for some people they can be a source of distraction or discomfort. The media feature `prefers-reduced-motion` allows you to wrap your heavy motion in `@media` to give users a choice. By the way, “reduce” doesn’t mean “disable”, it’s up to you to create a comfortable environment and not sacrifice clarity at the same time.

```html
<link
  rel="stylesheet"
  href="animation.css"
  media="(prefers-reduced-motion: no-preference)"
/>
```

Instead, you can put your motion-heavy styles into a separate file that will be loaded with the lowest priority when the user prefers reduced motion. The best way to achieve this would be to extract all the matching `@media` during the build process.
