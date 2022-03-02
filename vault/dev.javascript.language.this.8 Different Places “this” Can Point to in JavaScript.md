---
id: 3lspn87w7vnetrruly0x1ji
title: 8 Different Places “this” Can Point to in JavaScript
desc: ""
updated: 1646351862873
created: 1646351848979
---

https://blog.bitsrc.io/where-exactly-does-this-point-to-in-javascript-2be1e3fad1fd

# Function context

```javascript
var name = "window";
var doSth = function () {
  console.log(this.name);
};
doSth(); // 'window'
```

```javascript
let name2 = "window2";
let doSth2 = function () {
  console.log(this === window);
  console.log(this.name2);
};
doSth2(); // true, undefined
```
