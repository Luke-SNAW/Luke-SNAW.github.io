---
id: 9bv9bxtia6w6yhb0rz3bz92
title: Terminology
desc: ""
updated: 1668055510936
created: 1667956494535
---

## [Barrel](https://basarat.gitbook.io/typescript/main-1/barrel)

A barrel is a way to rollup exports from several modules into a single convenient module. The barrel itself is a module file that re-exports selected exports of other modules.

## [Module Resolution](https://www.typescriptlang.org/docs/handbook/module-resolution.html)

_Module resolution_ is the process the compiler uses to figure out what an import refers to. Consider an import statement like `import { a } from "moduleA"`; in order to check any use of `a`, the compiler needs to know exactly what it represents, and will need to check its definition `moduleA`.

At this point, the compiler will ask “what’s the shape of `moduleA`?” While this sounds straightforward, `moduleA` could be defined in one of your own `.ts`/`.tsx` files, or in a `.d.ts` that your code depends on.

## [Type Coercion](https://www.geeksforgeeks.org/what-is-type-coercion-in-javascript/)

**Type Coercion** refers to the process of automatic or implicit conversion of values from one data type to another.
