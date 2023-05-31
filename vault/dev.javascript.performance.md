---
id: qJYy3qzZt6rXHWQJPZd9Q
title: Javascript Performance
desc: ""
updated: 1685417870148
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
