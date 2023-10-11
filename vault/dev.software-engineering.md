---
id: j0N1aVKxe96dktmyADG9U
title: Software Engineering
desc: ""
updated: 1696901977461
created: 1645514209965
---

## Collections

- [Bulletproof React](https://github.com/alan2207/bulletproof-react) - A simple, scalable, and powerful architecture for building production ready React applications.
- [Code Smells](https://refactoring.guru/refactoring/smells)
- [Notes on Software Development Waste](https://hcarvalhoalves.github.io/software-development-waste/)
- [Small choices can wreck your codebase](https://swizec.com/blog/even-small-things-can-make-your-code-gnarly/)
- [Don’t start with microservices – monoliths are your friend](https://arnoldgalovics.com/microservices-in-production/)
- [Every Public Engineering Career Ladder](https://www.swyx.io/career-ladders/)
- [Best career advice: ask for feedback](https://xdg.me/ask-for-feedback/)
- [Programming to Interface Vs to Implementation](https://dmitripavlutin.com/interface-vs-implementation/)
- [The Catalog of Design Patterns](https://refactoring.guru/design-patterns/catalog)
- [Make It Work Make It Right Make It Fast](https://wiki.c2.com/?MakeItWorkMakeItRightMakeItFast) is an assertion that if you can "make it right", you'll be able to "make it fast" later.
- [Colocation](https://kentcdodds.com/blog/colocation)
- [Project Guidelines](https://github.com/elsewhencode/project-guidelines)
- [Hexagonal-Inspired Architecture in React](https://alexkondov.com/hexagonal-inspired-architecture-in-react/) #bookmark
- [Cheating is All You Need](https://about.sourcegraph.com/blog/cheating-is-all-you-need)

  > Software engineering exists as a discipline because you cannot EVER under any circumstances TRUST CODE.
  >
  > - You get the LLM to draft some code for you that’s 80% complete/correct.
  > - You tweak the last 20% by hand.

  > > [Vanclief](https://news.ycombinator.com/item?id=35275438) is hesitant about 5 times as productive because we only need to "check the code is good" for two main reasons:
  > >
  > > 1. It is my belief that if you are proficient enough in the task at hand, it is actually a distraction to be checking "someone else code" over just writing it yourself. When I wrote the code, I know it by heart and I know what it does (or is supposed to do). At least for me, having to be creating prompts and then reviewing the code that generates is slower and takes me out of the flow. It is also more exhausting than just writing the thing myself.
  > > 2. I am only able to check the correctness of the code, if am am proficient enough as a programmer (and possibly in the language as well). To become proficient I need to write a lot of code, but the more I use LLMs, the less repetitions I get in. So in a way it feels like LLMs are going to make you a "worse" programmer by doing the work for you.

- [Handles are the better pointers](https://floooh.github.io/2018/06/17/handles-vs-pointers.html)
- [Nanosecond timestamp collisions are common](https://www.evanjones.ca/nanosecond-collisions.html)
  - https://datatracker.ietf.org/doc/html/draft-peabody-dispatch-new-uuid-format
- [How Instagram scaled to 14 million users with only 3 engineers](https://instagram-engineering.com/what-powers-instagram-hundreds-of-instances-dozens-of-technologies-adf2e22da2ad)
  - Keep things very simple.
  - Don’t re-invent the wheel.
  - Use proven, solid technologies when possible.

## [You Can't Buy Integration](https://martinfowler.com/articles/cant-buy-integration.html)

- [99.5% of programming consists of gluing together calls to library functions.](http://paulgraham.com/weird.html)

## [Don't Call Yourself A Programmer, And Other Career Advice](https://www.kalzumeus.com/2011/10/28/dont-call-yourself-a-programmer/)

- 90% of programming jobs are in creating Line of Business software.
- Engineers are hired to create business value, not to program things.
- Add revenue. Reduce costs. Those are your only goals.

## [Eight tips to Write Functions like a Senior Developer](https://medium.com/@dhruba-dahal/eight-tips-to-write-functions-like-a-senior-developer-794140719351)

- Do one thing and do it well
- Never use flag arguments
- Prefer exceptions over error codes
- Make separation between command and query

## Architecture

- [Domain-centric Architectures (Clean and Hexagonal) for Dummies](https://medium.com/codex/clean-architecture-for-dummies-df6561d42c94)
- [BBC Online Uses Serverless to Scale Extremely Fast](https://www.infoq.com/news/2021/01/bbc-serverless-scale/)
- [Islands Architecture](https://www.patterns.dev/posts/islands-architecture/)
- [HN: Modules, not microservices](https://news.ycombinator.com/item?id=34230641)
  > - I just want to point out that for the second problem (scalability of CPU/memory/io), microservices almost always make things worse.
  > - I was working at Amazon when they started transitioning from monolith to microservices, and the big win there was locality of data and caching.
  > - Microservices are less _efficient_, but are still more _scalable_.
  > - I am working on a project that uses a microservice architecture to make the individual components scalable and separate the concerns. However one of the unexpected consequences is that we are now doing a lot of network calls between these microservices, and this has actually become the main speed bottleneck for our program, especially since some of these services are not even in the same data center. We are now attempting to solve this with caches and doing batch requests, but all of this created additional overhead that could have all been avoided by not using microservices.  
  >   This experience has strongly impacted my view of microservices and for all personal projects I will develop in the future I will stick with a monolith until much later instead of starting with microservices.

### [Thread-per-core](https://without.boats/blog/thread-per-core/)

The thread-per-core architecture for Rust async programs has been controversial. While it promises better performance and ease of implementation, it may only achieve one, not both. A share-nothing approach keeps data in separate core caches but is complex to implement transactionally. Research showed this approach reduced tail latencies over a shared approach. However, the experiments did not test dynamic work imbalances that could appear in practice. Work-stealing may help address imbalances while still keeping some data pinned to cores, achieving both performance and utilization benefits. The debate focuses on balancing work-stealing with shared state rather than ease of implementation claims.

> [The debate isn't about thread-per-core work stealing executors, it's whether async/await is a good abstraction for it in Rust. And the more async code I write the more I feel that it's leaky and hard to program against.](https://news.ycombinator.com/item?id=37791635)
