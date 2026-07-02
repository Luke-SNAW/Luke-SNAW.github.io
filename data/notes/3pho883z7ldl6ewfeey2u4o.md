
> https://jrsinclair.com/articles/2022/why-would-anyone-need-javascript-generator-functions/

Generators are an _odd_ part of the JavaScript language. And some people find them a bit of a puzzle. You might be a successful developer for decades and never feel the need to reach for them. Which raises the question, if you can go so long without ever needing them, what are they good for?

Generators have a funny syntax, too. They have these strange starred function definitions; you can’t define them with arrow functions; they add this mysterious `yield` keyword. If you’re not familiar with what they’re doing, they can make code impossible to read.

Part of the trouble is that generators are a low-level construct. That is, they’re kind of like a tool for building tools. And it’s those tools we build that solve day-to-day problems. But if you’re looking at generator functions in isolation, it can be hard to see why you’d ever want them.

Generators are quite a powerful construct, though. And they’re handy to have in your metaphorical toolbox. Like most tools, you might not need them for every single job. But for certain jobs, they make life much easier. Once you understand the tool better, you begin to see where they’re helpful. And, equally important, you begin to see when _not_ to use them.

What, then, are generators good for?

## Tim Tams and lazy iterators

Generators have _lots_ of uses. But the most immediate and obvious application is to make _lazy iterators_.

Now, I’m hoping you’re already familiar with JavaScript’s [iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols). These protocols are another low-level language feature. They let us tell the JavaScript engine that some object can be used in a `for...of` loop or with [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

The simplest thing we can do is define a generator function that yields some values. We can then use a `for...of` loop to iterate over them:

```javascript
function* culturalAchievements() {
  yield "Amazing coffee"
  yield "The Sydney Opera House"
  yield "The invention of Wi-Fi"
}

for (achievement of culturalAchievements()) {
  console.log(`Australia is known for: ${achievement}`)
}

// Australia is known for: Amazing coffee
// Australia is known for: The Sydney Opera House
// Australia is known for: The invention of Wi-Fi
```

...

## Infinite Iterators

Back in the 1990s, Arnotts ran a series of commercials for Tim Tams. The first of these featured Cate Blanchett meeting a genie. And involved her character wishing for a packet of Tim Tams that never runs out.

The [whole](https://www.youtube.com/watch?v=wz3hHxgDAnY) [series](https://www.youtube.com/watch?v=-p7thvWWLL0) of ads focussed around the concept of an infinite packet of Tim Tams. And, much like a packet of Tim Tams that never runs out, generators can create infinite iterators.

We could, for example, create a generator function that gives us an infinite sequence of ones:

```javascript
function* allTheOnes() {
  while (true) {
    yield 1
  }
}

console.log([...take(7)(allTheOnes())])
// [ 1, 1, 1, 1, 1, 1, 1 ]
```

Now, that might be interesting. But perhaps not so useful. We could, though, make this a little more general by specifying the value we want to repeat:

```javascript
function* repeat(val) {
  while (true) {
    yield val
  }
}

console.log([...take(3)(repeat("Tim Tam"))])
// [ 'Tim Tam', 'Tim Tam', 'Tim Tam' ]
```

...

## Wrapping up

If you’re not familiar with Generators, they may seem a little weird at first. And because they’re so a low-level language, we can use them for _lots_ of different applications. And that can make it difficult to see what you might want them for, day-to-day. But, as we’ve seen, they’re useful for tasks like:

- Efficiently processing large data sets;
- Working with infinite sequences; and
- Passing messages between two functions.

Now, you may never feel the need to reach for generators. The kind of work you’re doing might not suit them. But, it’s still handy to have them in the toolbox, just in case. And if you start looking, you’ll find generators working away behind the scenes in lots of places. And now and then, you might need to dig into some library code to work out what it’s doing. In those cases, it’s good to have an idea of how they work.
