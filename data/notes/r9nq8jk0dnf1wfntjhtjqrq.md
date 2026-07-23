
> https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs?ref=heydesigner

## The extremely short version

Instead of serving dozens of icons, all you need is just **five** icons and one JSON file.

For the browser using HTML:

```html
<link rel="icon" href="/favicon.ico" sizes="any" /><!-- 32×32 -->
<link rel="icon" href="/icon.svg" type="image/svg+xml" />
<link rel="apple-touch-icon" href="/apple-touch-icon.png" /><!-- 180×180 -->
<link rel="manifest" href="/manifest.webmanifest" />
```

And in your web app manifest:

```json
// manifest.webmanifest
{
  "icons": [
    { "src": "/icon-192.png", "type": "image/png", "sizes": "192x192" },
    { "src": "/icon-512.png", "type": "image/png", "sizes": "512x512" }
  ]
}
```

## The long version, where everything is explained

> ## Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.
>
> ---
>
> Antoine de Saint-Exupéry  
> — Airman's Odyssey

## The Ultimate Favicon Setup

Instead of creating many images with different sizes, I decided to rely on SVG and browser downscaling. If you’re concerned about performance, I’m here to set the record straight:

- Browsers download favicons in the background, so a bigger favicon image does not affect website performance.
- SVG is a great way to reduce image size for images that aren’t supposed to be bitmaps in the first place; for many _logos_ the resulting file will be much smaller than a PNG.
- With just three PNG images in this minimum set, you can use advanced tools to optimize their size. This solves a problem for Internet users that don’t have unlimited data plans.

Now I’ll reveal the minimal set of icons that I came up with during my research and practice. This list should work with all popular browsers and devices, both old and new.

#### I. favicon.ico for legacy browsers

