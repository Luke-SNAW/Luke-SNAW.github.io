---
id: ycbm1pqytzrms1hjatwjh7y
title: Performance
desc: ""
updated: 1646130207313
created: 1646130152552
---

- [Does shadow DOM improve style performance?](https://nolanlawson.com/2021/08/15/does-shadow-dom-improve-style-performance/): Kinda. It depends. And it might not be enough to make a big difference in the average web app. But it’s worth understanding why.
- [How I made Google’s data grid scroll 10x faster with one line of CSS](https://medium.com/@johan.isaksson/how-i-made-googles-data-grid-scroll-10x-faster-with-one-line-of-css-78cb1e8d9cb1)
  ```css
  table {
    contain: strict;
  }
  ```
- [When is it “Right” to Reach for contain and will-change in CSS?](https://css-tricks.com/when-is-it-right-to-reach-for-contain-and-will-change-in-css/): [the will-change property](https://css-tricks.com/almanac/properties/w/will-change/)
- [Frontend Web Performance: The Essentials [0]](https://medium.com/@matthew.costello/frontend-web-performance-the-essentials-0-61fea500b180): Layout Bad, Composite Good
  - https://csstriggers.com/
  - https://gist.github.com/paulirish/5d52fb081b3570c81e3a
