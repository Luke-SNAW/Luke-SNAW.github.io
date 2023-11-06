---
id: t551a82h3taujz7zlf5c8pm
title: Tailwind
desc: ""
updated: 1698985346392
created: 1672120075569
---

## [Dynamic class names](https://tailwindcss.com/docs/content-configuration#dynamic-class-names)

```js
class = `bg-${ zero ? pageColor : baseColor}` // not work
class = zero ? `bg-${pageColor}` : `bg-${baseColor}` // not work
```

## [Unknown at rule @apply css(unknownAtRules)](https://github.com/tailwindlabs/tailwindcss/discussions/5258)

use `lang="postcss"` [#](https://github.com/tailwindlabs/tailwindcss/discussions/5258#discussioncomment-3055628)

webpack css loader에 추가

```js
exports.cssLoaders = function (options) {
  return {
    postcss: generateLoaders("sass"), // // https://vue-loader.vuejs.org/en/configurations/extract-css.html
  }
}
```
