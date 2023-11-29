---
id: 8modsw2sp3142owxlp8t1qr
title: Web browser tools
desc: ""
updated: 1701247755159
created: 1646811472608
---

## Web apps

- [Pomodoro Timer](https://pomodorotimer.online/)

## Chrome

- chrome://settings/adPrivacy
- chrome://inspect/#devices

## Web browser extensions

- [SingleFile](https://github.com/gildas-lormeau/SingleFile) is a Web Extension (and a CLI tool) compatible with Chrome, Firefox (Desktop and Mobile), Microsoft Edge, Vivaldi, Brave, Waterfox, Yandex browser, and Opera. It helps you to save a complete web page into a single HTML file.
- [How do Chrome extensions impact browser performance?](https://www.debugbear.com/blog/chrome-extension-performance-2021)
- [JavaScript Restrictor](https://polcak.github.io/jsrestrictor/) - Various websites collect information about users without their awareness.
- [Copy as Markdown for Chrome & Firefox](https://github.com/yorkxin/copy-as-markdown)
- [Live Stream Downloader](https://chrome.google.com/webstore/detail/live-stream-downloader/looepbdllpjgdmkpdcdffhdbmpbcfekj)

### Firefox add-ons

- Simple Translate: simpler and faster than `To Google Translate`

## Bookmarklet

### [kill-sticky](https://github.com/t-mart/kill-sticky)

Bookmarklet to remove sticky elements and restore scrolling to web pages!

> https://news.ycombinator.com/item?id=32998091

```js
javascript:(function()%7Bdocument.querySelectorAll(%22body%20*%22).forEach(function(node)%7Bif(%5B%22fixed%22%2C%22sticky%22%5D.includes(getComputedStyle(node).position))%7Bnode.parentNode.removeChild(node)%7D%7D)%3Bdocument.querySelectorAll(%22html%20*%22).forEach(function(node)%7Bvar%20s%3DgetComputedStyle(node)%3Bif(%22hidden%22%3D%3D%3Ds%5B%22overflow%22%5D)%7Bnode.style%5B%22overflow%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-x%22%5D)%7Bnode.style%5B%22overflow-x%22%5D%3D%22visible%22%7Dif(%22hidden%22%3D%3D%3Ds%5B%22overflow-y%22%5D)%7Bnode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D%7D)%3Bvar%20htmlNode%3Ddocument.querySelector(%22html%22)%3BhtmlNode.style%5B%22overflow%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-x%22%5D%3D%22visible%22%3BhtmlNode.style%5B%22overflow-y%22%5D%3D%22visible%22%7D)()%3B%0A
```

### [Getting all links from any web site into a spreadsheet using browser developer tools](https://christianheilmann.com/2023/08/24/quick-tip-getting-all-links-from-any-web-site-into-a-spreadsheet-using-browser-developer-tools/) - `console.table($$('a'),['innerHTML','href'])`

## Dev

- [67 Weird Debugging Tricks Your Browser Doesn't Want You to Know](https://alan.norbauer.com/articles/browser-debugging-tricks/)
