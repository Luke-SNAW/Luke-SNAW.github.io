---
id: 61h3ipl1kp9q6ut8qbd906x
title: style-a-parent-element-based-on-its-number-of-children-using-css-has
desc: ""
updated: 1669535915339
created: 1669535891000
---

> https://www.bram.us/2022/11/17/style-a-parent-element-based-on-its-number-of-children-using-css-has/

```css
/* At most 3 (3 or less, excluding 0) children */
ul:has(> :nth-child(-n + 3):last-child) {
  outline: 1px solid red;
}

/* At most 3 (3 or less, including 0) children */
ul:not(:has(> :nth-child(3))) {
  outline: 1px solid red;
}

/* Exactly 5 children */
ul:has(> :nth-child(5):last-child) {
  outline: 1px solid blue;
}

/* At least 10 (10 or more) children */
ul:has(> :nth-child(10)) {
  outline: 1px solid green;
}

/* Between 7 and 9 children (boundaries inclusive) */
ul:has(> :nth-child(7)):has(> :nth-child(-n + 9):last-child) {
  outline: 1px solid yellow;
}
```
