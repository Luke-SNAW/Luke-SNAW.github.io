
> https://javascript.plainenglish.io/no-more-confusion-about-typescripts-type-and-interface-63c39418ae35

Type aliases are extended by `&`, while interfaces are extended by `extends`.

So can an interface extend the type defined by the type alias through extends? The answer is yes. Additionally, type aliases can also extend defined interface types via the **&** operator.

# Differences

1. Type aliases can define aliases for primitive types, union types, or tuple types, while interfaces cannot:

```ts
type MyNumber = number; // primitive type
type StringOrNumber = string | number; // union type
type Point = [number, number]; // tuple type
```

2. Interfaces with the same name are automatically merged(Declaration Merging), while type aliases are not:

**When to use `type`**

1. When defining aliases for primitive types, use `type`
2. When defining a tuple type, use `type`
3. When defining a function type, use `type`
4. When defining union types, use `type`
5. When defining the mapped types, use `type`

**When to use `interface`**

1. When you need to take advantage of the declaration merging feature, use `interface`
2. When defining an object type and no need to use type, use `interface`
