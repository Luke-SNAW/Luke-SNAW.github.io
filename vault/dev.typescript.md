---
id: 2ijeu1j04o0qzmy7hzk1tlb
title: TypeScript
desc: ""
updated: 1725600314374
created: 1652057928334
---

## Collections

- [Stop SHOUTING = 'shouting'](https://swizec.com/blog/stop-shouting-shouting/)
- [Typing Component Props | React TypeScript Cheatsheets](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example/#basic-prop-types-examples)
- [TypeScript Generics: What’s with the Angle Brackets <>?](https://javascript.plainenglish.io/typescript-generics-whats-with-the-angle-brackets-4e242c567269)
- [Covariance and Contravariance in TypeScript](https://dmitripavlutin.com/typescript-covariance-contravariance/)
- [A Simple Explanation of Function Overloading in TypeScript](https://dmitripavlutin.com/typescript-function-overloading/)
- [TypeScript Features to Avoid](https://www.executeprogram.com/blog/typescript-features-to-avoid)
- [The Shocking Secret About Static Types](https://medium.com/javascript-scene/the-shocking-secret-about-static-types-514d39bf30a3)
- [Index Signatures in TypeScript](https://dmitripavlutin.com/typescript-index-signatures/)
  ```typescript
  type SpecificSalary = Record<"yearlySalary" | "yearlyBonus", number>
  interface StringByString {
    [key: string]: string | undefined
  }
  const object: StringByString = {}
  ```
- [3 Useful TypeScript Patterns to Keep in Your Back Pocket](https://spin.atomicobject.com/2021/05/11/3-useful-typescript-patterns/)

  ```typescript
  type Names = "Bob" | "Bill" | "Ben"
  type JobTitles = "Welder" | "Carpenter" | "Plumber"

  const JobAssignments: { [Key in Names]: JobTitles } = {
    Bob: "Welder",
    Bill: "Carpenter",
    Ben: "Plumber",
  }
  ```

- [Why Are Const Assertions a Gem in TypeScript?](https://blog.bitsrc.io/why-are-const-assertions-a-gem-in-typescript-e1d353f5d8ce)
- [All JavaScript and TypeScript Features of the last 3 years](https://betterprogramming.pub/all-javascript-and-typescript-features-of-the-last-3-years-629c57e73e42)

## Overrated?

- [Static typing helps, but only a little.](https://buildtogether.tech/tooling/#:~:text=Static%20typing%20helps%2C%20but%20only%20a%20little.)
- [The TypeScript Tax](https://medium.com/javascript-scene/the-typescript-tax-132ff4cb175b)
- [The Shocking Secret About Static Types](https://medium.com/javascript-scene/the-shocking-secret-about-static-types-514d39bf30a3)

## Type, interface

- [Differences Between TypeScript Type vs Interface](https://www.educba.com/typescript-type-vs-interface/)
- [Type vs Interface in TypeScript](https://blog.bitsrc.io/type-vs-interface-in-typescript-cf3c00bc04ae)
  - Use interfaces when:
    - A new object or an object method needs to be defined.
    - You wish to benefit from declaration merging.
  - Use types when:
    - You need to define a primitive-type alias
    - Defining tuple types
    - Defining a union
    - You must create functions and attempt to overload them in object types through composition.
    - Requiring the use of mapped types
- [Using type predicates](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#using-type-predicates)
  - `#4 Use type predicate to avoid type assertion` in [11 Tips That Make You a Better Typescript Programmer](https://dev.to/zenstack/11-tips-that-help-you-become-a-better-typescript-programmer-4ca1)

### [Differences Between Type Aliases and Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

Type aliases and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an `interface` are available in `type`, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

#### Extending an interface

```ts
interface Animal {
  name: string
}
interface Bear extends Animal {
  honey: boolean
}
const bear = getBear()
bear.name
bear.honey
```

#### Extending a type via intersections

```ts
type Animal = {
  name: string
}
type Bear = Animal & { honey: boolean }
const bear = getBear()
bear.name
bear.honey
```

#### Adding new fields to an existing interface

```ts
interface Window {
  title: string
}
interface Window {
  ts: TypeScriptAPI
}
const src = 'const a = "Hello World"'
window.ts.transpileModule(src, {})
```

#### A type cannot be changed after being created

```ts
type Window = { title: string }
type Window = { ts: TypeScriptAPI }
// Error: Duplicate identifier 'Window'.
```

### [Preferring Interfaces Over Intersections](https://github.com/microsoft/TypeScript/wiki/Performance#preferring-interfaces-over-intersections)

Much of the time, a simple type alias to an object type acts very similarly to an interface.

```ts
interface Foo {
  prop: string
}

type Bar = { prop: string }
```

However, and as soon as you need to compose two or more types, you have the option of extending those types with an interface, or intersecting them in a type alias, and that's when the differences start to matter.

Interfaces create a single flat object type that detects property conflicts, which are usually important to resolve! Intersections on the other hand just recursively merge properties, and in some cases produce `never`. Interfaces also display consistently better, whereas type aliases to intersections can't be displayed in part of other intersections. Type relationships between interfaces are also cached, as opposed to intersection types as a whole. A final noteworthy difference is that when checking against a target intersection type, every constituent is checked before checking against the "effective"/"flattened" type.

For this reason, extending types with `interface`s/`extends` is suggested over creating intersection types.

```diff
- type Foo = Bar & Baz & {
-     someProp: string;
- }
+ interface Foo extends Bar, Baz {
+     someProp: string;
+ }
```
