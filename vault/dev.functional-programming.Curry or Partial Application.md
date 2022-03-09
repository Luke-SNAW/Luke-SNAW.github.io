---
id: 4vjiywn2gjb1gzms9bqustx
title: Curry or Partial Application?
desc: ""
updated: 1646822642166
created: 1646822177926
---

https://medium.com/javascript-scene/curry-or-partial-application-8150044c78b8

The Difference Between
Partial Application and Curry

# Definitions

Application: The process of applying a function to its arguments in order to produce a return value.

Partial Application: The process of applying a function to some of its arguments. The partially applied function gets returned for later use. In other words, a function that **takes a function with multiple parameters** and **returns a function with fewer parameters**. Partial application fixes (partially applies the function to) one or more arguments inside the returned function, and the returned function takes the remaining parameters as arguments in order to complete the function application.

Curry: A function that **takes a function with multiple parameters** as input and **returns a function with exactly one parameter**.

# Why Does this Matter?

James Coglan gave a great talk that will help explain why you should care:
https://youtu.be/XcS-LdEBUkE

- A partial application **may or may not have a predictable return type**.
- A curried function always returns another function with an arity of 1 until all of the arguments have been applied.

All the cool things James talks about rely on **function type uniformity**. For example he talks about how promises can help abstract your program logic’s dependence on time.

Promises do that because they **lift** whatever function you’re calling so that the return type is always uniform: All functions that return promises return the same type, which means that you can use them in standardized ways. James talks about lots of ways that promises help.

By dealing with **containers** instead of the **values inside of containers**, you can create lots of **generic functions that will work universally** for anything that uses the **container’s interface**.

Like promises, **curried functions return containers** that all share the same interface. The **returned functions are the containers** in this case. You just keep calling the returned function until you’ve exhausted all the arguments and the final value gets returned.

In other words, **a curried function is a function that can lift all of its arguments** so that **you can deal** with those arguments **in a standardized way**.

The most common use for currying in functional programming is to make it easier to compose functions. For more on that topic, read [“Master the JavaScript Interview: What is Function Composition?”](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0)
