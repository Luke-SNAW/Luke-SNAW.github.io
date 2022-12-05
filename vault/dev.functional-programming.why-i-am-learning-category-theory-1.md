---
id: m3zpjkkh97bf1ao5rgm3k8l
title: Why I Am Learning Category Theory 1
desc: ""
updated: 1670205125662
created: 1670204953258
---

> https://the.scapegoat.dev/why-i-am-learning-category-theory-1/  
> https://news.ycombinator.com/item?id=33802844

Category theory is a domain of mathematics that exerts a strange influence over programmers. One thing that can be said for sure about category theory is that it is highly abstract, and its relationship to software engineering is not immediately obvious. I consider myself to be more on the pragmatic side of software engineering, so **why did I set out to learn category theory beyond the few concepts popularized by functional programming?**

In particular, I have been following along [MIT 18.S097: Programming with Categories](http://brendanfong.com/programmingcats.html) and reading [Category Theory for Programmers](https://bartoszmilewski.com/2014/10/28/category-theory-for-programmers-the-preface/) by Bartosz Milewski along with a few books like Steve Awodey's [Category Theory](https://www.amazon.com/Category-Theory-Oxford-Logic-Guides/dp/0199237182) and [Seven Sketches in Compositionality](https://www.amazon.com/Invitation-Applied-Category-Theory-Compositionality/dp/1108711820/ref=d_bpx_wsirn_iabw_v1_sccl_2_1/144-6076266-4505621). I want to thank my fellow Recursers who are taking part in our category theory reading group, as I wouldn't have nearly as much fun as I have.

## My background in functional programming

**My background is in systems programming**; I work mostly on embedded and full-stack web development. Having been a Common Lisp aficionado, I use a lot of functional programming patterns. Until recently, my knowledge of category theory was a set of applied patterns: functors, monoids, foldables, applicatives, and especially monads.

I rarely use these concepts explicitly, but they help me build software: I know when to fold a monoidal data structure, how to lift a functor into another, and how to use applicatives to validate data (if these sound abstract, that's because I wanted it to sound abstract. The programming itself is very pedestrian).

Since I write mostly C++, PHP or Javascript, I use functions and simple data structures and don't go heavy on generics and type system magic. However, **because of its theoretical underpinnings, my code can (usually) be cleanly composed into larger structures.**

Yet, I always knew my approach to be a "pop-sci" version of category theory: I never bothered to look up the actual mathematical theory. The rare times I opened up a textbook, I was taken aback by millions of words I didn't know—I would look things up on Wikipedia or nlab and be utterly confused.

My gut, however, was telling me that there was a lot of potential to be unlocked by delving deeper.

## Turning diagrams into code

Since I was a kid, I have been fascinated with [diagrams](https://the.scapegoat.dev/diagrams/).

Nowadays, **I write code by first drawing simple boxes and arrows and doodles, then iteratively transforming them into more formal constructs**. The drawings can represent time sequences, data structures, schema evolution, infrastructure, and state machines. At some point, the design is concrete enough that it can be turned into code.

**Using these diagrams made collaboration with engineers in other disciplines very effective.** For example, when drawing state machine diagrams and sequence diagrams, mechanical engineers I collaborated with were able to point out subtle race conditions, missed transitions, and faulty logic in my firmware.

I "discovered" monads by trying really hard to encode the "arrows" of my state machines into more mundane programming languages like PHP or C++. It was a very autodidact approach, and I knew intuitively that there were formal ways of turning this visual approach to problem-solving into robust software.

It was only years later that I realized that I had been implementing monads all along. This was a deep moment of insight for me. It allowed me to reduce tricky programming problems (concurrency in embedded systems, transaction sequencing, and error handling in distributed systems) into a single, concise concept, along with almost trivial-looking code.

Category theory is literally the mathematics of boxes (objects), arrows (morphisms), and composition. **Composition is how we build large software out of smaller parts while keeping complexity in check.** Boxes and arrows is also how humans think in other disciplines, which makes category theory a powerful tool for uncovering cross-disciplinary analogies.

## Putting words to my thinking

**I have always had an "expanding," holistic way of thinking about software systems.** Going back to software I wrote as a junior developer, like this [AVR Bluetooth Stack](https://github.com/wesen/avr-bt-stack), I wonder if I would write it any differently nowadays. My understanding of composition, naming, and components seem to already be fully formed, despite my inexperience (I only knew BASIC, assembly, and C when I wrote the above).

This holistic approach encompasses systems (the above stack runs on both the host and 8-bit microcontrollers, which wasn't a common pattern back in 2001), machine and human (I always try to think of the developer as an [actual user of the software they write](https://the.scapegoat.dev/you-the-developer-are-a-user-too/), code structure, runtime behavior, among other things. Of course, 18-year-old me didn't come up with these patterns out of the box, and they are influenced by the design of the Bluetooth specification, but the fact that I knew to recognize and apply them speaks to an innate sense of structure.

As described in the previous paragraph, I build software by drawing boxes and arrows first and refining them until I can encode them as software.

This structural approach encompasses much more than just code and data structures. I apply it to:

- product thinking
- communication structures
- schema design and evolution (database design, data schema evolution)
- logging and debugging (events, logging schema)
- runtime behavior (event loops, state machines, sequence diagrams)
- module and codebase decoupling
- software engineering workflow (git workflow, issues, and project management)

Breaking things into boxes and arrows allows me to recognize commonalities across domains, so much so that I, for example, consider [web development to be the same as embedded development](https://the.scapegoat.dev/embedded-programming-is-like-web-development/). I thought this statement would be quite uncontroversial, but it turns out that I got a lot of pushback. The reason I consider the two to be similar, if not the same, is that I have been able to form abstractions that carry across from embedded development to web development. **An abstraction is a controlled form of forgetting the details to focus on something more fundamental, allowing one to make statements that are shorter to state yet broader in meaning.**

Category theory is really the mathematics of composition, reducing everything it encounters to simple structures of objects and morphisms (boxes and arrows, really) and showing where they are similar and where they aren't based on how they can be composed. Once a system has been abstracted, that abstraction is abstracted: categories, functors, and monoids themselves form categories, which are yet more categories that can be put into relation with other categories.

**I hope that category theory will allow me to formalize my intuitive understanding of abstraction, put words to it, and use those words (or, better, words others have written) to explain my thinking.** The hardest about abstraction is that it requires effort to form yet becomes trivial once understood. This leads to a myriad of confusing monad tutorials that assume that there is one easy way to form the mental chunk for that abstraction when really understanding monads about the repeated struggle to work with the concept until it finally clicks. Everybody's favorite monad tutorial is the third they worked through.

## Writing more expressive software

Finally, I am seeing how learning about concepts I already had a good intuitive feel for (monoids, functors, ...) unlocks a whole new world of abstraction. I was swimming at the surface of seemingly simple concepts that actually have incredible depth, depths talented mathematicians have been studying for centuries. A good podcast about this is [corecursive's episode about portal abstractions with Sam Ritchie](https://corecursive.com/050-sam-ritchie-portal-abstractions-2/).

While I already use a lot of these patterns when writing functional code, there is so much more to be gained from understanding monoids or functors as formulated in category theory language. I started recognizing them in schema migrations, database transactions, state transitions in embedded systems, wire protocols, etc.

**While I rarely call my classes or functions or modules mathematical names (in fact, due to the messy imperative languages I tend to use, I often can't, as their type system is rarely powerful enough), my thinking is heavily inspired by the underlying mathematical concept**. That doesn't really matter much to me since writing verbose code due to not having programming language support doesn't impact the abstraction and its validity as such.

**The soundness of the abstractions unearthed by thinking about a domain in terms of category theory means that elegant, concise, and, most importantly, composable domain-specific languages can be designed.** This might be the most important result I get from learning more about mathematics. To me, a domain-specific language doesn't need to be an actual language but also encompasses API and protocol design.

## A never-ending journey

I am still at the very surface of category theory and just hit the first wall by working on F-algebras and recursion schemes. Yet, the value I got from sitting down and understanding functors, monoids, and adjunctions at a rigorous mathematical level, as well as working with the "actual" definition of categories, has already brought me a lot of confidence in my current approach to software design.

I couldn't be more excited about what is coming next.
