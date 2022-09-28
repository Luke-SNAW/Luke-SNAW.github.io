---
id: 8modsw2sp3142owxlp8t1qr
title: Web Browser
desc: ""
updated: 1664336991186
created: 1646811472608
---

# Web apps

- [Pomodoro Timer](https://pomodorotimer.online/)

# Firefox add-ons

- Simple Translate: simpler and faster than `To Google Translate`

# Web browser extensions

- [SingleFile](https://github.com/gildas-lormeau/SingleFile) is a Web Extension (and a CLI tool) compatible with Chrome, Firefox (Desktop and Mobile), Microsoft Edge, Vivaldi, Brave, Waterfox, Yandex browser, and Opera. It helps you to save a complete web page into a single HTML file.
- [How do Chrome extensions impact browser performance?](https://www.debugbear.com/blog/chrome-extension-performance-2021)
- [JavaScript Restrictor](https://polcak.github.io/jsrestrictor/) - Various websites collect information about users without their awareness.
- [Stylish](https://chrome.google.com/webstore/detail/stylish-custom-themes-for/fjnbnpbmkenffdnngjfgmeleoegfcffe?hl=en) - Custom themes for any website
- [Stylus](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne?hl=en)

# Bookmarklet

## [kill-sticky](https://github.com/t-mart/kill-sticky)

Bookmarklet to remove sticky elements and restore scrolling to web pages!

> https://news.ycombinator.com/item?id=32998091

```js
javascript:(function()%7Bdocument.querySelectorAll(%22body%20*%22).forEach(function(node)%7Bif(%5B%22fixed%22%2C%22sticky%22%5D.includes(getComputedStyle(node).position))%7Bnode.parentNode.removeChild(node)%7D%7D)%3Bdocument.querySelectorAll(%22html%20*%22).forEach(function(node)%7Bvar%20s%3DgetComputedStyle(node)%3Bif(%22hidden%22%3D%3D%3Ds%5B%22overflow%22%5D)%7Bnode.style%5B%22overflow%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-x%22%5D)%7Bnode.style%5B%22overflow-x%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-y%22%5D)%7Bnode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D%7D)%3Bvar%20htmlNode%3Ddocument.querySelector(%22html%22)%3BhtmlNode.style%5B%22overflow%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-x%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D)()%3B%0A
```
