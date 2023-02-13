---
id: iiz9j2u1ecu76gmi3e7b33r
title: Optimal Images in HTML
desc: ""
updated: 1676254701936
created: 1676254471528
---

> https://www.builder.io/blog/fast-images

So you've got your nice page and you're adding your background image and…

```css
.hero {
  /* 🚩 */
  background-image: url("/image.png");
}
```

WAIT!

Did you know that this is going to be very unoptimized for performance? And in more ways than one.

## Why you should (generally) avoid `background-image` in CSS

### Optimal image sizing

Outside of using SVGs, there's virtually no case where every visitor to your site should receive the exact same image file, given the vast amount of screen sizes and resolutions individuals have these days.

_Does your site even work on watches yet?_ (Kidding…I think)

You could say, "oh! Media queries, I’ll manually specify a range of sizes of screen sizes and images":

```css
/* 🚩 */
.hero {
  background-image: url("/image.png");
}
@media only screen and (min-width: 768px) {
  .hero {
    background-image: url("/image-768.png");
  }
}
@media only screen and (min-width: 1268px) {
  .hero {
    background-image: url("/image-1268.png");
  }
}
```

Well, there is a problem with this. Besides being quite tedious and verbose, this is only taking screen _size_ into account, but not _resolution_.

So you could say, "aha! I know a cool trick for this, `[image-set](https://developer.mozilla.org/en-US/docs/Web/CSS/image/image-set)` to specify different image sizes for different resolutions":

```css
/* 🚩 */
.hero {
  background-image: image-set(url("/image-1x.png") 1x, url("/image-2x.png") 2x);
}
```

And you’d be right, this has some benefits. But, generally speaking, we need to take into account _both_ screen size and resolution.

So we could write some bloated CSS that combined media queries and image-set, but this is just getting complex, and it means we need to know exactly how large our image is for each screen, even as the site layout evolves over time.

And still, this doesn’t support critical things like lazy loading, next-gen formats for supported browsers, priority hints, async decoding, and more.

And to top things off, we also have an issue with chained requests.

### Avoiding chained requests

- X Fetch HTML -> Fetch CSS -> Fetch Image
- O Fetch HTML -> Fetch Image

With an image tag, you have the link to the `src` right in the HTML. So the browser can fetch the initial HTML, scan for images, and begin fetching high-priority images immediately.

In the case of loading images in CSS, assuming you use external stylesheets (`link rel=”styleshset”`, like most do, instead of inline `style` everywhere) the browser must scan your HTML, fetch the CSS, and then find that a `background-image` is applied to an element, and only after all of that can go fetch that image. This will take longer.

