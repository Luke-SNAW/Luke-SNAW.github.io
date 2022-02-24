---
id: oqorpev88k7pz1ycbznggbt
title: HOW TO GET STARTED WITH PROPERTY-BASED TESTING IN JAVASCRIPT USING FAST-CHECK
desc: ""
updated: 1645692279794
created: 1645687239237
---

https://jrsinclair.com/articles/2021/how-to-get-started-with-property-based-testing-in-javascript-with-fast-check/

Property-based testing helps us write better tests, with less code, and greater coverage. This leads to more confidence in our code, and fewer bugs in our applications. But, as always, there’s a price. Property tests take more effort to write, and they take longer to run. Still, I’m convinced that the trade-off is worth it.

# What is property-based testing?

Most tests we programmers write are example-based tests.

Instead of writing every example input by hand, we instruct the computer to generate them for us. We tell the computer what types of input we want, and it generates hundreds of random examples.

Now, this raises a question: If we have randomly generated input, how do we know what output to expect? And the answer is, we don’t. Well, not exactly, anyway. Instead of testing that a particular input matches expected output, we assert properties.

A property is something that should always be true. They’re sometimes referred to as ‘laws’ or ‘rules’. This sounds abstract, and a little mathematical.

# A hypothetical scenario

# How do we work out what properties to test?

# Writing a property test

# Fixing our code

# Is property testing bad practice?

Now, at first glance, you might think property-based testing goes against conventional wisdom. Instead of a handful of unit tests, we’re suddenly running hundreds or thousands of tests. Won’t this make refactoring difficult? As a colleague of mine commented:

> My worry is that introducing property-based testing brings us back to a world where we have very rigid tests, that stifle ongoing development on components.

This is a reasonable concern. But let’s be clear about why we want to avoid having lots of small tests. We want to avoid testing implementation details. That is, we don’t want to over-specify our tests. Doing so wastes time and CPU cycles checking things that don’t matter. Or worse, fixing broken tests that never tested anything useful in the first place.

Counter to what you might expect, property tests make it harder to over-specify tests. It means not testing things we don’t care about.

The nice thing about property tests is that they combine the best bits of integration tests, end-to-end tests, and unit tests.

# References

If you’d like to learn more about property-based tests, I’ve listed a few good references below:

- [The Magic of Generative Testing: Fast-Check in JavaScript](https://www.youtube.com/watch?v=a2J_FSkxWKo). An excellent (and short) presentation introducing property-based testing.
- [Property Testing with JSVerify](https://dev.to/glebec/property-testing-with-jsverify-part-i-3one). Gabriel Lebec has written a nice introduction to property testing. It uses another library, jsverify, but it’s still worth a read.
- [John Hughes - Don’t Write Tests](https://www.youtube.com/watch?v=hXnS_Xjwk2Y). John Hughes is one of the authors of QuickCheck. QuickCheck is the original property-testing framework for Haskell.
- [John Hughes - How to specify it! A guide to writing properties of pure functions | Code Mesh LDN 19](https://www.youtube.com/watch?v=zvRAyq5wj38). More good advice from John Hughes.
- [Algebra-Driven Design by Sandy Maguire](https://www.youtube.com/watch?v=zvRAyq5wj38). Sandy Maguire takes property-based testing and applies it to software development in general. He creates a whole new way of approaching software engineering.

Finally, you can find the code I used to write this tutorial on GitHub.
