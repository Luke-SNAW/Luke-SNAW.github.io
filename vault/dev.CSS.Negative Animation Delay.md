---
id: izqeslz6vrffmc6c9b3y8qb
title: Negative Animation Delay
desc: ""
updated: 1660779568769
created: 1660779387599
---

> https://css-irl.info/quick-tip-negative-animation-delay/

```html
<h1>
  <span style="--i: 0">B</span>
  <span style="--i: 1">O</span>
  <span style="--i: 2">U</span>
  <span style="--i: 3">N</span>
  <span style="--i: 4">C</span>
  <span style="--i: 5">I</span>
  <span style="--i: 6">N</span>
  <span style="--i: 7">G</span>
</h1>
```

```css
span {
  --delay: calc(var(--i) * 200ms);
  animation: bounce 500ms var(--delay, 0) infinite;
}
```

![With a negative delay, all the characters are animating straight away.](https://css-irl.info/quick-tip-negative-animation-delay-02.webp)