And yes, you can work around some things, like inlining CSS, [preloading](https://web.dev/optimize-lcp/#optimize-when-the-resource-is-discovered) images, and pre-connecting to origins. But, as you read on, you will see additional advantages you get with the HTML `img` tag that you sadly don’t get with `background-image` in CSS.

### When to consider a background image

Before we move on to discuss the most optimal way of loading images, we have to remember that like all rules, there are exceptions. For instance, if you have a very small image you want to tile with `background-repeat` , there isn’t an easy way to accomplish repeating (that I know of) with `img` tags.

But for any image that is larger than, say, 50px, I would highly suggest avoiding setting it in CSS and instead using an `img` tag for virtually everything.

## Optimally loading images

Now that we’ve complained about the challenges of using `background-image` in CSS, let’s talk actual solutions.

In modern HTML, the `img` tag gives us a number of useful attributes to optimally load images. Let’s run through them.

### Browser-native lazy loading

The first amazing attribute we get on an `img` tag to improve our image performance is [`loading=lazy`](https://web.dev/browser-level-image-lazy-loading/#the-loading-attribute):

```html
<!-- 😍 -->
<img loading="lazy" ... />
```

This is already a huge improvement, as now your visitors won’t automatically download images that are not even in the viewport. And even better — this has great performance, it’s fully natively implemented by browsers, requires no JS, and is [supported by all modern browsers](https://caniuse.com/loading-lazy-attr)

> **Note** one important detail — ideally, do not lazy load images “[above the fold](https://en.wikipedia.org/wiki/Above_the_fold)” (that is, images that will be in the browser’s viewport immediately on first load). That will help ensure your most critical images load as soon as possible, and all others will load only as needed.

P.S.: `loading=lazy` [also works on](https://web.dev/iframe-lazy-loading/) `[iframes](https://web.dev/iframe-lazy-loading/)` 😍

### Optimal sizing for all screen sizes _and_ resolutions

Using `srcset` with your images is critical. Unless you are loading an SVG, you need to make sure that different screen sizes and resolutions get an optimally sized image:

```html
<img
  srcset="
    /image.png?width=100 100w,
    /image.png?width=200 200w,
    /image.png?width=400 400w,
    /image.png?width=800 800w
  "
  ...
/>
```

One important thing to note is that this is a more powerful version than you get with `image-set` in CSS, because you can use the `[w](https://html.spec.whatwg.org/multipage/images.html#introduction-3:viewport-based-selection-2)` [unit](https://html.spec.whatwg.org/multipage/images.html#introduction-3:viewport-based-selection-2) in an `img` `srcset`.

What is useful about it is that it takes _both_ size and resolution into account. So, if the image is currently displaying 200px wide, on a 2x pixel density device, with the above `srcset` the browser will know to grab the `400w` image (that is, the image that is `400px` wide, so it displays perfectly at 2x pixel density). Similarly, the same image on a 1x pixel density image will grab the `200w` image.

### Modern formats with the `picture` tag

You may have noticed we’re using a `.png` in our examples here. This is supported by any browser, but is almost never the most optimal image format.

This is where adding the `picture` around our `img` can allow us to specify more modern and optimal formats, such as [webp](https://developers.google.com/speed/webp), and supported browsers will favor those, via the `source` tag:

```html
<picture>
  <source
    type="image/webp"
    srcset="
      /image.webp?width=100 100w,
      /image.webp?width=200 200w,
      /image.webp?width=400 400w,
      /image.webp?width=800 800w
    "
  />
  <img ... />
</picture>
```

Optionally, you can support additional formats as well, such as [AVIF](https://en.wikipedia.org/wiki/AVIF):

```html
<picture>
  <source
    type="image/avif"
    srcset="
      /image.avif?width=100 100w,
      /image.avif?width=200 200w,
      /image.avif?width=400 400w,
      /image.avif?width=800 800w,
      ...
    "
  />
  <source
    type="image/webp"
    srcset="
      /image.webp?width=100 100w,
      /image.webp?width=200 200w,
      /image.webp?width=400 400w,
      /image.webp?width=800 800w,
      ...
    "
  />
  <img ... />
</picture>
```

### Don’t forget the `aspect-ratio`

It’s important to keep in mind that we also want to avoid [layout shifts](https://web.dev/cls/). This happens when an image loads if you don’t specify a precise size for the image ahead of the image downloading. There are two ways you can accomplish this.

The first is to specify a `width` and `height` attribute for your image. And optionally, but often a good idea, set the images `height` to `auto` in CSS so that the image is properly responsive as the screen size changes:

```html
<img width="500" height="300" style="height: auto" ... />
```

Alternatively, you can also just use the newer [`aspect-ratio`](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio) property in CSS to always have the right aspect ratio automatically. With this option, you don’t need to know the exact width and height of your image, just its aspect ratio:

```html
<img style="aspect-ratio: 5 / 3; width: 100%" ... />
```

`aspect-ratio` also pairs great with `[object-fit](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)` and `[object-position](https://developer.mozilla.org/en-US/docs/Web/CSS/object-position)`, which are quite similar to `[background-size](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size)` and `[background-position](https://developer.mozilla.org/en-US/docs/Web/CSS/object-position)` for background images, respectively.

```css
.my-image {
  aspect-ratio: 5 / 3;
  width: 100%;
  /* Fill the available space, even if the 
     image has a different intrinsic aspect ratio */
  object-fit: cover;
}
```

### Async image decoding

Additionally, you can specify `decoding="async"` to images to allow the browser to move the image decoding off of the main thread. MDN recommends to [use this for off-screen images](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/decoding#usage_notes).

```html
<img decoding="async" ... />
```

### Resource hints

One last, and more advanced option, is `[fetchpriority](https://web.dev/priority-hints/)`. This can be helpful to hint to the browser if an image is extra high priority, such as your [LCP image](https://web.dev/optimize-lcp/).

```html
<img fetchpriority="high" ... />
```

Or, to lower the priority of images, such as if you have images that are above the fold but not of high importance, such as on other pages of a carousel:

```html
<div class="carousel">
  <img class="slide-1" fetchpriority="high" />
  <img class="slide-2" fetchpriority="low" />
  <img class="slide-3" fetchpriority="low" />
</div>
```

### Add your `alt` text, kids

Yes, `alt` text is critical for accessibility and SEO, and is not to be overlooked:

```html
<img alt="Builder.io drag and drop interface" ... />
```

Or, for images that are _purely_ presentational (like abstract shapes, colors, or gradients), you can explicitly mark them as presentation only with the `role` attribute:

```html
<img role="presentation" ... />
```

### Understanding the `sizes` attribute

One important caveat to `srcset` attribute mentioned above is that browsers need to know the size an image will render at in order to pick the best sized image to fetch.

Meaning, once the image has rendered, the browser knows its actual display size, multiples that by the pixel density, and fetches the closest possible image in size in the srcset.

But for your _initial_ page load, browsers like chrome have a preload scanner that looks for img tags in the HTML to begin prefetching them immediately.

The thing is - this happens even before the page has rendered. For instance, our CSS hasn't even been fetched yet, so we have no indication as to how the image will display and at what size. As a result, the browser has to make some assumptions.

By default the browser will assume all images are `100vw` - aka the full page width. That's anywhere from a little to a _whole lot_ larger than they actually are. So that is far from optimal.

This is where the sizes attribute comes in handy:

```html
<img
  srcset="..."
  sizes="(max-width: 400px) 200px, (max-width: 800px) 100vw, 50vw"
  ...
/>
```

With this attribute, we can tell the browser at various window sizes, how large to expect our image to be (either exactly, with an exact pixel value like `500px`, or relative to the window, such as `50vw` to say it should display around 50% of the window width).

So in the example above, a `900px` wide screen will not match either of the first two caluses, and instead match the fallback clause that specifies for larger screens assume the image will display at `50vw`.

So since `50vw * 900px = 450px` the browser will aim for a `450px` wide image for a `1x` pixel density display, a `900px` wide image for `2x` pixel density, etc. It will then look for the closest match in the `srcset` and use that as the image to prefetch.

## Let’s recap

Wow, ok, that was a lot. Let’s put it all together.

Here is a great example of a very optimized image for loading:

```html
<picture>
  <source
    type="image/avif"
    srcset="
      /image.avif?width=100 100w,
      /image.avif?width=200 200w,
      /image.avif?width=400 400w,
      /image.avif?width=800 800w
    "
  />
  <source
    type="image/webp"
    srcset="
      /image.webp?width=100 100w,
      /image.webp?width=200 200w,
      /image.webp?width=400 400w,
      /image.webp?width=800 800w
    "
  />
  <img
    src="/image.png"
    srcset="
      /image.png?width=100 100w,
      /image.png?width=200 200w,
      /image.png?width=400 400w,
      /image.png?width=800 800w
    "
    sizes="(max-width: 800px) 100vw, 50vw"
    style="width: 100%; aspect-ratio: 16/9"
    loading="lazy"
    decoding="async"
    alt="Builder.io drag and drop interface"
  />
</picture>
```

#### **For high priority images:**

The above image is a good default, and best for images that may be below the fold.

For your highest priority images, you should remove `loading="lazy"` and `decoding="async"` and consider adding `fetchpriority="high"` if this is your absolute highest priority image, like your LCP image:

```diff
      style="width: 100%; aspect-ratio: 16/9"
-     loading="lazy"
-     decoding="async"
+     fetchpriority="high"
      alt="Builder.io drag and drop interface"
```

#### **For vectors (like SVGs):**

Also, for vector formats such as SVG, we don't need to provide multiple sizes and formats, and can just include the below:

```html
<!-- for SVG -->
<img
  src="/image.svg"
  style="width: 100%; aspect-ratio: 16/9"
  loading="lazy"
  decoding="async"
  alt="Builder.io drag and drop interface"
/>
```

Note that we completely removed the `<picture>` and `<source>` tags, as well as removed the `srcset` and `sizes` attributes, as they are no longer needed.

For high priority SVGs, the same rules mentioned above apply (remove `loading` and `decoding`, and optionally add `fetchpriority="high"` for your LCP image)

### Using an image for a background

Oh yeah, I almost forgot that we started this article by talking about our _original_ use case — a background image.

Now while the image optimization discussed here applies to any type of image you may want to use (such as background, foreground, and so on), it only takes a little bit of CSS (namely some absolute positioning and the object-fit property) to make an `img` behave like a `background-image`.

Here is a pared down example you can [try yourself](https://jsfiddle.net/gt9ahezx/2/):

```html
<div class="container">
  <picture class="bg-image">
    <source type="image/webp" ... />
    <img ... />
  </picture>
  <h1>I am on top of the image</h1>
</div>
<style>
  .container {
    position: relative;
  }
  h1 {
    position: relative;
  }
  .bg-image {
    position: absolute;
    inset: 0;
  }
  .bg-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
</style>
```

## Is using this much additional HTML bad for performance?

Yes and no, but mostly no.

It’s easy to forget just _how_ large images are (in terms of bytes). Adding a few bytes to your HTML can save you thousands, or even millions, of bytes on those images by loading much more optimized versions.

Second, let’s not forget that gzipping is a thing. The additional markup you will add for each image quickly becomes very redundant, which is perfectly suited for gzip to [deflate](https://en.wikipedia.org/wiki/Deflate) away.

So while DOM bloat and payload size definitely should always be a concern, I would suggest that the tradeoffs are in your favor on this one.

## An easier way

These days, you almost never need write all of that stuff by hand. Frameworks like [NextJS](https://nextjs.org/) and [Qwik](https://qwik.builder.io/), as well as platforms like [Cloudinary](https://cloudinary.com/) and [Builder.io](https://www.builder.io/), provide image components that make this straightforward, and look instead like the below:

```jsx
<!-- 😍 -->
<Image
  src="/image.png"
  alt="Builder.io drag and drop interface" />
```

And with that, you can get most, if not all, of the above optimizations (including generating all of those different image sizes and formats), automatically.

Note that that in most cases you still need to specify when an image is high priority, like so:

```jsx
<!-- High priority image -->
<Image
  priority
  src="/image.png"
  alt="Builder.io drag and drop interface" />
```

And in most cases if you want to use the `sizes` attribute you'll need to specify that manually too. Most of these components allow you to pass through options like that directly, like so:

```jsx
<!-- Manually speify sizes -->
<Image
  sizes="(max-width: 500px) 200px, 50vw"
  src="/image.png"
  alt="Builder.io drag and drop interface" />
```

The only Image component that I know that can automate setting the `sizes` attribute is the one that I made for [Builder.io](https://www.builder.io/), as we run a puppeteer script in the background to analyze the actual displayed layout of the image at various screen sizes and can generate that accordingly.

## Conclusion

Use `img` in HTML over CSS `background-image` whenever you can. Use lazy loading, `srcset`, `picture` tags, and the other optimizations we discussed above to deliver images in the most optimal way. Be aware of high-priority as compared to low-priority images and tweak your attributes accordingly.

Or, just use a good framework (like [NextJS](https://nextjs.org/) or [Qwik](https://qwik.builder.io/)) and/or good platforms (like [Cloudinary](https://cloudinary.com/) or [Builder.io](https://www.builder.io/)) and you’ll be covered, the easy way.

## About me

Hi! I'm [Steve](https://twitter.com/Steve8708?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor), CEO of [Builder.io](https://www.builder.io/).

I built our `Image` component and image optimization API, and have spent an absurd amount of time performance profiling them across hundreds of real world sites and apps.

Our platform is a way to drag + drop with your components to create pages and other CMS content on your existing site or app, [visually](https://www.builder.io/blog/headless-cms-workflow).

It’s all API driven and has integrations for all modern frameworks. You may find it interesting or useful:
