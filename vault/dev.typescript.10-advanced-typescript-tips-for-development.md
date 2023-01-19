---
id: iobm3jmimhpok244jve1s4r
title: 10 Advanced TypeScript Tips for Development
desc: ""
updated: 1674001801632
created: 1674000422536
---

> https://levelup.gitconnected.com/10-advanced-typescript-tips-for-development-2666298d50f

## 1. keyof

`keyof` is slightly similar to `Object.keys`, except that `keyof` takes the keys of the interface.

```ts
interface Point {
  x: number
  y: number
}
// type keys = "x" | "y"
type keys = keyof Point
```

Suppose we have an `object` as shown below and we need to implement a `get` function using typescript to get the value of its properties.

```ts
const data = {
  a: 3,
  hello: "max",
}
function get(o: object, name: string) {
  return o[name]
}
```

We might have written it that way at first, but it has many drawbacks:

1. Unable to confirm the return type: this will lose ts’ maximum type-checking capability
2. Unable to constrain the key: may commit a spelling error

In this case, you can use `keyof` to enhance the `type` function of the `get` function, for those who are interested, see the type tag of `_.get` and its implementation.

```ts
function get<T extends object, K extends keyof T>(o: T, name: K): T[K] {
  return o[name]
}
```

## 2. Required & Partial & Pick

Now that you know the `keyof`, you can use it to do some extensions to the properties, such as implementing `Partial` and `Pick`, `Pick` is generally used in `_.pick`

```ts
type Partial<T> = {
  [P in keyof T]?: T[P]
}

type Required<T> = {
  [P in keyof T]-?: T[P]
}

type Pick<T, K extends keyof T> = {
  [P in K]: T[P]
}

interface User {
  id: number
  age: number
  name: string
}

// Equivalent to: type PartialUser = { id?: number; age?: number; name?: string; }
type PartialUser = Partial<User>

// Equivalent to: type PickUser = { id: number; age: number; }
type PickUser = Pick<User, "id" | "age">
```

These types are built into Typescript.

## 3. Condition Type

It is similar to the ?: operator, you can use it to extend some basic types.

```ts
T extends U ? X : Y

type isTrue<T> = T extends true ? true : false
// Equivalent to type t = false
type t = isTrue<number>

// Equivalent to type t = false
type t1 = isTrue<false>
```

## 4. never & Exclude & Omit

the never type represents the type of values that never occur.

There are many interesting and useful types that can be introduced by combining `never` and `conditional` type, such as `Omit`

```ts
type Exclude<T, U> = T extends U ? never : T
// Equivalent to: type A = 'a'
type A = Exclude<"x" | "a", "x" | "y" | "z">
```

In combination with `Exclude`, we can introduce Omit’s writing style

```ts
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>

interface User {
  id: number
  age: number
  name: string
}

// Equivalent to: type PickUser = { age: number; name: string; }
type OmitUser = Omit<User, "id">
```

## 5. typeof

As the name implies, typeof represents a type that takes a certain value, and the following examples show their usage

```ts
const a: number = 3
// Equivalent to: const b: number = 4
const b: typeof a = 4
```

In a typical server-side project, we often need to stuff some tools into the `context`, such as config, logger, db models, utils, etc., and then use `typeof`.

```ts
import logger from "./logger"
import utils from "./utils"

interface Context extends KoaContect {
  logger: typeof logger
  utils: typeof utils
}

app.use((ctx: Context) => {
  ctx.logger.info("hello, world")

  // will return an error because this method is not exposed in logger.ts, which minimizes spelling errors
  ctx.loger.info("hello, world")
})
```

## 6. is

Before that, let’s look at a `koa` error handling process. Here is the process of centralizing the `error` handling and identifying the `code`

```ts
app.use(async (ctx, next) => {
  try {
    await next()
  } catch (err) {
    let code = "BAD_REQUEST"
    if (err.isAxiosError) {
      code = `Axios-${err.code}`
    } else if (err instanceof Sequelize.BaseError) {
    }
    ctx.body = {
      code,
    }
  }
})
```

At `err.code`, it will compile with an error that Property `‘code’` does not exist on type `‘Error’.ts(2339)`.  
In this case, you can use `as AxiosError` or `as any` to avoid the error, but forced type conversion is not friendly enough!

```ts
if ((err as AxiosError).isAxiosError) {
  code = `Axios-${(err as AxiosError).code}`
}
```

In this case, you can use is to determine the type of the value.

```ts
function isAxiosError(error: any): error is AxiosError {
  return error.isAxiosError
}

if (isAxiosError(err)) {
  code = `Axios-${err.code}`
}
```

In the GraphQL source code, there are many such uses to identify types.

```ts
export function isType(type: any): type is GraphQLType

export function isScalarType(type: any): type is GraphQLScalarType

export function isObjectType(type: any): type is GraphQLObjectType

export function isInterfaceType(type: any): type is GraphQLInterfaceType
```

## 7. interface & type

What is the difference between interface and type? You can refer [here](https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript).

The difference between interface and type is very small, for example, the following two ways of writing are similar.

```ts
interface A {
  a: number
  b: number
}

type B = {
  a: number
  b: number
}
```

The `interface` can be merged as follows, while the `type` can only be linked using the & class.

```ts
interface A {
  a: number
}

interface A {
  b: number
}

const a: A = {
  a: 3,
  b: 4,
}
```

## 8. Record & Dictionary & Many

These syntactic sugars are learned from the types source code of `lodash`, and are usually used quite frequently in the workplace.

```ts
type Record<K extends keyof any, T> = {
  [P in K]: T
}

interface Dictionary<T> {
  [index: string]: T
}

interface NumericDictionary<T> {
  [index: number]: T
}

const data: Dictionary<number> = {
  a: 3,
  b: 4,
}
```

## 9. Maintaining the const table with const enum

```ts
Use objects to maintain consts
const TODO_STATUS {
  TODO: 'TODO',
  DONE: 'DONE',
  DOING: 'DOING'
}

// Maintaining constants with const enum
const enum TODO_STATUS {
  TODO = 'TODO',
  DONE = 'DONE',
  DOING = 'DOING'
}

function todos (status: TODO_STATUS): Todo[];

todos(TODO_STATUS.TODO)
```

> [Stop SHOUTING = 'shouting'](https://swizec.com/blog/stop-shouting-shouting/)

## 10. VS Code Tips & Typescript Command

Sometimes with VS Code, the issues that arise when compiling with `tsc` do not match the issues prompted by vs code
Find the words `Typescript` in the bottom right corner of the project, the version number is shown on the right side, you can click on it and select `Use Workspace Version`, it means that it is always the same as the `typescript` version that the project depends on.

Or edit .`vs-code/settings.json`

```json
{
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

In short, TypeScript increases the readability and maintainability of code and makes our development more elegant.
