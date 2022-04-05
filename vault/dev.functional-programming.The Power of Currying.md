---
id: ew2g878jseu0jd1334f4z25
title: The Power of Currying
desc: ""
updated: 1649205302283
created: 1649204876682
---

https://blog.bitsrc.io/functional-programming-part-3-the-powers-of-currying-213eb69b234b

# What is Currying

A curried function is a **function that keeps returning functions until all its params are fulfilled**

# How Currying Works

# Why Currying

Currying will make our code:

1. Cleaner
2. Less repetitive params passing and less verbose code
3. More composable
4. More reusable

# Why Currying Makes our Code Better

## Mainly, some functions take “config” data as input

If we have functions that take “config” params, we better curry them because these “configs” will probably be repeated over and over again.

If we have functions that take “config” params, we better curry them because these “configs” will probably be repeated over and over again.
For example, let’s suppose we have a translator function, that takes a locale and a text to be translated:

```javascript
const translator = (locale, text) => {
  /*translation*/
};
```

The usage would look like this:

```javascript
translator("fr", "Hello");
translator("fr", "Goodbye");
translator("fr", "How are you?");
```

Every time we call translator we **should provide** locale and text. Which is redundant and dirty to provide the locale on every call.
But instead, let’s curry translator like this:

```javascript
const translator = curry((locale, text) => {
  /*translation*/
});
const inFrench = translator("fr");
```

Now `inFrench` **has** `fr` as `locale` provided to the curried translator function and **waits** for `text` to be provided. We can use it like this:

```javascript
inFrench("Hello");
inFrench("Goodbye");
inFrench("How are you?");
```

Currying did us a great favour indeed, we don’t need to specify the locale each time, instead the curried `inFrench` **has** `locale` due to currying.
After currying -in this specific example. Code is:

1. Cleaner
2. Less verbose and less redundant
   **Because we separated “config” from actual “data”. Which is quite handy in many areas and use cases.**

# Why separate “config” from “data” params?

Many components and functions need the use of some functionalities (`translate` in our case) but **shouldn’t or can’t know about the “config” part** (`locale`). Where these components or functions **have the “data” only part** (`text`). **So these functions will be able to use that function without the need of knowing about the “config” part.**

Thus, that component or function **will be less coupled with the system**, which will make the components more composable and more maintainable.

# When do we apply this idea

# Closure and Currying Relationship

A **Closure**: is a function returned by a “parent” function and has access to the parent function’s internal state. (described earlier here)
**Currying**: will always result a closure. Because each function returned by a curried function will be provided with parents’ internal state.

# More Examples
