---
id: mraMGoestTO9V6pkpE8XE
title: Language
desc: ""
updated: 1666679946697
created: 1644885695251
---

## Collections

- [10 Powerful JavaScript Destructuring Techniques Every Developer Should Know](https://javascript.plainenglish.io/10-powerful-javascript-destructuring-techniques-every-developer-should-know-15ae06818bb6)
- [How to Read the ECMAScript Specification](https://timothygu.me/es-howto/)
- [New JavaScript features](https://exploringjs.com/impatient-js/ch_new-javascript-features.html)

---

## [Avoid the “delete” Keyword in JavaScript](https://javascript.plainenglish.io/avoid-the-delete-keyword-in-javascript-87ff2a47f26c)

```javascript
const snowbit = {
  age: 15,
  test: "abc",
};
const { test, ...newSnowbit } = snowbit;
console.log(newSnowbit); //  {age: 15}
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
