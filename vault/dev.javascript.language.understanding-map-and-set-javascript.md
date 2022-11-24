---
id: ty18338r7mpf80hm3a3z2g5
title: Understanding Map and Set JavaScript
desc: ""
updated: 1669167367209
created: 1669167355784
---

> https://www.taniarascia.com/understanding-map-and-set-javascript/

## When to Use Map

Summing up, Maps are similar to Objects in that they hold key/value pairs, but Maps have several advantages over objects:

- Size - Maps have a size property, whereas Objects do not have a built-in way to retrieve their size.
- Iteration - Maps are directly iterable, whereas Objects are not.
- Flexibility - Maps can have any data type (primitive or Object) as the key to a value, while Objects can only have strings.
- Ordered - Maps retain their insertion order, whereas objects do not have a guaranteed order.

Due to these factors, Maps are a powerful data structure to consider. However, Objects haves some important advantages as well:

- JSON - Objects work flawlessly with JSON.parse() and JSON.stringify(), two essential functions for working with JSON, a common data format that many REST APIs deal with.
- Working with a single element - Working with a known value in an Object, you can access it directly with the key without the need to use a method, such as Map's get().

This list will help you decide if a Map or Object is the right data structure for your use case.
