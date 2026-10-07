
> https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/

## [Resizing images for big wins](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/#resizing-images-big-wins)

## [Compression lesson](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/#compression-lesson)

## [Formats for the win](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/#formats-win)

## [Load responsively](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/#load-responsively)

With the HTML [`<picture> element`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture), we can load the image in the right size and format, no matter the device. It ensures the best image-loading experience every time, taking into account a device’s DPR automatically.

```html
<picture>
  <source
    srcset="
      assets/cactus-300.avif   300w,
      assets/cactus-1100.avif 1100w,
      assets/cactus-1300.avif 1300w,
      assets/cactus-2100.avif 2100w
    "
    sizes="(max-width: 1300px) 100vw, 1300px"
    type="image/avif"
    height="747"
    width="1100"
  />
  <source
    srcset="
      assets/cactus-300.webp   300w,
      assets/cactus-1100.webp 1100w,
      assets/cactus-1300.webp 1300w,
      assets/cactus-2100.webp 2100w
    "
    sizes="(max-width: 1300px) 100vw, 1300px"
    type="image/webp"
    height="747"
    width="1100"
  />
  <img
    srcset="
      assets/cactus-300.jpg   300w,
      assets/cactus-1100.jpg 1100w,
      assets/cactus-1300.jpg 1300w,
      assets/cactus-2100.jpg 2100w
    "
    sizes="(max-width: 1300px) 100vw, 1300px"
    src="assets/cactus-1100.jpg"
    alt="Cactus image loaded responsively"
    height="747"
    width="1100"
  />
</picture>
```

## [Lazy loading for image optimization](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/#lazy-loading-image-optimization)
