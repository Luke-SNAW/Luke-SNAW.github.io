
> https://dmitripavlutin.com/typescript-record/

The usual way to define a type of an object in TypeScript is using an object type:

```ts
interface SalaryInterface {
  annual: number
  bonus: number
}

const salary: SalaryInterface = { annual: 56000, bonus: 1200 } // OK
```

or an [index signature](https://dmitripavlutin.com/typescript-index-signatures/):

```ts
type NumericObject = {
  [key: string]: number
}

const salary: NumericObject = { annual: 56000, bonus: 1200 } // OK
```

These are good ways to define object types.

But `Record<K, V>`, the third approach, has the benefit of being shorter and more readable. Let's see how to use it in your code.

### Table of Contents

- [1. Record type](https://dmitripavlutin.com/typescript-record/#1-record-type)
- [2. Record with union key](https://dmitripavlutin.com/typescript-record/#2-record-with-union-key)
- [3. Record benefits](https://dmitripavlutin.com/typescript-record/#3-record-benefits)
- [4. Conclusion](https://dmitripavlutin.com/typescript-record/#4-conclusion)

## 1. Record type

`Record<K, V>` is a [generic type](https://www.typescriptlang.org/docs/handbook/2/generics.html) that represents an object type which keys are `K` and values are `V`.

For example, `Record<string, number>` is an object type with string keys and number values:

```ts
type NumericRecord = Record<string, number>

const salary: NumericRecord = { annual: 56000, bonus: 1200 } // OK
```

`Record<string, number>` is permissive regarding the object structure, as long as the keys are strings and values are numbers:

```ts
type NumericRecord = Record<string, number>

const salary1: NumericRecord = { annual: 56000 } // OK
const salary2: NumericRecord = { monthly: 8000 } // OK
const salary3: NumericRecord = {} // OK
const salary4: NumericRecord = { foo: 0, bar: 1, baz: -2 } // OK
```

But `Record<string, number>` throws a type error if the value of a prop is a string:

```ts
type NumericRecord = Record<string, number>

const salary2: NumericRecord = { annual: "56K" } // Type error!
```

There are 2 simple rules to remember regarding the allowed types of the keys and values. In `Record<K, V>`:

- the key type `K` is restricted to `number`, `string`, `symbol`, including their [literals](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#literal-types)
- but there is no restriction on the value type `V`

Let's see some valid record types:

```ts
type T1 = Record<string, string> // OK
type T2 = Record<number, number> // OK
type T3 = Record<string, () => void> // OK
type T4 = Record<number | "key1", boolean> // OK
type T5 = Record<"key1" | "key2", boolean> // OK
type T6 = Record<string, Record<string, number>> // OK
type T7 = Record<string, { payment: number }> // OK
```

Types like `boolean`, `object`, `Function`, etc. are not accepted as keys:

```ts
type T1 = Record<boolean, number> // Type error!
type T2 = Record<object, number> // Type error!
```

## 2. Record with union key

As seen above, `Record<string, number>` permits any key names in the object. But quite often you need to annotate objects with a fixed set of keys.

The record type accepts a [union type](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types) as a key, which is useful to fixate the keys.

A [union of string literals](https://mariusschulz.com/blog/string-literal-types-in-typescript#string-literal-types-and-union-types) is a common way to define the key type:

```ts
type Keys = "key1" | "key2" | "keyN"
```

For example, `Record<'annual' | 'bonus', number>` represents an object which can have only `annual` and `bonus` keys:

```ts
type Salary = Record<"annual" | "bonus", number>

const salary1: Salary = { annual: 56000, bonus: 1200 } // OK
```

Using less than necessary or keys than aren't in the union is prohibited:

```ts
type Salary = Record<"annual" | "bonus", number>

const salary1: Salary = { annual: 56000 } // Type error!
const salary2: Salary = { bonus: 1200 } // Type error!
const salary3: Salary = {} // Type error!
const salary4: Salary = { monthly: 8000 } // Type error!
```

The record type with union keys is equivalent to the regular object type. The record type has the benefit of not repeating the value type (like the regular object does):

```ts
type Salary = Record<"annual" | "bonus", number>

// is equivalent to

type SalaryObj = {
  annual: number
  bonus: number
}
```

## 3. Record benefits

I prefer record type instead of index signature most of the time. Record syntax is shorter and more readable (altought it's also a matter of taste).

For example, the record parameter is a bit easier to grasp than the index signature parameter:

```ts
function logSalary1(salary: Record<string, number>) {
  console.log(salary)
}

function logSalary2(salary: { [key: string]: number }) {
  console.log(salary)
}
```

Compared to record type, the index signature doesn't accept literals or a union as key type:

```ts
type Salary = {
  [key: "annual" | "bonus"]: number // Type error!
}
```

## 4. Conclusion

`Record<K, V>` is an object type with key type `K` and value type `V`.

The key type `K` can be only `number`, `string`, or `symbol`, including their literals. On the value type `V` is no restriction.

To limit the keys to a specific set, you can use a union of string literals `Record<'key1' | 'key2', V>` as the key type.

Check also my post [index signatures](https://dmitripavlutin.com/typescript-index-signatures/) to learning more about object types.
