
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
