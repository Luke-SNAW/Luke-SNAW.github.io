
## [Barrel](https://basarat.gitbook.io/typescript/main-1/barrel)

A barrel is a way to rollup exports from several modules into a single convenient module. The barrel itself is a module file that re-exports selected exports of other modules.

## [Module Resolution](https://www.typescriptlang.org/docs/handbook/module-resolution.html)

_Module resolution_ is the process the compiler uses to figure out what an import refers to. Consider an import statement like `import { a } from "moduleA"`; in order to check any use of `a`, the compiler needs to know exactly what it represents, and will need to check its definition `moduleA`.

At this point, the compiler will ask “what’s the shape of `moduleA`?” While this sounds straightforward, `moduleA` could be defined in one of your own `.ts`/`.tsx` files, or in a `.d.ts` that your code depends on.

## [Type Coercion](https://www.geeksforgeeks.org/what-is-type-coercion-in-javascript/)

**Type Coercion** refers to the process of automatic or implicit conversion of values from one data type to another.

## [Two types of equalities in JavaScript](https://www.syncfusion.com/blogs/post/5-different-ways-to-deep-compare-javascript-objects.aspx#:~:text=Two%20types%20of%20equalities%20in%20JavaScript)

When discussing object comparisons in JavaScript, there are two types of equalities one must be aware of:

- Referential equality: Determines whether the two provided operands refer to the same reference/object instance.
- Deep equality: Determines whether objects are equal by comparing each property in the operands.

Referential equality can be determined with equality operators such as strict equality (===) or coercive equality (==)
