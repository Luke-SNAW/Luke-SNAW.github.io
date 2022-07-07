---
id: nr2q81zle9rmxaq4qvcs01z
title: Reflect
desc: ""
updated: 1657096060798
created: 1657096012313
---

> https://www.javascripttutorial.net/es6/javascript-reflection/  
> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect

## What is reflection

In computer programming, reflection is the ability of a program to manipulate [variables](https://www.javascripttutorial.net/javascript-variables/), properties, and methods of [objects](https://www.javascripttutorial.net/javascript-objects/) at runtime.

Prior to ES6, JavaScript already has reflection features even though they were not officially called that by the community or the specification. For example, methods like `Object.keys()`, `Object.getOwnPropertyDescriptor()`, and `Array.isArray()` are the classic reflection features.

ES6 introduces a new global object called `Reflect` that allows you to call methods, construct objects, get and set properties, manipulate and extend properties.

The `Reflect` API is important because it allows you to develop programs and frameworks that are able to handle dynamic code.
