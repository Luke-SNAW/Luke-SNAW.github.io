---
id: gl5r2b3p7y7s8z82c0g9fni
title: Visual tools
desc: ""
updated: 1675927344054
created: 1646264359213
---

## Collections

- [Responsive Image Breakpoints Generator](https://www.responsivebreakpoints.com/) - Easily generate the optimal responsive image dimensions
- [TypeIt](https://github.com/alexmacarthur/typeit) - The Most Versatile JavaScript Animated Typing Utility on the Planet
- [imaskjs](https://github.com/uNmAnNeR/imaskjs) - vanilla javascript input mask
- [deck.gl](https://github.com/visgl/deck.gl) - WebGL2 powered geospatial visualization layers
- [Golden Layout](https://github.com/golden-layout/golden-layout) - A multi window layout manager for webapps
- [color](https://github.com/Qix-/color) - Javascript color conversion and manipulation library
- [timeago.js](https://github.com/hustcc/timeago.js) - 🕗 ⌛ timeago.js is a tiny(2.0 kb) library used to format date with `*** time ago` statement.
- [Cheetah Grid](https://github.com/future-architect/cheetah-grid) - The fastest open-source data table for web.
- [Shepherd](https://github.com/shipshapecode/shepherd) - Guide your users through a tour of your app
- [Lexical](https://github.com/facebook/lexical) is an extensible text editor framework that provides excellent reliability, accessibility and performance.
- [DFlex](https://github.com/dflex-js/dflex) - A Drag-and-Drop library for all JavaScript frameworks implementing an enhanced transformation mechanism to manipulate DOM elements.
- [impress.js](https://github.com/impress/impress.js) is a presentation framework based on the power of CSS3 transforms and transitions in modern browsers and inspired by the idea behind prezi.com.
- [css-doodle](https://github.com/css-doodle/css-doodle) - A web component for drawing patterns with CSS.
- [WinBox](https://github.com/nextapps-de/winbox) is a modern HTML5 window manager for the web.
- [Tesseract.js](https://github.com/naptha/tesseract.js) - Pure Javascript OCR for more than 100 Languages 📖🎉🖥
- [PhotoSwipe](https://github.com/dimsemenov/photoswipe) — JavaScript image gallery and lightbox
- ✨ [Viselect](https://github.com/Simonwep/selection) - A high performance and lightweight library to add a visual way of selecting elements, just like on your Desktop.

## Canvas

- [Atrament](https://github.com/jakubfiala/atrament.js) - A small JS library for beautiful drawing and handwriting on the HTML Canvas.
- [img-comparison-slider](https://github.com/sneas/img-comparison-slider) - Image comparison slider. Compare images before and after. Supports React, Vue, Angular. - [https://img-comparison-slider.sneas.io/](https://img-comparison-slider.sneas.io/)
- [Viewer.js](https://github.com/fengyuanchen/viewerjs) - JavaScript image viewer.
- [html2canvas](https://github.com/niklasvh/html2canvas) - Screenshots with JavaScript
- [🍃 Leaflet](https://github.com/Leaflet/Leaflet) - JavaScript library for mobile-friendly interactive maps

## Scroll

- [LetMeScroll](https://github.com/BMSVieira/letmescroll.js)
- [Smooth Scrollbar](https://github.com/idiotWu/smooth-scrollbar) - Customizable, Pluginable, and High-Performance JavaScript-Based Scrollbar Solution.
- [ScrollMovie](https://github.com/nagatapote/scroll-movie) is the library that enables you to animate background image as you scroll the window.
- [pushIn.js](https://github.com/nateplusplus/pushin) is a lightweight parallax effect, built with JavaScript, that simulates an interactive dolly-in or push-in animation on a webpage.

## Animation

- [AutoAnimate](https://github.com/formkit/auto-animate) is a zero-config, drop-in animation utility that adds smooth transitions to your web app. You can use it with Vue, React, or any other JavaScript application.

### [Create Page Transitions in Next.js with Framer Motion](https://javascript.plainenglish.io/how-to-create-page-transitions-in-next-js-with-framer-motion-47642c462c62)

```javascript
import "../styles/globals.css"
import { motion } from "framer-motion"

function MyApp({ Component, pageProps, router }) {
  return (
    <motion.div
      key={router.route}
      initial="initial"
      animate="animate"
      variants={{
        initial: {
          opacity: 0,
        },
        animate: {
          opacity: 1,
        },
      }}
    >
      <Component {...pageProps} />
    </motion.div>
  )
}

export default MyApp
```

## Calendar

- [tui-calendar](https://github.com/nhn/tui.calendar) - 🍞📅 A JavaScript calendar that is full featured. Now your service just got the customizable calendar.

## graphic

- [TWGL: A Tiny WebGL helper Library](https://github.com/greggman/twgl.js)
- [Delivering 3D Scenes to the Web](https://rd.nytimes.com/projects/delivering-3d-scenes-to-the-web) - NY shares four demos that showcase the methods that it has found most useful for publishing photogrammetry to the web.
- [three.js postprocessing / pixel](https://threejs.org/examples/?q=pixel#webgl_postprocessing_pixel)
