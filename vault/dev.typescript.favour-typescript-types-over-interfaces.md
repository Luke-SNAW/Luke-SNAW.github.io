---
id: sdltx77jqmnlqumlnblxrpd
title: Favour TypeScript Types Over Interfaces
desc: ""
updated: 1683519333412
created: 1683519145571
---

> https://www.lloydatkinson.net/posts/2023/favour-typescript-types-over-interfaces/

Some time ago, I came to the conclusion that the TypeScript `type` keyword should almost always be favoured over the `interface` keyword. I arrived at this conclusion after considering the use cases and implications. Of course, there is a large overlap, but I personally believe that interfaces (in TypeScript) are a more restrictive and less useful construct than types.

## Overlapping functionality

When I first used TypeScript, I was surprised that two language features could be so similar as to appear almost indistinguishable.

- Both allow for declaring a contract or _shape_ of a type[^1]
- Both can be members of a union type
- Both can be extended to create derived types
- Both can be used for OO inheritance with classes and the `implements` keyword

## Types are more widely applicable

The type construct is more general purpose than interfaces. Consider the following code block.

```ts
type Status = "standard" | "vip"
type User = { name: string; status: Status }
```

Not only was a contract or _shape_ of a user-defined, but a union type was also defined. A clear advantage is revealed; types can express multiple constructs and are more versatile than interfaces.

Union types are also _explicitly_ part of the syntax, such as `string | number.` That is, types are a more natural and everyday occurrence in TypeScript. For example, consider the following code block.

```ts
// This is not valid.
// interface Status = 'standard' | 'vip';

type Status = 'standard' | 'vip';
interface User = { name: string, status: Status };
```

What has been achieved here compared to the first code block, other than extra characters and using two keywords and language features over one? Not much - other than confusion when revisiting the codebase and raising questions as to why both were used.

## Using types is more consistent

The previous section demonstrates that types are less restrictive and surpass the use cases of interfaces. Continuing to use both keywords is simply inconsistent for no good reason. Making the choice between them is not difficult. The stricter but more versatile keyword or the looser and less useful keyword?

`Type` wins.

## Interfaces can be merged (that’s rarely good)

