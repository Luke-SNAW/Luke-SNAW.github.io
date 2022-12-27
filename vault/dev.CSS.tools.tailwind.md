---
id: t551a82h3taujz7zlf5c8pm
title: Tailwind
desc: ""
updated: 1672126434449
created: 1672120075569
---

## [Dynamic class names](https://tailwindcss.com/docs/content-configuration#dynamic-class-names)

```js
class = `bg-${ zero ? pageColor : baseColor}` // not work
class = zero ? `bg-${pageColor}` : `bg-${baseColor}` // not work
```
