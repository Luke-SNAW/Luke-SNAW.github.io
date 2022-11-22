---
id: mraMGoestTO9V6pkpE8XE
title: Language
desc: ''
updated: 1669100648008
created: 1644885695251
---

## Collections

- [10 Powerful JavaScript Destructuring Techniques Every Developer Should Know](https://javascript.plainenglish.io/10-powerful-javascript-destructuring-techniques-every-developer-should-know-15ae06818bb6)
- [New JavaScript features](https://exploringjs.com/impatient-js/ch_new-javascript-features.html)
- [How JavaScript Works](https://blog.devgenius.io/how-javascript-works-behind-the-scenes-88c546173f32)
- [Primitive vs Reference Data Types in JavaScript](https://www.freecodecamp.org/news/primitive-vs-reference-data-types-in-javascript/)
- [Compare require() vs import() in JavaScript](https://javascript.plainenglish.io/require-vs-import-in-js-82a7a47671f)
- [`export default thing` is different to `export { thing as default }`](https://jakearchibald.com/2021/export-default-thing-vs-thing-as-default/)
- [Optimizing JavaScript Standard Library Functions in JSC](https://webkit.org/blog/11934/optimizing-javascript-standard-library-functions-in-jsc/)
- [What Does 'this' Mean in JavaScript? The this Keyword Explained with Examples](https://www.freecodecamp.org/news/what-is-this-in-javascript/)
- [Lexical Scope in JavaScript](https://www.freecodecamp.org/news/javascript-lexical-scope-tutorial/)

  ```text
  Lexical scope is the definition area of an expression.

  In other words, an item's lexical scope is the place in which the item got created.

  Note:
  - Another name for lexical scope is static scope.
  - The place an item got invoked (or called) is not necessarily the item's lexical scope. Instead, an item's definition space is its lexical scope.
  ```

- [Arrow Functions vs. Regular Functions in JavaScript](https://blog.bitsrc.io/arrow-functions-vs-regular-functions-in-javascript-458ccd863bc1)
  - Simple Invocation: `this` equals the global object or maybe undefined if you are using strict mode.
  - Method Invocation: `this` equals the object that owns the method.
  - Indirect Invocation: `this` equals the first argument.
  - Constructor Invocation: `this` equals the newly created instance.
- [A pipe operator for JavaScript: introduction and use cases](https://2ality.com/2022/01/pipe-operator.html)
- [Understanding the “this” Keyword in JavaScript](https://betterprogramming.pub/understanding-the-this-keyword-in-javascript-cb76d4c7c5e8)
  - Immediately Invoked Function Expression (IIFE)
  - “this” Refers to an Invoker Object (Parent Object)
- [Classes vs. prototypal inheritance in vanilla JS](https://gomakethings.com/classes-vs.-prototypal-inheritance-in-vanilla-js/)
- [How the JavaScript Event Loop Works](https://javascript.plainenglish.io/what-is-the-javascript-event-loop-84d21ef276ee)
- [How Exactly Does the ‘new’ Keyword work in JavaScript?](https://javascript.plainenglish.io/how-exactly-new-keyword-works-in-javascript-af3abf238f8a)
- [prototype in Javascript](https://javascript.plainenglish.io/deep-understanding-of-prototypes-in-javascript-367a81f98847)
- [JavaScript Operators — What are Unary Operators?](https://javascript.plainenglish.io/javascript-operators-unary-operators-e9d33c94db5c)
- [How JavaScript Maps Can Make Your Code Faster](https://medium.com/@bretcameron/how-javascript-maps-can-make-your-code-faster-90f56bf61d9d)
- [How to remove items from an object with object destructuring and the spread operator](https://gomakethings.com/how-to-remove-items-from-an-object-with-object-destructuring-and-the-spread-operator/)
  ```javascript
  let { hobbies, height, eyes, ...merlinAbridged } = merlin
  ```
- [JavaScript's Forgotten Keyword (with)](https://dev.to/mistval/javascript-s-forgotten-keyword-with-48id)
- [How to avoid uncaught async errors in Javascript](https://advancedweb.hu/how-to-avoid-uncaught-async-errors-in-javascript/)
- [What is type coercion in vanilla JavaScript (and how does it work)?](https://gomakethings.com/what-is-type-coercion-in-vanilla-javascript-and-how-does-it-work/)
- [Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)
- [Why ['1', '7', '11'].map(parseInt) returns [1, NaN, 3] in Javascript](https://medium.com/dailyjs/parseint-mystery-7c4368ef7b21)
- [🔥 Frontend Interview Cheatsheet That Helped Me Get Offers From Amazon & LinkedIn](https://itnext.io/frontend-interview-cheatsheet-that-helped-me-to-get-offer-on-amazon-and-linkedin-cba9584e33c7)
- [JavaScript Under The Hood: Advanced Concepts Developers Should Know](https://blog.bitsrc.io/javascript-under-the-hood-advanced-concepts-developers-should-know-a89ddbb11228)
- [All About JavaScript Events](https://blog.openreplay.com/all-about-javascript-events/)
  - **Browser Events** These events occur in the browser [window](https://developer.mozilla.org/en-US/docs/Web/API/Window) rather than the HTML page. Event handlers are bound to the window object, not to the element. E.g., load, error, scroll, resize, etc.
  - **HTML Events** This is the inverse of the browser event. They are the event that occurs in the [element](https://developer.mozilla.org/en-US/docs/Web/API/Element), and the event handlers are bound to the element. E.g., click, mouseover, mouseenter, etc.

---

## [Avoid the “delete” Keyword in JavaScript](https://javascript.plainenglish.io/avoid-the-delete-keyword-in-javascript-87ff2a47f26c)

```javascript
const snowbit = {
  age: 15,
  test: "abc",
}
const { test, ...newSnowbit } = snowbit
console.log(newSnowbit) //  {age: 15}
```

Let me explain, You should not use `delete` to remove the property from the object because this mutates the original and that can lead to unpredictable behaviours and becomes difficult to debug.

## [What are wrapper objects for primitive values?](https://2ality.com/2022/02/wrapper-objects.html)

Each of the primitive types `boolean`, `number`, `bigint`, `string` and `symbol` has an associated _wrapper class_ (`Boolean`, `Number`, `BigInt`, `String`, `Symbol`). In this blog post, we examine what these classes are good for.

Table of contents:

1. [Wrapper classes for primitive types](https://2ality.com/2022/02/wrapper-objects.html#wrapper-classes-for-primitive-types)
2. [Instantiating wrapper classes](https://2ality.com/2022/02/wrapper-objects.html#instantiating-wrapper-classes)
   1. Generically wrapping primitive values
   2. Unwrapping primitive values
   3. Primitive values vs. wrapper objects
3. [Function-calling wrapper classes](https://2ality.com/2022/02/wrapper-objects.html#function-calling-wrapper-classes)
4. [Further reading](https://2ality.com/2022/02/wrapper-objects.html#further-reading)

## Closure

- [Closures](https://www.w3schools.com/js/js_function_closures.asp): A closure is a function having access to the parent scope, even after the parent function has closed.
- [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures): A function bundled together with its lexical environment forms a closure.

### [Advantages and Disadvantages of Closures](https://javascript.plainenglish.io/closures-in-javascript-js-interview-series-c93af277bfac)

#### Advantages

- Closures help in data encapsulation, i.e, with closures, you can store data in a separate scope and share it only where necessary.
- Modern JavaScript libraries (like React) heavily rely on closures for rendering components on state or prop change.

#### Disadvantages

- Closures consume a lot of memory space since the functions need to store the value of the variable in memory, even though the function of the variable itself would not be used multiple times in the code.

## Promise

- [JavaScript Promises: then(f,f) vs then(f).catch(f)](https://dmitripavlutin.com/javascript-promises-then-vs-then-catch/)

## Symbol

- [JavaScript Symbols: the Most Misunderstood Feature of the Language?](https://blog.bitsrc.io/javascript-symbols-the-most-misunderstood-feature-of-the-language-282b6e2a220e)

  ```javascript
  let a = "foo"
  ```

  - The primitive is “foo”, not `a`.
  - Another very interesting aspect around this, is that primitives in JavaScript are immutable. That means you can’t change the number 2 ever. Instead, you can reassign a variable to have another (immutable) primitive value.
  - Symbols are primitive values and can be assigned to variables.

- [All About JavaScript Events](https://blog.openreplay.com/all-about-javascript-events/)
  - **Browser Events** These events occur in the browser [window](https://developer.mozilla.org/en-US/docs/Web/API/Window) rather than the HTML page. Event handlers are bound to the window object, not to the element. E.g., load, error, scroll, resize, etc.
  - **HTML Events** This is the inverse of the browser event. They are the event that occurs in the [element](https://developer.mozilla.org/en-US/docs/Web/API/Element), and the event handlers are bound to the element. E.g., click, mouseover, mouseenter, etc.


- [All About JavaScript Events](https://blog.openreplay.com/all-about-javascript-events/)
  - **Browser Events** These events occur in the browser [window](https://developer.mozilla.org/en-US/docs/Web/API/Window) rather than the HTML page. Event handlers are bound to the window object, not to the element. E.g., load, error, scroll, resize, etc.
  - **HTML Events** This is the inverse of the browser event. They are the event that occurs in the [element](https://developer.mozilla.org/en-US/docs/Web/API/Element), and the event handlers are bound to the element. E.g., click, mouseover, mouseenter, etc.