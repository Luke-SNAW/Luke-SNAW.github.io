---
id: gl5r2b3p7y7s8z82c0g9fni
title: Visual
desc: ""
updated: 1654401255397
created: 1646264359213
---

- [TypeIt](https://github.com/alexmacarthur/typeit) - The Most Versatile JavaScript Animated Typing Utility on the Planet
- [imaskjs](https://github.com/uNmAnNeR/imaskjs) - vanilla javascript input mask
- [deck.gl](https://github.com/visgl/deck.gl) - WebGL2 powered geospatial visualization layers
- [Golden Layout](https://github.com/golden-layout/golden-layout) - A multi window layout manager for webapps
- [color](https://github.com/Qix-/color) - Javascript color conversion and manipulation library
- [timeago.js](https://github.com/hustcc/timeago.js) - 🕗 ⌛ timeago.js is a tiny(2.0 kb) library used to format date with `*** time ago` statement.
- [Cheetah Grid](https://github.com/future-architect/cheetah-grid) - The fastest open-source data table for web.
- [Delivering 3D Scenes to the Web](https://rd.nytimes.com/projects/delivering-3d-scenes-to-the-web) - NY shares four demos that showcase the methods that it has found most useful for publishing photogrammetry to the web.
- [Shepherd](https://github.com/shipshapecode/shepherd) - Guide your users through a tour of your app
- [Lexical](https://github.com/facebook/lexical) is an extensible text editor framework that provides excellent reliability, accessibility and performance.
- [DFlex](https://github.com/dflex-js/dflex) - A Drag-and-Drop library for all JavaScript frameworks implementing an enhanced transformation mechanism to manipulate DOM elements.

# Canvas

- [Atrament](https://github.com/jakubfiala/atrament.js) - A small JS library for beautiful drawing and handwriting on the HTML Canvas.
- [img-comparison-slider](https://github.com/sneas/img-comparison-slider) - Image comparison slider. Compare images before and after. Supports React, Vue, Angular. - [https://img-comparison-slider.sneas.io/](https://img-comparison-slider.sneas.io/)
- [Viewer.js](https://github.com/fengyuanchen/viewerjs) - JavaScript image viewer.
- [html2canvas](https://github.com/niklasvh/html2canvas) - Screenshots with JavaScript
- [🍃 Leaflet](https://github.com/Leaflet/Leaflet) - JavaScript library for mobile-friendly interactive maps

# Scroll

- [LetMeScroll](https://github.com/BMSVieira/letmescroll.js)
- [Smooth Scrollbar](https://github.com/idiotWu/smooth-scrollbar) - Customizable, Pluginable, and High-Performance JavaScript-Based Scrollbar Solution.
- [ScrollMovie](https://github.com/nagatapote/scroll-movie) is the library that enables you to animate background image as you scroll the window.

# [Create Page Transitions in Next.js with Framer Motion](https://javascript.plainenglish.io/how-to-create-page-transitions-in-next-js-with-framer-motion-47642c462c62)

```javascript
import "../styles/globals.css";
import { motion } from "framer-motion";

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
  );
}

export default MyApp;
```
