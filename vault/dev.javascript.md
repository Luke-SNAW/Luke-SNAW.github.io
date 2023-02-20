---
id: IowIScQvzEu3KQ4dvwPTt
title: JavaScript
desc: ""
updated: 1676866804948
created: 1645056460403
---

## Collections

- [Track down the JavaScript code responsible for polluting the global scope](https://mmazzarolo.com/blog/2022-02-16-track-down-the-javascript-code-responsible-for-polluting-the-global-scope/)
- [Web Developers Don’t Just Know About localStorage](https://medium.com/frontend-canteen/web-developers-dont-just-know-about-localstorage-2f37385bd8ad)
- 🛁 [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript) - Clean Code concepts adapted for JavaScript
- [Ask HN: Why did Frontend development explode in complexity?](https://news.ycombinator.com/item?id=34218003)
- [10 Web Development Trends in 2023](https://www.robinwieruch.de/web-development-trends/)
- [useSignal() is the future of web frameworks and is a better abstraction than useState(), which is showing its age.](https://javascriptweekly.com/link/135369/web)
- [React Server Components vs. Server-Side Rendering](https://www.thearmchaircritic.org/mansplainings/react-server-components-vs-server-side-rendering)
  - https://beta.nextjs.org/docs/rendering/fundamentals

## [Discover the Magic of Portals: A Beginner’s Guide to React’s Most Powerful Tool](https://blog.bitsrc.io/discover-the-magic-of-portals-a-beginners-guide-to-react-s-most-powerful-tool-f6f1965ea305)

Portals allow you to render components outside of their parent component’s tree.

### When should you use portals?

- Modals and dialogs
- Tooltips and popovers
- Overlaying content

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

## API

- [The User Activation API](https://webkit.org/blog/13862/the-user-activation-api/)
