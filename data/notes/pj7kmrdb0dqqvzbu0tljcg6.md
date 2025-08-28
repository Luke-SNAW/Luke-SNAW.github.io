
> https://blog.bitsrc.io/functional-programming-oh-functors-5e670d8eeb8d

## What is a Functor?

A functor is just a

1. Wrapper over a value
2. That gives us a mapping interface
3. And obeys the functor’s laws (we’ll talk about them later)

## Examples on functors we use daily

1. `Array`
2. `Promise`

## Yes `Array` and `Promise` are functors, but how?

Let’s reflect on the functor definition…

**`Array` is a:**

1. Wrapper over a **list of items**
2. That gives us `**map**` **as a mapping interface**
3. And obeys the functor’s laws

Example:

```js
;[1, 2, 3] // the wrapped value
  .map(
    // the mapping interface
    (x) => x * 2
  )
```

**`Promise` is a:**

1. Wrapper over **any JS data type value**
2. That gives us `**then**` **as a mapping interface**
3. And obeys the functor’s laws

Example:

```js
const promise = new Promise((resolve, reject) => {
  resolve(
    { data: "Any JS type" } // the wrapped value
  )
})

promise.then(
  // the mapping interface
  (response) => console.log(response)
)
```

## What’s the relationship between the `Array` (and `Promise`) and the Functor?

A Functor is a design pattern, while `Array` and `Promise` are data types.

## Why am I telling you that `Array` and `Promise` are Functors?

To shutdown the fear of the idea of functors.

They are easy to understand, yet they have a powerful concept. And we use them daily without consciously knowing!

## Why to use functors?

Great question! Please follow along…

# A Problem

After talking a bit about functors and connecting them with our daily use, it’d be wise to dig deeper and build our own. In order to understand more the idea of a functor.

Let’s face a problem first…

Take a look at this piece of data

```js
{
  products: [
    {
      name: "building stuff",
      type: "book",
      price: 22,
      discount: 20,
    },
  ]
}
```

## Our task

To find the final price of the first product with discount. While if for any reason we encounter bad data, the fallback should be `"Nothing”` as string.

## Algorithmic steps

1. Find first discounted product
2. Apply discount
3. Keep checking for data invalidity. Where if data is invalid for any reason, we return `“Nothing”` as a fallback

## First try (the traditional way)

```js
const isProductWithDiscount = (product) => !isNaN(product.discount)
const findFirstDiscounted = (products) => products.find(isProductWithDiscount)
const calcPriceAfterDiscount = (product) => product.price - product.discount

const findFinalPrice = (data, fallbackValue) => {
  if (!data || !data.products) return fallbackValue

  const discountedProd = findFirstDiscounted(data.products)
  if (!discountedProd) return fallbackValue

  return calcPriceAfterDiscount(discountedProd)
}

findFinalPrice(data, "Nothing") // 2
```

## Notes on our first try

**The good things:**

1. Granular logical units (`isProductWithDiscount`, `findFirstDiscounted` and `calcPriceAfterDiscount`)
2. We defended our logic against data invalidity

**Things we can improve:**

