---
id: t551a82h3taujz7zlf5c8pm
title: Tailwind
desc: ''
updated: 1765418251878
created: 1672120075569
---

- [Tailwind, and the death of web craftsmanship](https://pdx.su/blog/2023-07-26-tailwind-and-the-death-of-craftsmanship/)
  > While Tailwind may help with initial development speed, it can reduce craftsmanship and make code harder to work with over time.
- [Utility First, Component Second](https://mytory.net/archives/17476)
  - 유틸리티 우선 방법론은 컴포넌트 구성 시점을 늦춤으로써, 개발자가 유틸리티로 빠르게 시작하고 중복이 보일 때 컴포넌트를 만드는 '시점'의 문제로 전환했습니다.
  - 유틸리티 우선 방법론에서 'First'는 유틸리티 중시뿐만 아니라, 컴포넌트 구성 시점을 늦추는 관점을 도입하여 CSS 아키텍처의 난제를 해결하는 데 기여했습니다.

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

## [tints.dev](https://www.tints.dev/) - Palette Generator + API for Tailwind CSS
