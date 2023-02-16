---
id: acvfwko2zkttghtfvatxr5b
title: Use Maps More and Objects Less
desc: ""
updated: 1676505575435
created: 1676504920562
---

> https://www.builder.io/blog/maps

Objects in JavaScript are awesome. They can do anything! Literally…anything.

But, like all things, just because you _can_ do something, doesn’t (necessarily) mean you _should._

```typescript
// 🚩
const mapOfThings = {}

mapOfThings[myThing.id] = myThing

delete mapOfThings[myThing.id]
```

For instance, if you're using objects in JavaScript to store arbitrary key value pairs where you'll be adding and removing keys frequently, you should really consider using a `map` instead of a plain object.

```typescript
// ✅
const mapOfThings = new Map()

mapOfThings.set(myThing.id, myThing)

mapOfThings.delete(myThing.id)
```

### Performance issues with objects

Whereas with objects, where the delete operator is notorious for poor performance, maps are optimized for this exact use case and in some cases can be seriously faster.

[Benchmark result (from the below link) showing Maps about 5x faster in this benchmark compared to Objects](https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2Fdefb300b5ebe42108d9ab813d3b99b5f?width=705)

Note of course this is just one [example benchmark](https://perf.builder.io/?q=eyJpZCI6IndkbG1kbG94cm5nIiwidGl0bGUiOiJNYXAgdnMgT2JqZWN0IFBlcmZvcm1hbmNlIiwiYmVmb3JlIjoiY29uc3QgcmFuZG9tS2V5ID0gKCkgPT4gTWF0aC5mbG9vcihNYXRoLnJhbmRvbSgpICogMTAwMDAwMDApXG5jb25zdCBkYXRhID0gWy4uLkFycmF5KDEwMDAwKV0ubWFwKHJhbmRvbUtleSlcbmNvbnN0IG9iaiA9IE9iamVjdC5mcm9tRW50cmllcyhkYXRhLm1hcCh4ID0%2BIFt4LCB4XSkpXG5jb25zdCBtYXAgPSBuZXcgTWFwKE9iamVjdC5lbnRyaWVzKG9iaikpIiwidGVzdHMiOlt7Im5hbWUiOiJNYXAiLCJjb2RlIjoiLy8gRnJlZXplIHRoZSBrZXlzIGxpc3QgKHdlIGRvbid0IHdhbnQgdG8gbXV0YXRlIHdoaWxlIGl0ZXJhdGluZylcbmNvbnN0IGtleXMgPSBBcnJheS5mcm9tKG1hcC5rZXlzKCkpXG5mb3IgKGNvbnN0IGtleSBvZiBrZXlzKSB7XG4gIC8vIERlbGV0ZSBrZXlcbiAgbWFwLmRlbGV0ZShrZXkpXG4gIC8vIENyZWF0ZSBhIHJhbmRvbSBuZXcga2V5XG4gIGNvbnN0IG5ld0tleSA9IHJhbmRvbUtleSgpXG4gIG1hcC5zZXQobmV3S2V5LCBuZXdLZXkpXG59IiwicnVucyI6W10sIm9wcyI6OTAxfSx7Im5hbWUiOiJPYmplY3QiLCJjb2RlIjoiY29uc3Qga2V5cyA9IE9iamVjdC5rZXlzKG9iailcbmZvciAoY29uc3Qga2V5IG9mIGtleXMpIHtcbiAgLy8gRGVsZXRlIGtleVxuICBkZWxldGUgb2JqW2tleV1cbiAgLy8gQ3JlYXRlIGEgcmFuZG9tIG5ldyBrZXlcbiAgY29uc3QgbmV3S2V5ID0gcmFuZG9tS2V5KClcbiAgb2JqW25ld0tleV0gPSBuZXdLZXlcbn0iLCJydW5zIjpbXSwib3BzIjoxODN9XSwidXBkYXRlZCI6IjIwMjMtMDItMDlUMDc6MDk6MzQuMjY2WiJ9) (run with Chrome v109 on a Core i7 MBP). You can also compare [another benchmark](https://www.notion.so/Use-Maps-more-and-Objects-less-Outline-6f3e4c17e18543908ddde250ad9d2315) created by [Zhenghao He](https://www.zhenghao.io/posts/object-vs-map#performance-extravaganza). Just keep in mind — micro benchmarks like this are [notoriously imperfect](https://mrale.ph/blog/2012/12/15/microbenchmarks-fairy-tale.html) so take them with a grain of salt.

That said, you don’t need to trust my or anyone else’s benchmarks, as [MDN itself clarifies that maps are specifically optimized for this use case](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps) of frequently adding and removing keys, as compared with an object that is not as optimized for this use case:

[Screenshot of the MDN docs pointing to Maps being mentioned to have better performance than Objects for scenarios that involve frequent additions and removals of key-value pairs](https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F0d08535f5d2e4c5bbefe257c58103d25?width=705)

If you are curious why, it has to do with how JavaScript VMs optimize JS objects by assuming their [shape](https://mathiasbynens.be/notes/shapes-ics), whereas a map is purpose-built for the use case of a hashmap where keys are dynamic and ever-changing.

Read more about how VMs assume shapes in this thread by Miško (CTO of [Builder.io](https://www.builder.io/), and creator of Angular and [Qwik](https://qwik.builder.io/)):

Another great article is [What’s up with monomorphism](https://mrale.ph/blog/2015/01/11/whats-up-with-monomorphism.html), which explains the performance characteristics of objects in JavaScript, and why they are not as optimized for hashmap-like use cases of frequently adding and removing keys.

![Understanding monomorphism can improve your JavaScript performance 60x.](https://pbs.twimg.com/media/FoRGcweaQAQjB1g.png)

But beyond performance, maps also solve for several issues that exist with objects.

### Built-in keys problem

One major issue of objects for hashmap-like use cases is that objects are polluted with tons of keys built into them already. _WHAT?_

```typescript
const myMap = {}

myMap.valueOf // => [Function: valueOf]
myMap.toString // => [Function: toString]
myMap.hasOwnProperty // => [Function: hasOwnProperty]
myMap.isPrototypeOf // => [Function: isPrototypeOf]
myMap.propertyIsEnumerable // => [Function: propertyIsEnumerable]
myMap.toLocaleString // => [Function: toLocaleString]
myMap.constructor // => [Function: Object]
```

So if you try and access any of these properties, each of them has values already even though this object is supposed to be empty.

This alone should be a clear reason not to use an object for an arbitrary-keyed hashmap, as it can lead to some really hairy bugs you’ll only discover later.

### Iteration awkwardness

Speaking of strange ways that JavaScript objects treat keys, iterating through objects is riddled with gotchas.

For instance, you may already know not to do this:

```typescript
for (const key in myObject) {
  // 🚩 You may stumble upon some inherited keys you didn't mean to
}
```

And you may have been told instead to do this:

```typescript
for (const key in myObject) {
  if (myObject.hasOwnProperty(key)) {
    // 🚩
  }
}
```

But this is still problematic, as `myObject.hasOwnProperty` can easily be overridden with any other value. Nothing is preventing anyone from doing `myObject.hasOwnProperty = () => explode()`.

So instead you should really do this funky mess:

```typescript
for (const key in myObject) {
  if (Object.prototype.hasOwnProperty.call(myObject, key) {
    // 😕
  }
}
```

Or if you prefer your code to not look like a mess, you can use the more recently added [`Object.hasOwn`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwn):

```typescript
for (const key in myObject) {
  if (Object.hasOwn(myObject, key) {
    // 😐
  }
}
```

Or you can give up on a `for` loop entirely and just use `Object.keys` with `forEach`.

```typescript
Object.keys(myObject).forEach((key) => {
  // 😬
})
```

However, with maps, there are no such issues at all. You can use a standard `for` loop, with a standard iterator, and a really nice destructuring pattern to get both the `key` and `value` at once:

```typescript
for (const [key, value] of myMap) {
  // 😍
}
```

_Me gusta._

In fact, this is so nice, we now have an [`Object.entries`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) method to do similar with objects. It's one additional step so doesn't feel quite so first-class, but hey it works.

```typescript
for (const [key, value] of Object.entries(myObject)) {
  // 🙂
}
```

Add that one to the long list of "loops in objects are ugly so choose one of the following 5 options you prefer".

But for Maps, it's nice to know there is one simple and elegant way to iterate built in directly.

Additionally, you can iterate over just keys or values as well:

```typescript
for (const value of myMap.values()) {
  // 🙂
}

for (const key of myMap.keys()) {
  // 🙂
}
```

### Key ordering

One additional perk of maps is they preserve the order of their keys. This has been a long asked for quality of objects, and now exists for maps.

This gives us another very cool feature, which is that we can destructure keys directly from a map, in their exact order:

```typescript
const [[firstKey, firstValue]] = myMap
```

This can also open up some interesting use cases, like trivially implementing an O(1) LRU Cache:

> One cool use case for Maps - creating a simple O(1) LRU cache
>
> Given how Maps preserve the order of their keys, implementation is trivial:  
> [https://t.co/HkMyzL03o0](https://t.co/HkMyzL03o0)

### Copying

Now you might say, _oh, well, objects have some advantages, like they're very easy to copy_, for instance, using an object spread or assign.

```typescript
const copied = { ...myObject }
const copied = Object.assign({}, myObject)
```

But it turns out that maps are just as easy to copy:

```typescript
const copied = new Map(myMap)
```

The reason this works is because the constructor of `Map` takes an iterable of `[key, value]` tuples. And conveniently, maps are iterable, producing tuples of their keys and values. Nice.

Similarly, you can also do deep copies of maps, just like you can with objects, using [structuredClone](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone):

```typescript
const deepCopy = structuredClone(myMap)
```

### Converting maps to objects and objects to maps

Converting maps to objects is readily done using [Object.fromEntries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries):

```typescript
const myObj = Object.fromEntries(myMap)
```

And going the other way is straightforward as well, using [Object.entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries):

```typescript
const myMap = new Map(Object.entries(myObj))
```

Easy!

And, now that we know this, we no longer have to construct maps using tuples:

```typescript
const myMap = new Map([
  ["key", "value"],
  ["keyTwo", "valueTwo"],
])
```

You can instead construct them like objects, which to me is a bit nicer on the eyes:

```typescript
const myMap = new Map(
  Object.entries({
    key: "value",
    keyTwo: "valueTwo",
  })
)
```

Or you could make a handy little helper too:

```typescript
const makeMap = (obj) => new Map(Object.entries(obj))

const myMap = makeMap({ key: "value" })
```

Or with TypeScript:

```typescript
const makeMap = <V = unknown>(obj: Record<string, V>) =>
  new Map<string, V>(Object.entries(obj))

const myMap = makeMap({ key: "value" })
// => Map<string, string>
```

I’m a fan of that.

### Key types

Maps are not just a more ergonomic and better-performing way to handle key value maps in JavaScript. They can even do things that you just cannot accomplish at all with plain objects.

For instance, maps are not limited to only having strings as keys — you can use any type of object as a key for a map. And I mean, like, anything.

```typescript
myMap.set({}, value)
myMap.set([], value)
myMap.set(document.body, value)
myMap.set(function () {}, value)
myMap.set(myDog, value)
```

But, why?

One helpful use case for this is associating metadata with an object without having to modify that object directly.

```typescript
const metadata = new Map()

metadata.set(myDomNode, {
  internalId: "...",
})

metadata.get(myDomNode)
// => { internalId: '...' }
```

This can be useful, for instance, when you want to associate temporary state to objects you read and write from a database. You can add as much temporary data associated directly with the object reference, without risk.

```typescript
const metadata = new Map()

metadata.set(myTodo, {
  focused: true,
})

metadata.get(myTodo)
// => { focused: true }
```

Now when we save `myTodo` back to the database, only the values we want saved are there, and our temporary state (which is in a separate map) does not get included accidentally.

This does have one issue though.

Normally, the garbage collector would collect this object and remove it from memory. However, because our map is holding a reference, it'll never be garbage collected, causing a memory leak.

### WeakMaps

Here’s where we can use the `WeakMap` type. Weak maps perfectly solve for the above memory leak as they hold a weak reference to the object.

So if all other references are removed, the object will automatically be garbage collected and removed from this weak map.

```typescript
const metadata = new WeakMap()

// ✅ No memory leak, myTodo will be removed from the map
// automatically when there are no other references
metadata.set(myTodo, {
  focused: true,
})
```

### Moar map stuff

A few remaining useful things to know about Maps before we continue on:

```typescript
map.clear() // Clear a map entirely
map.size // Get the size of the map
map.keys() // Iterator of all map keys
map.values() // Iterator of all map values
```

Ok, you get it, maps have nice methods. Moving on.

### Sets

If we are talking about maps, we should also mention their cousin, Sets, which give us a better-performing way to create a _unique_ list of elements where we can easily add, remove, and look up if a set contains an item:

```typescript
const set = new Set([1, 2, 3])

set.add(3)
set.delete(4)
set.has(5)
```

In some cases, sets can [yield significantly better performance](https://perf.builder.io/?q=eyJpZCI6IjZtaDFsdjJscm56IiwidGl0bGUiOiJBcnJheSB2cyBTZXQgcGVyZm9ybWFuY2UiLCJiZWZvcmUiOiJjb25zdCBsZW5ndGggPSAxMF8wMDBcbmNvbnN0IGFyciA9IFsuLi5BcnJheShsZW5ndGgpLmtleXMoKV0ubWFwKHggPT4gKHggKiAxNikudG9TdHJpbmcoMzYpKVxuY29uc3Qgc2V0ID0gbmV3IFNldChhcnIpIiwidGVzdHMiOlt7Im5hbWUiOiJBcnJheSIsImNvZGUiOiJjb25zdCByYW5kb21WYWx1ZSA9IChNYXRoLmZsb29yKE1hdGgucmFuZG9tKCkgKiBsZW5ndGgpICogMTYpLnRvU3RyaW5nKDM2KVxuXG4vLyBGaW5kIHRoZSB2YWx1ZVxuYXJyLmluY2x1ZGVzKHJhbmRvbVZhbHVlKVxuXG4vLyBSZW1vdmUgdGhlIHZhbHVlXG5hcnIuc3BsaWNlKGFyci5pbmRleE9mKHJhbmRvbVZhbHVlKSwgMSlcblxuLy8gQWRkIGl0IGJhY2tcbmFyci5wdXNoKHJhbmRvbVZhbHVlKSIsInJ1bnMiOltdLCJvcHMiOjEwNDQwfSx7Im5hbWUiOiJTZXQiLCJjb2RlIjoiY29uc3QgcmFuZG9tVmFsdWUgPSAoTWF0aC5mbG9vcihNYXRoLnJhbmRvbSgpICogbGVuZ3RoKSAqIDE2KS50b1N0cmluZygzNilcblxuLy8gRmluZCB0aGUgdmFsdWVcbnNldC5oYXMocmFuZG9tVmFsdWUpXG5cbi8vIFJlbW92ZSB0aGUgdmFsdWVcbnNldC5kZWxldGUocmFuZG9tVmFsdWUpXG5cbi8vIEFkZCBpdCBiYWNrXG5zZXQuYWRkKHJhbmRvbVZhbHVlKSIsInJ1bnMiOltdLCJvcHMiOjc4MTMxNn1dLCJ1cGRhdGVkIjoiMjAyMy0wMi0wN1QxMDoxOTozMi4wNjVaIn0%3D) than the equivalent operations with an array.

[Screenshot of the Array vs Set benchmark with Sets having almost 100x better performance](https://cdn.builder.io/api/v1/image/assets%2FYJIGb4i01jvw0SRdL5Bt%2F7034341cab394484b2e80ea3829b1acb?width=705)

_Blah blah microbenchmarks are not perfect, test your own code under real-world conditions to verify you get a benefit, or_ [_don't just take my word for it_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set#performance).

Similarly, we get a `WeakSet` class in JavaScript that will help us avoid memory leaks as well.

```typescript
// No memory leaks here, captain 🫡
const checkedTodos = new WeakSet([todo1, todo2, todo3])
```

### [Serialization](https://www.builder.io/blog/maps#serialization)

Now you might say there's one last advantage that plain objects and arrays have over maps and sets — serialization.

_Ha! You thought you got me on that one. But I’ve got answers for you, friend._

So, yes, `JSON.stringify()`/ `JSON.parse()` support for objects and maps is extremely handy.

But, have you ever noticed that when you want to pretty print JSON you always have to add a `null` as the second argument? Do you know what that parameter even does?

```typescript
JSON.stringify(obj, null, 2)
//                  ^^^^ what dis do
```

As it turns out, that parameter can be very helpful to us. It is called a _replacer_ and it allows us to define how any custom type should be serialized.

We can use this to easily convert maps and sets to objects and arrays for serialization:

```typescript
JSON.stringify(obj, (key, value) => {
  // Convert maps to plain objects
  if (value instanceof Map) {
    return Object.fromEntries(value)
  }
  // Convert sets to arrays
  if (value instanceof Set) {
    return Array.from(value)
  }
  return value
})
```

> Why did the JavaScript developer quit their job? They didn’t get _arrays_. Ha ha ho ho. Ok.

Now we can just abstract this into a basic reusable function, and serialize away.

```typescript
const test = { set: new Set([1, 2, 3]), map: new Map([["key", "value"]]) }

JSON.stringify(test, replacer)
// => { set: [1, 2, 3], map: { key: value } }
```

For converting back, we can use the same trick with `JSON.parse()`, but doing the opposite, by using its _reviver_ parameter, to convert arrays back to Sets and objects back to maps when parsing:

```typescript
JSON.parse(string, (key, value) => {
  if (Array.isArray(value)) {
    return new Set(value)
  }
  if (value && typeof value === "object") {
    return new Map(Object.entries(value))
  }
  return value
})
```

Also note that both _replacers_ and _revivers_ work recursively, so they are able to serialize and deserialize maps and sets _anywhere_ in our JSON tree.

But, there is just one small problem with our above serialization implementation.

We currently don’t differentiate a plain object or array versus a map or a set at parse time, so we cannot intermix plain objects and maps in our JSON or we will end up with this:

```typescript
const obj = { hello: "world" }
const str = JSON.stringify(obj, replacer)
const parsed = JSON.parse(obj, reviver)
// Map<string, string>
```

We can solve this by creating a special property; for example, called `__type`, to denote when something should be a map or a set as opposed to a plain object or array, like so:

```typescript
function replacer(key, value) {
  if (value instanceof Map) {
    return { __type: "Map", value: Object.fromEntries(value) }
  }
  if (value instanceof Set) {
    return { __type: "Set", value: Array.from(value) }
  }
  return value
}

function reviver(key, value) {
  if (value?.__type === "Set") {
    return new Set(value.value)
  }
  if (value?.__type === "Map") {
    return new Map(Object.entries(value.value))
  }
  return value
}

const obj = { set: new Set([1, 2]), map: new Map([["key", "value"]]) }
const str = JSON.stringify(obj, replacer)
const newObj = JSON.parse(str, reviver)
// { set: new Set([1, 2]), map: new Map([['key', 'value']]) }
```

Now we have full JSON serialization and deserialization support for sets and maps. Neat.

### [When you should use what](https://www.builder.io/blog/maps#when-you-should-use-what)

For structured objects that have a well-defined set of keys — such as if every `event` should have a title and a date — you generally want an object.

```typescript
// For structured objects, use Object
const event = {
  title: "Builder.io Conf",
  date: new Date(),
}
```

They're very optimized for fast reads and writes when you have a fixed set of keys.

When you can have any number of keys, and you may need to add and remove keys frequently, consider using `map` for better performance and ergonomics.

```typescript
// For dynamic hashmaps, use Map
const eventsMap = new Map()
eventsMap.set(event.id, event)
eventsMap.delete(event.id)
```

When creating an array where the order of elements matter and you may intentionally want duplicates in the array, then a plain array is generally a great idea.

```typescript
// For ordered lists, or those that may need duplicate items, use Array
const myArray = [1, 2, 3, 2, 1]
```

But when you know you never want duplicates and the order of items doesn't matter, consider using a set.

```typescript
// For unordered unique lists, use Set
const set = new Set([1, 2, 3])
```

## [About me](https://www.builder.io/blog/maps#about-me)

Hi! I'm [Steve](https://twitter.com/Steve8708?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor), CEO of [Builder.io](https://www.builder.io/).

We make a way to drag + drop with your components to create pages and other CMS content on your site or app, [visually](https://www.builder.io/blog/headless-cms-workflow).

You may find it interesting or useful:
