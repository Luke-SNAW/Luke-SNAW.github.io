---
id: qJYy3qzZt6rXHWQJPZd9Q
title: Javascript Performance
desc: ""
updated: 1712124428120
created: 1644479524849
---

## Collections

- [RAIL 모델을 사용한 성능 측정](https://web.dev/rail/)
  - 응답: 50ms 미만으로 이벤트 처리
  - 애니메이션: 10ms 안에 프레임 생성
  - 로드: 5초 이내에 콘텐츠를 전달하고 상호 작용 준비하기
  - [RAIL 측정 도구](https://web.dev/rail/#chrome-devtools)
- [New browser APIs to detect JavaScript performance problems in production](https://michaelscodingspot.com/javascript-performance-apis/)
- [How JavaScript engines achieve great performance](https://blogg.bekk.no/how-javascript-engines-achieve-great-performance-fb0b36601557)
- [Add a Service Worker to Your Site](https://css-tricks.com/add-a-service-worker-to-your-site/): Serve frequently accessed assets from your local cache instead of the network, reducing data usage and improving performance.
- [12 Front End Performance Patterns You Need to Know](https://medium.com/geekculture/12-front-end-performance-patterns-you-need-to-know-def550620464)
  - SSG with SWR
  - Use Responsive, Compressed, WebP Formatted Images, Served via a CDN
  - Minify, Compress, & Serve Your Static Code Files via a CDN
  - Prefetching
  - Lazy Loading
  - Caching
- [Speeding up VSCode (extensions) in 2022](https://jason-williams.co.uk/speeding-up-vscode-extensions-in-2022)
- [Patterns.dev](https://www.patterns.dev/) is a free book on design patterns and component patterns for building powerful web apps with vanilla JavaScript and React.
- [Precise Timing With Web Animations API](https://www.smashingmagazine.com/2022/06/precise-timing-web-animations-api/)
- [Speeding up the JavaScript ecosystem - eslint](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-3/)
- [Mastering the Art of Efficient JavaScript DOM Manipulation](https://itnext.io/mastering-the-art-of-efficient-javascript-dom-manipulation-899b5cbf5a3f)
  - Use document fragments
  - Use event delegation - `event.target.matches`
- [In Defence of DOMContentLoaded](https://csswizardry.com/2023/07/in-defence-of-domcontentloaded/)
  > The DOMContentLoaded event fires once all of your deferred JavaScript has finished running.
- [Speeding up the JavaScript ecosystem - Polyfills gone rogue](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-6/)
  > Many popular npm packages depend on 6-8x more packages than they need to. Most of these are unnecessary polyfills.
- [Optimizing Javascript for fun and for profit](https://romgrk.com/posts/optimizing-javascript)
  - [Avoid different shapes](https://romgrk.com/posts/optimizing-javascript#2-avoid-different-shapes)

## [Speeding up the JavaScript ecosystem - The barrel file debacle](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-7/)

The use of barrel files, which only re-export other files, is very common in large JavaScript projects.

However, they can significantly slow down development tasks by forcing the rebuilding of the entire module graph for every file. This is because JavaScript engines must fully parse and evaluate all import statements.

The article provides data showing that constructing the module graph for 10 files is much faster than for 30,000 files. Barrel files can cause test runners to waste minutes rebuilding the graph for each test. Linters are also severely impacted, sometimes taking hours to run.

Removing unnecessary barrel files can dramatically improve performance, speeding up builds by 60-80% according to the author.

## [JavaScript Hydration Is a Workaround, Not a Solution](https://thenewstack.io/javascript-hydration-is-a-workaround-not-a-solution/)

JavaScript hydration is a technique used to add interactivity to server-rendered HTML pages by attaching event handlers to DOM elements on the client-side.

However, this process requires recovering the necessary information to rebuild the application state and framework state. The document argues that hydration is an overhead because it duplicates the work already done by the server.

A better approach called resumability avoids this overhead by serializing and transferring the necessary information from server to client. This allows lazy execution of event handlers on the client-side instead of eagerly executing all components.
