---
id: IowIScQvzEu3KQ4dvwPTt
title: JavaScript
desc: ""
updated: 1671695236101
created: 1645056460403
---

## Collections

- [Track down the JavaScript code responsible for polluting the global scope](https://mmazzarolo.com/blog/2022-02-16-track-down-the-javascript-code-responsible-for-polluting-the-global-scope/)
- [Web Developers Don’t Just Know About localStorage](https://medium.com/frontend-canteen/web-developers-dont-just-know-about-localstorage-2f37385bd8ad)
- 🛁 [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript) - Clean Code concepts adapted for JavaScript

## [15 Useful JavaScript Tips](https://javascript.plainenglish.io/15-useful-javascript-tips-814eeba1f4fd)

### Event listeners run only once

```js
element.addEventListener("click", () => console.log("I run only once"), {
  once: true,
})
```

### element’s dataset

```html
<div id="user" data-name="Maxwell" data-age="32" data-something="Some Data">
  Hello Maxwell
</div>
<script>
  const user = document.getElementById("user")

  console.log(user.dataset)
  // { name: "Maxwell", age: "32", something: "Some Data" }

  console.log(user.dataset.name) // "Maxwell"
  console.log(user.dataset.age) // "32"
  console.log(user.dataset.something) // "Some Data"
</script>
```
