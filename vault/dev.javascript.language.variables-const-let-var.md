---
id: zu7v05kxz33bidk9rfw4gsn
title: "A Simple Explanation of JavaScript Variables: const, let, var"
desc: ""
updated: 1667779600875
created: 1667779566316
---

> https://dmitripavlutin.com/javascript-variables-const-let-var/

In contrast to const and let, the scope of the var variables is defined only by the function body:

```javascript
function welcomeTo() {
  // Function scope
  var city = "Gotham";
  console.log(`Welcome to ${city}!`); // logs 'Welcome to Gotham!'
}
console.log(`Welcome to ${city}!`); // throws ReferenceError

welcomeTo();
```

A code block doesn’t create a scope for var variables:

```javascript
if (true) {
  // Code block scope
  var city = "Gotham";
  console.log(city); // logs 'Gotham'
}
console.log(city); // logs 'Gotham'
```

Normally, you won’t access a var variable before the declaration statement. But if you do, JavaScript won’t throw a reference error, but rather evaluate the variable to undefined:

```javascript
console.log(city); // logs undefined
var city = "Gotham";
```

It happens because a var variables hoists up to the top of the scope.
