
## Media Queries

- [media query: hover](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/hover)
- [media query: pointer](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/pointer)

## Container Queries

- [An Interactive Guide to CSS Container Queries](https://ishadeed.com/article/css-container-query-guide)

  ```css
  /* Try to add more items and see what happens. */
  .timelineWrapper {
    container: timeline / inline-size;
    --force-vertical: false;

    &:has(.c-timeline__item:nth-last-child(n + 5)) {
      --force-vertical: true;
    }
  }
  ```

  ```css
  @container timeline (inline-size > 430px) and style(--force-vertical: false) {
    /* Apply the full variation. */
  }
  ```

- [A Friendly Introduction to Container Queries](https://www.joshwcomeau.com/css/container-queries-introduction/)

## Style Queries

- [CSS Style Queries](https://ishadeed.com/article/css-container-style-queries/)
- [Getting Started with Style Queries](https://developer.chrome.com/docs/css-ui/style-queries?hl=en)
  - Can't you do it with attributes?
