
> https://blog.bitsrc.io/typescript-advanced-types-for-next-js-examples-and-best-practices-in-2023-a3a3946a353e

## Deep Partial

Sometimes, you may want to make only some properties of an object optional, without affecting the type of the object itself. You can create a DeepPartial utility that makes all properties of an object and nested objects optional. This can be useful when working with complex data models.

```ts
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P]
}
```

## How to Use Deep Partial

Here’s an example of how you could use DeepPartial in a Next.js project:

```ts
interface User {
  name: string
  address: {
    street: string
    city: string
  }
}

type DeepPartialUser = DeepPartial<User>

// The DeepPartialUser type is equivalent to:
interface PartialUser {
  name?: string
  address?: {
    street?: string
    city?: string
  }
}

const user: DeepPartialUser = {
  address: {
    street: "123 Main St.",
  },
}
```

## Optional Props

You can create an OptionalProps utility that makes some properties of a component’s props optional, while keeping the rest of the properties required. This can be useful when you have a large props interface with some optional and some required properties.

```ts
type OptionalProps<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>
```

## How to Use Optional Props

Here’s an example of how you could use OptionalProps in a Next.js project:

```ts
interface ButtonProps {
  text: string
  onClick: () => void
  disabled: boolean
  size: "small" | "medium" | "large"
}

type OptionalButtonProps = OptionalProps<ButtonProps, "size" | "disabled">

// The OptionalButtonProps type is equivalent to:
interface ButtonPropsOptional {
  text: string
  onClick: () => void
  size?: "small" | "medium" | "large"
  disabled?: boolean
}

function Button(props: OptionalButtonProps) {
  // ...
}

;<Button text="Click me" onClick={() => console.log("Button clicked")} />
```

## Merge Types

Sometimes, you may want to merge two or more types together to create a new type. You can create a MergeTypes utility that takes multiple types as arguments and returns a new type that merges all the properties of the input types.

type MergeTypes<T extends object[]> = T[number];

## How to Use Merge Types

Here’s an example of how you could use MergeTypes in a Next.js project:

```ts
interface User {
  name: string
  email: string
}

interface Address {
  street: string
  city: string
}

type UserInfo = MergeTypes<[User, Address]>

// The UserInfo type is equivalent to:
interface UserInfoMerged {
  name: string
  email: string
  street: string
  city: string
}

const user: UserInfo = {
  name: "John Doe",
  email: "john.doe@example.com",
  street: "123 Main St.",
  city: "New York",
}
```

## Promise Type

You can create a PromiseType utility that extracts the resolved type of a Promise. This can be useful when working with asynchronous code that returns promises.

```ts
type PromiseType<T extends Promise<any>> = T extends Promise<infer U>
  ? U
  : never
```

## How to Use Promise Type

Here’s an example of how you could use PromiseType in a Next.js project:

```ts
async function fetchUserData(): Promise<User> {
  // fetch user data from API
}

type UserPromise = PromiseType<typeof fetchUserData>

// The UserPromise type is equivalent to:
interface User {
  name: string
  email: string
  // ...
}

async function getUser(): Promise<UserPromise> {
  const user = await fetchUserData()
  return user
}
```

## Readonly Props

You can create a ReadonlyProps utility that makes all properties of a component’s props readonly. This can be useful when you want to prevent the props from being modified by the component.

```ts
type ReadonlyProps<T> = { readonly [P in keyof T]: T[P] }
```

## How to Use Readonly Props

Here’s an example of how you could use ReadonlyProps in a Next.js project:

```ts
interface ButtonProps {
  readonly text: string
  readonly onClick: () => void
}

function Button(props: ReadonlyProps<ButtonProps>) {
  // ...
}

;<Button text="Click me" onClick={() => console.log("Button clicked")} />
// This would be a compile-time error:
// <Button text="Click me" onClick={() => console.log("Button clicked")} />
// ^-- error: Cannot assign to 'text' because it is a read-only property.
```
