
## Collections

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
- [The truth about CSS selector performance](https://blogs.windows.com/msedgedev/2023/01/17/the-truth-about-css-selector-performance/)
- [The Ultimate Low-Quality Image Placeholder Technique](https://csswizardry.com/2023/09/the-ultimate-lqip-lcp-technique/)
- [CSS :has() performance](https://www.joshwcomeau.com/css/has/#:~:text=What%20about%20performance%3F) - Browsers are really good at doing style recalculation. This isn't something we need to worry about. 😄
- [Improving rendering performance with CSS `content-visibility`](https://nolanlawson.com/2024/09/18/improving-rendering-performance-with-css-content-visibility/)
  - This final solution achieved around a 45% performance improvement in both Chrome and Firefox, reducing the load time from 3 seconds to 1.3 seconds.
  - While satisfied with the [content-visibility](https://web.dev/articles/content-visibility) approach, the author acknowledges that a true virtual list implementation would likely provide even better performance, especially for larger datasets.