1. We’re defending too much. ([Defensive programming](https://en.wikipedia.org/wiki/Defensive_programming) is a must in any resilient software, but too much is too much. In our code, 50% of `findFinalPrice` function’s body is checking for data invalidity, which is considered too much defence)
2. `fallbackValue` is almost everywhere

**Why are we concerned about these improvements?** Because they are mentally consuming maintainers. Thus directly impacting DX (_Developer Experience_) negatively.

## So there’s still room for improvements, right?

Let’s analyse the code and try to come up with a solution…

**Code structure analysis:** The parts we aim to improve are forming a pattern (defence and fallback) and they are actually intact and atomic! And that’s good!

**Solution _(Taking in mind analysis above)_:** We should be able to abstract that pattern into a wrapper that could handle these corner cases for us.

**Result:** The wrapper will take care of the corner cases. While we’ll only have to take care of the business logic!

If we’re able to implement this, that’d be great indeed!

# The `Maybe` Functor

> Reminder: A functor is just a wrapper over a value and gives us a mapping interface (i.e. `_map_`) and obeys some laws.

As we discussed earlier. We only want a wrapper that abstracts away handling data (either bad or good).

So, the role of `Maybe` functor, is to wrap our data (potentially bad data), and handle the corner cases for us. How is that? Follow along…

`**Maybe**` **Functor Implementation**

```js
function Maybe(value) {
  const isNothing = () => value === null || value === undefined
  const map = (fn) => (isNothing() ? Maybe() : Maybe(fn(value)))
  const getValueOrFallback = (fallbackValue) =>
    isNothing() ? fallbackValue : value

  return {
    map,
    getValueOrFallback,
  }
}
```

**Implementation explanation:**

1. `isNothing`: checks if the wrapped value in `Maybe` functor is invalid.
2. `map`: the mapping interface to our value wrapper, where we use this to apply our business logic lambdas to the wrapped value. _(Note: that_ `_map_` _returns new value in another_ `_Maybe_` _instance, so we can keep doing_ `_.map().map().map…_`_)_
3. `getValueOrFallback`: returns the wrapped value or fallbacks to `fallbackValue`.

**Let’s use** `**Maybe**`**:**

- **With good data:**

```js
Maybe("Ahmad")
  .map((x) => x.substring(1))
  .getValueOrFallback("fallback") // 'hmad'
```

- **With bad data:**

```js
Maybe(null)
  .map((x) => x.substring(1)) // will not be executed
  .getValueOrFallback("fallback") // 'fallback'
```

Sounds good so far! `Maybe` functor cared for the corner cases for us! And “aborted” execution when data was invalid. While we only cared for business logic!

It looks like we achieved our goal! Let’s put it to work…

## Solving the previous problem using `Maybe` functor

Ok, let’s try to solve the products problem using `Maybe` functor

```js
const isProductWithDiscount = (product) => !isNaN(product.discount)
const findFirstDiscounted = (products) => products.find(isProductWithDiscount)
const calcPriceAfterDiscount = (product) => product.price - product.discount

Maybe(data)
  .map((x) => x.products)
  .map(findFirstDiscounted)
  .map(calcPriceAfterDiscount)
  .getValueOrFallback("Nothing") // 2
```

**We were able to improve the previous code using** `**Maybe**` **functor, where**

1. We no more defend the code ourselves, but the `Maybe` functor does that for us.
2. We configured the `fallbackValue` only once.

## Reflecting `Maybe` functor on functor’s definition

`Maybe` functor is just a

1. Wrapper over **any JS data type value**
2. That gives us `**map**` **as a mapping interface**
3. And obeys the functor’s laws

# Functors Laws

- **Identity law**

When performing the mapping operation, if the values in the functor are mapped to themselves, the result will be an unmodified functor.

Example:

```js
const w1 = Maybe(value)
const w2 = Maybe(value).map((v) => v)
// w1 and w2 are equivalent
```

- **Composition**

If two sequential mapping operations are performed one after the other using two functions, the result should be the same as a single mapping operation with one function that is equivalent to applying the first function to the result of the second.

Example:

```js
const w1 = Maybe(value).map((v) => f(g(v)))
const w2 = Maybe(value)
  .map((v) => g(v))
  .map((v) => f(v))
// w1 and w2 are equivalent
```

# Why To Use Functors?

1. \*\*Abstraction of function application
2. Empowering [functional composition](https://blog.bitsrc.io/functional-programming-composition-2e9b863d8bcb)
3. Reducing amount of defensive code (in case if we used `Maybe` functor)
4. Cleaner code structure (Did you notice how linear the logic is now? Amazing!)
5. Variables are more explicit about what we expect (That `Maybe` _models a value that may or may not be present. That it models a “value” or “nothing”_)

## **\*\*What do we mean by “Abstraction of function application”?**

That we pass a transformer function (i.e. `x => x.products`) to the mapping interface (i.e. `map`) of the wrapper (i.e. `Maybe`) and it knows how to take care of itself (by its internal implementation).

We don’t care about the wrapper’s implementation details it has inside (implementation details are hidden), and yet we know how to use the wrapper (`Array` or `Promise`) by using their mapping interfaces.

And that’s actually crucially important in the programming world. Where that lowers the bar on how much we -as programmers- need to understand in order to be able to get stuff done. They can be implemented in any language that supports higher-order functions (which is most of them these days). And that creates a language-agnostic vocabulary.

# Why Don’t We See More Functors In Our Codebases?

Simply, because we’re not used to. Before `.map` (and `.then`) we were used to mutate arrays or loop through them manually. But once we discovered `.map` we started adapting it as the new transformation tool! I hope after understanding the value of functors, we start introducing them more into our daily coding routines as a very usual thing!

# Quick Note

`Maybe` functor is just an example on functors. It’s not the only functor we have, there are more functors out there and for different purposes. We talked about the simplest here (The `Maybe` functor), so we can get a bit closer to the idea of functors!

# Conclusion

Functor design pattern is a simple — yet very powerful pattern. We use it daily in different data types without knowing. Hopefully, we can recognise and appreciate functors a bit more and give them more space in our codebase, because they’ll clean code and give us more power; Due to the composability nature they have and abstractions they offer.

At the end, a functor is just a wrapper over a value that gives us a mapping interface, and obeys some laws.

_Thanks a lot for taking time reading through this article_ ❤️ _I’m cooking the next ones in the series. Please let me know what you think in the comments about this article or the series._

# This is an article in a series of articles talking about Functional Programming

In this series of articles we cover the main concepts of Functional Programming. At the end of the series, you’ll be able to tackle problems in a more functional approach.

# This series discusses:

0. [A Brief Comparison Between Programming Paradigms](https://blog.bitsrc.io/functional-programming-part-0-a-brief-comparison-between-programming-paradigms-3ff192cd32b6)

1. [First Class functions](https://blog.bitsrc.io/functional-programming-part-1-first-class-functions-791103984dfb)
2. [Pure functions](https://blog.bitsrc.io/functional-programming-part-2-pure-functions-85491f3d7190)
3. [Currying](https://blog.bitsrc.io/functional-programming-part-3-the-powers-of-currying-213eb69b234b)
4. [Composition](https://blog.bitsrc.io/functional-programming-composition-2e9b863d8bcb)
5. _Functors (this article)_
6. Monads