ICO files actually have a [directory structure](<https://en.wikipedia.org/wiki/ICO_(file_format)#Icon_resource_structure>) and can pack files with different resolutions. I recommend sticking to a single 32×32 image, unless the one you have doesn’t downscale well to 16×16 (if it becomes blurry, for instance). In that case, you can ask your designer to come up with a special version of the logo that’s tailored to fit small pixel grids.

Don’t get smart with the folder static asset folder structure and cache busters. `https://example.com` website should have a favicon on `https://example.com/favicon.ico`. Some tools, like RSS readers, just request `/favicon.ico` from the server and don’t bother looking elsewhere.

We need `sizes="any"` for `<link>` to `.ico` file in order to fix the [Chrome bug](https://twitter.com/subzey/status/1417099064949235712) where it chooses an ICO file over an SVG.

#### II. A single SVG icon with a light/dark version for modern browsers

SVG is a vector format that describes curves instead of pixels. At large sizes, it’s more efficient than raster images. As of this writing, [72% of all browsers](https://caniuse.com/link-icon-svg) support SVG icons.

Your HTML page should have a `<link>` tag in its `<head>` with `rel="icon"`, `type="image/svg+xml"` and with the `href` containing a link to the SVG file as attributes.

SVG is an XML format and can contain a `<style>` tag to describes CSS. As with any CSS, it can contain media queries like `@media (prefers-color-scheme: dark)`. This will allow you to toggle the same icon between [light and dark system themes](https://web.dev/building-an-adaptive-favicon/).

#### III. 180×180 PNG image for Apple devices

The Apple touch icon is an image that Apple devices will use if you add the webpage as a shortcut to your home screen on an iPhone or iPad. Your HTML page should have `<link rel="apple-touch-icon" href="apple-touch-icon.png">` tag inside `<head>`.

Since iOS 8+, iPads have required an image with a 180×180 resolution. Other devices will downscale it, but if we provide the source with a high-enough quality, the downscaling won’t hurt the end-user (I’ll come back to this later).

Small note: an Apple touch icon will look better if you place `20px` padding around the icon and add some background color. You can use any image editor to do this.

#### IV. Web app manifest with 192×192 and 512×512 PNG icons for Android devices

- A web app manifest is a JSON file containing all the details for a browser to install your website as a system application. This format came about from Google via its [PWA](https://en.wikipedia.org/wiki/Progressive_web_application) initiative.
- Your HTML page should have a `<link rel="manifest" href="path.webmanifest">` tag with a link to the manifest file.
- The manifest should have an `icon` field that links to two icons: 192×192, for display on the home screen, and 512×512 which will be used as a splash screen as PWA is loading.

```json
{
  "icons": [
    { "src": "/icon-192.png", "type": "image/png", "sizes": "192x192" },
    { "src": "/icon-512.png", "type": "image/png", "sizes": "512x512" }
  ]
}
```

## Did we forget anyone?

There are, of course, more favicon flavors out there, some of them quite obscure, so let’s see how our setup fares with them. Maybe, it’s time to say farewell to some of the less successful formats out there.

#### Windows Tile Icon

Microsoft Edge used to [support](<https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/hh772707(v=vs.85)>) a special icon format to pin websites to the start menu. For recent versions of Windows, this is no longer required.

#### Safari Pinned Icon

Safari formerly had a requirement of SVG monochrome icon for [pinned tabs](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/pinnedTabs/pinnedTabs.html). However, since Safari 12, we can use a regular favicon for pinned tabs. Even [apple.com](https://www.apple.com/) doesn’t use the `mask-icon` anymore.

#### rel=“shortcut”

A lot of (now outdated) tutorials will include a `favicon.ico` into HTML like this:

```html
<link rel="shortcut icon" href="/favicon.ico" sizes="any" />
```

Be warned that `shortcut` is not, and never has been, a valid link relation. Read this [amazing article](https://mathiasbynens.be/notes/rel-shortcut-icon) by Mathias Bynens from ten years ago that explains why we never needed shortcuts and why `rel="icon"` is just fine.

#### Opera Coast

In the past, Opera Coast, an experimental browser for iOS, required a special 228×228 icon. This browser left the App Store in 2017, and I doubt it survived the multiple iOS updates since that time.

Now, as we wave good-bye to our fallen comrades, let’s see how to produce an ultimate favicon set for those who are still standing.

## How to build our Ultimate Favicon Set

Here’s how to build our ultimate, minimalistic favicon set in six quick steps. All you need to start is an SVG file for the logo that you want to use.

#### Step 1: Prepare the SVG

Be sure that the SVG image is _square_. Open the source file in your system viewer and check the image’s width and height. It’s easy to adjust the SVG size using any SVG editor. In [Inkscape](https://inkscape.org/), you can change document size by selecting File → Document Properties and then center the logo using Object → Align and Distribute.

Save your file as `icon.svg`. Now let’s fiddle with our SVG and make it play well with modern system _themes_. Ask your designer how the colors should be inverted for a dark theme (for B&W logos, you just change black to white).

Now, open your SVG file in a _text_ editor. Find a `<path>` with a dark or missing `fill`. Add a CSS media query that will trigger on theme changes and change `fill` to the colors you want:

```diff
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 500 500">
+   <style>
+     @media (prefers-color-scheme: dark) {
+     .a { fill: #f0f0f0 }
+     }
+   </style>
-   <path fill="#0f0f0f" d="…" />
+   <path class="a" fill="#0f0f0f" d="…" />
  </svg>
```

You may also use this media query technique with SVGs to [add wide-gamut P3 colors](https://evilmartians.com/chronicles/how-to-use-p3-colors-in-svg) to your favicons.

#### Step 2: Create an ICO file

Open your `icon.svg` file in a raster graphics editor. I recommend [GIMP](https://www.gimp.org/); it’s free and multi-platform.

Accept rendering SVG to raster. Set the width and height to be 32 pixels. Export file to `favicon.ico` using _32 bpp, 8-bit alpha, no palette_ settings.

If you do not have GIMP you can install [Inkscape](https://inkscape.org/) and [ImageMagick](https://www.imagemagick.org/script/download.php) and convert SVG to ICO in the terminal:

```shell
inkscape ./icon.svg --export-width=32 --export-filename="./tmp.png"
# In Windows call `magick convert ./tmp.png ./favicon.ico`
convert ./tmp.png ./favicon.ico
rm ./tmp.png
```

Scale the image down to 16×16 and check the icon visibility. If it has become too blurry, it would be better to ask your designer for a custom tiny version of the logo.

To include a separate 16×16 version of an icon:

1. Open `favicon.ico` with the 32×32 icon.
2. Create a new layer with a 16×16 size.
3. Put the 16×16 version of an icon into this layer.
4. Export the file. GIMP will save each layout as a separate version of the icon.

Or you can do the same in ImageMagick by:

```shell
convert ./icon-32.png ./icon-16.png ./favicon.ico
```

#### Step 3: Create PNG images

Open your source SVG file in a raster graphics editor again and create a 512×512 image. Export it as `icon-512.png`.  
Scale the image to 192×192 and export it to `icon-192.png`. Now scale the image itself to 140×140 and set the canvas to 180×180, and then export it as `apple-touch-icon.png`.

Or you can do the same in Inkscape:

```shell
inkscape ./icon.svg --export-width=512 --export-filename="./icon-512.png"
inkscape ./icon.svg --export-width=192 --export-filename="./icon-192.png"
```

#### Step 4: Optimize PNG and SVG files

The best tool for optimizing SVGs is [SVGO](https://github.com/svg/svgo). To use it, run:

```shell
npx svgo --multipass icon.svg
```

[Squoosh](https://squoosh.app/) is a great web app to optimize raster images:

1. Open your `icon-512.png` in Squoosh.
2. Change the Compress setting to `OxiPNG`.
3. Enable “Reduce palette”.
4. Set 64 colors.
5. Compare the before/after by moving the slider. If you see a difference, increase the number of colors.
6. Save the file.

Repeat these steps for `icon-192.png` and `apple-touch-icon.png`.

#### Step 5: Add the icons to HTML

You need to add links to `favicon.ico` and to `apple-touch-icon.png` into your HTML.

For static HTML:

```diff
  <title>My website</title>
+ <link rel="icon" href="/favicon.ico" sizes="any">
+ <link rel="icon" href="/icon.svg" type="image/svg+xml">
+ <link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

However, we recommend using a bundler to generate cache busters (include the file’s hash in the name as a fingerprint). If you are using Webpack with [`HtmlWebpackPlugin`](https://webpack.js.org/plugins/html-webpack-plugin/):

1. Create an `index.html` template.
2. Add the template to the plugin options:

   ```js
   new HtmlWebpackPlugin({ template: "./view/index.html" })
   ```

3. Define an HTML template with links (the examples use `HtmlWebpackPlugin` to include files, but it can be your templating language of choice):

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="utf-8" />
       <title>My website</title>
       <meta name="viewport" content="width=device-width,initial-scale=1" />
       <link rel="icon" href="/favicon.ico" sizes="any" />
       <link
         rel="icon"
         type="image/svg+xml"
         href="<%=
         require('./icon.svg').default
       %>"
       />
       <link
         rel="apple-touch-icon"
         href="<%=
         require('./apple-touch-icon.png').default
       %>"
       />
     </head>
     <body></body>
   </html>
   ```

4. Use [`copy-webpack-plugin`](https://www.npmjs.com/package/copy-webpack-plugin) to copy `favicon.ico` _without_ adding a hash to file name.

#### Bonus tip: create a separate icon for staging

Favicons are a nice way to distinguish your production environment from a staging one. I find that using an alternative icon for staging is super effective for avoiding any costly cases of confusion.

Create a `favicon-dev.ico` with the same logo, but invert the colors (or do something that makes sense to you). Do the same for SVG and create `icon-dev.svg`.

Now, replace the icons in your HTML template depending on the `process.env.NODE_ENV === 'production'` condition:

```diff

  <!doctype html>
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>My website</title>
      <meta name="viewport" content="width=device-width,initial-scale=1">
-     <link rel="icon" href="/favicon.ico" sizes="any">
+     <link rel="icon" sizes="any" href="<%=
+       process.env.NODE_ENV === 'production'
+         ? '/favicon.ico'
+         : require('./favicon-dev.ico').default
+     %>">
      <link rel="icon" type="image/svg+xml" href="<%=
-       require('./icon.svg').default
+       process.env.NODE_ENV === 'production'
+         ? require('./icon.svg').default
+         : require('./icon-dev.svg').default
      %>">
      <link rel="apple-touch-icon" href="<%=
        require('./apple-touch-icon.png').default
      %>">
    </head>
    <body></body>
  </html>
```

#### Step 6: Create a web app manifest

For static HTML, create a JSON file named `manifest.webmanifest`:

```json
{
  "name": "My website",
  "icons": [
    { "src": "/icon-192.png", "type": "image/png", "sizes": "192x192" },
    { "src": "/icon-512.png", "type": "image/png", "sizes": "512x512" }
  ]
}
```

Link it in your HTML:

```diff
  <title>My website</title>
+ <link rel="manifest" href="/manifest.webmanifest">
  <link rel="icon" href="/favicon.ico" sizes="any">
  <link rel="icon" href="/icon.svg" type="image/svg+xml">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

With Webpack, you can use [webpack-pwa-manifest](https://www.npmjs.com/package/webpack-pwa-manifest) plugin:

```js
  plugins: [
    …,
    new WebpackPwaManifest({
      name: 'My website',
      icons: [
        { src: resolve('./icon-192.png'), sizes: '192x192' },
        { src: resolve('./icon-512.png'), sizes: '512x512 }
      ]
    })
  ]
```

Thank you for reading! As you can see, with modern web standards, the task of creating our Ultimate Favicon Set becomes quite straightforward. And even though following the steps manually shouldn’t take much of your time, having an automated tool to do the same will make things even more amazing! Feel free to ping me on [Twitter](https://twitter.com/sitnikcode) if you’re willing to build one; I’ll be more than happy to help!