Interfaces support [declaration merging](https://www.typescriptlang.org/docs/handbook/declaration-merging.html). This is definetly a “feature” to be cautious of. It has two good use cases - creating or extending the typings of third party libraries and declaring environment variables.

```ts
/// <reference types="astro/client" />

interface ImportMetaEnv {
  readonly PLAUSIBLE_API_KEY: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

Outside of those two use cases, I do not see any value in the following code block. It’s simply confusing, especially if multiple interfaces with the same name are created throughout the code base.

```ts
interface Box {
  height: number
  width: number
}
interface Box {
  scale: number
}
const box: Box = { height: 5, width: 6, scale: 10 }
```

## Interfaces lean more towards OO thinking

Interfaces are, by their nature, strongly tied to classes. I would even suggest that interfaces were added to TypeScript specifically to support the class-based OO paradigm.

**To be clear**, I’m not saying OO is bad (though I often favour functional concepts), but let’s be realistic - the TypeScript (and JavaScript) ecosystem leans strongly towards approximately two paradigms: non-class based object orientation and functional.

I can only think of two examples where I used classes or OO with TypeScript recently. This strongly contrasts with a typical project using UI libraries like React, where simple functions + data (often in the form of hooks) and declarative patterns and concepts are commonplace[^2].

There are some common myths used to “sell” TypeScript to developers. I believe some of these myths are harmful and perpetuate this “let’s apply OO everywhere without considering the implications of the ecosystem”. One of these is that [because TypeScript has classes, it is an OO language](https://dev.to/macsikora/no-typescript-is-not-oop-version-of-javascript-3ed4) - it’s a multi-paradigm language. Aside from the fact that JavaScript also has classes, this myth is popular amongst developers who have only experienced OO.

This is a topic I’d like to expand on more in another article, so I’ll finish this section with an insightful talk from Douglas Crockford.

> There are a few we know are gonna be bad. The worst is class. Class was the most requested new feature in JavaScript and all of the requests came from Java programmers who have to program in JavaScript and don’t want to have to learn how to do that.

## Types can still be used with classes

Again demonstrating the versatility of types, I created a customer processor in a typical OO style. There are two types available for implementation, and both are examples of [higher-order functions](https://fsharpforfunandprofit.com/posts/dependency-injection-1/) (or in OO terminology: [dependency injection](https://blog.ploeh.dk/2017/01/27/from-dependency-injection-to-dependency-rejection/s)). No interfaces here, yet still featuring composition.

```ts
type Trackable = {
  onProgress: ((progress: number) => void) | null
}

type CustomerProcessor = {
  processBatch(customers: Customer[]): void
}

class CustomerProcessorWithProgress implements CustomerProcessor, Trackable {
  private processed: number = 0

  onProgress: ((progress: number) => void) | null = null

  processBatch(customers: Customer[]) {
    this.processed = this.processed + customers.length
    this.onProgress?.(this.processed)
  }
}
```

[Playground Link (full version)](https://www.typescriptlang.org/play?#code/C4TwDgpgBAwgrgZ2AewLYQE5QLxQEoQCGAJsgHYA2IAPAN4BQUTUZh6AXFEhgJZkDmAbkbMMEAMbIMxBJzJxUAI0wBtALrCAvgD5h9UJCgAVDIXEBrQoorRcDZlHIAFDMn5iEsqAApvYV+4QnnIKyhgAlDjaUABuyDzEkQA+LHAUFFp6BtDwSGiYLsjiQQhSOFD2zP5FJQBChMDiABbe4ogo6BheuR2qauGccQmZ9PTiFISesO35GIXFnlIA6jzATYWBUzyoYDboZMAI03md8yVSADTGphZWNhUiTP48MQ3Q1QsIEMQhSpjlAAZhA5Ho4yBsPF5fNVNl55H8IlFYvFElAUvJ0uUMRlRg4PnUGs1WjNOt0SX1IpUHEw1jwEAA6fGeb7lWkMplfYhQADUUDaJ0wDJsAjWwOpNKadPpzgCkIA-PTvGzGa5Pt9wmKmJp6Jo9JIyEgoByyrgyBAAO7HXpzVXnDArNYQkreDWjfWGgBmPC6wHqjSanB6s3U5RUoNoLDYEE4AHIAGLIZAxq5iSTSLwqADMAA4ACwAJiuuYAnABWbNqKCaC7hyMcKAx+oYZNQVNSGScFQARgBmeLVz75au2fzecr1drrHrjcIAC8W23052u6XMwA2cc1jRu8iGr764h+5qB8kYEO4MMOCNT6MNgCKcAAHguJO2M33cwCrj3M6XN5Oo1jB8nxfNMOygFRi1zAB2fN-23ehjQwaVwVlEpyj8NDPEibBokqd1kBsekKDcbwAAMnWCKAABJaBhSFNDI11dVGJCVRqTwjxaL0fS4102I5LjvH3chD0JJoNSAA)

## Interface Hungarian Notation

Developers often bring conventions, patterns, and idioms from other languages they know. This can be good, as functional concepts like immutability, pure functions, and composition over inheritance work well in OO languages.

However, using naming conventions from one language in definitely not something to bring across. For example, C# interfaces starting with “I” are not idiomatic in TypeScript, but they are idiomatic C#. The point of a naming convention is to make code more readable and consistent.

## Conclusion

I’ve explained my preference and why I believe type should be the default choice in your projects. It’s up to you which you use, but I hope you can see the benefits of types and why they are a better choice in most cases.

The inevitable angry comments can be directed to `/dev/null`.

[^1]: The term “types” in TypeScript can refer to any object, be it a type alias or an interface. However, in the TypeScript ecosystem, the word “type” is typically usually used to specifically refer to the `type` keyword. This distinction is generally understood, even amongst pedants who are particular about precise language usage
[^2]: Angular being the opposite and the framework of choice for the “I don’t want to learn JavaScript/TypeScript” crowd.
