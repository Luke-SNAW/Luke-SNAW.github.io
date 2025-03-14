---
id: j0N1aVKxe96dktmyADG9U
title: Software Engineering
desc: ""
updated: 1741564362142
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
- [Locality of Behaviour (LoB)](https://htmx.org/essays/locality-of-behaviour/)
- [Locality of Behavior in React Components](https://alexkondov.com/locality-of-behavior-react/)
  > Abstractions are not an enemy of locality. You don’t need to inline everything in a single file. In the context of a React component, the invocation of the function is more important than what it actually does.
- [Bloom Filters](https://samwho.dev/bloom-filters/)
  - Bloom filters return true it doesn't mean "yes", it means "maybe", false-positive.
  - If you're happy to accept being wrong 0.0001% of the time (1 in a million), you could use a bloom filter which can store the same data in 82% reduction in size.
- [Three Laws of Software Complexity](https://maheshba.bitbucket.io/blog/2024/05/08/2024-ThreeLaws.html)
  1. A well-designed system will degrade into a badly designed system over time.
  2. Complexity is a Moat (filled by Leaky Abstractions).
  3. There is no fundamental upper limit on Software Complexity.
- [When Imperfect Systems are Good, Actually: Bluesky's Lossy Timelines](https://jazco.dev/2025/02/19/imperfection/)
- [Succinct data structures](https://blog.startifact.com/posts/succinct/)

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
- [Domain-Driven Hexagon](https://github.com/Sairyss/domain-driven-hexagon)
- [BBC Online Uses Serverless to Scale Extremely Fast](https://www.infoq.com/news/2021/01/bbc-serverless-scale/)
- [Islands Architecture](https://www.patterns.dev/posts/islands-architecture/)
- [HN: Modules, not microservices](https://news.ycombinator.com/item?id=34230641)
  > - I just want to point out that for the second problem (scalability of CPU/memory/io), microservices almost always make things worse.
  > - I was working at Amazon when they started transitioning from monolith to microservices, and the big win there was locality of data and caching.
  > - Microservices are less _efficient_, but are still more _scalable_.
  > - I am working on a project that uses a microservice architecture to make the individual components scalable and separate the concerns. However one of the unexpected consequences is that we are now doing a lot of network calls between these microservices, and this has actually become the main speed bottleneck for our program, especially since some of these services are not even in the same data center. We are now attempting to solve this with caches and doing batch requests, but all of this created additional overhead that could have all been avoided by not using microservices.  
  >   This experience has strongly impacted my view of microservices and for all personal projects I will develop in the future I will stick with a monolith until much later instead of starting with microservices.
- [Kernighan and Pike were right: Do one thing, and do it well](https://medium.com/source-and-buggy/do-one-thing-and-do-it-well-886b11a5d21)
- [It's not microservice or monolith; it's cognitive load you need to understand first](https://fernandovillalba.substack.com/p/its-not-microservice-or-monolith)
  > - “Instead of choosing between a monolithic architecture or a microservices architecture, design the software to fit the maximum team cognitive load”
  > - If you have only one team, consider adjusting your architecture to match the team’s capacity. Favour monolithic, cohesive and modular architectures.
  > - If you have multiple teams, consider doing microservices or similar type of architectures so they can work independently.
  > - The types of communication boundaries change significantly between single and multiple team architectures. Single teams are optimized to communicate via the codebase, documentation, discussions and design meetings. Multiple teams are better optimized to communicate via well-designed APIs (or libraries) that abstract the complexities of their domains.

### [Thread-per-core](https://without.boats/blog/thread-per-core/)

The thread-per-core architecture for Rust async programs has been controversial. While it promises better performance and ease of implementation, it may only achieve one, not both. A share-nothing approach keeps data in separate core caches but is complex to implement transactionally. Research showed this approach reduced tail latencies over a shared approach. However, the experiments did not test dynamic work imbalances that could appear in practice. Work-stealing may help address imbalances while still keeping some data pinned to cores, achieving both performance and utilization benefits. The debate focuses on balancing work-stealing with shared state rather than ease of implementation claims.

> [The debate isn't about thread-per-core work stealing executors, it's whether async/await is a good abstraction for it in Rust. And the more async code I write the more I feel that it's leaky and hard to program against.](https://news.ycombinator.com/item?id=37791635)

## Algorithms

### [Hexagonal Grids](https://www.redblobgames.com/grids/hexagons/)

This guide discusses different approaches to representing hexagonal grids in code, including cube, axial, offset, and doubled coordinates.

- Each system has tradeoffs in terms of simplicity for algorithms and storage.
- Axial coordinates are recommended for algorithms as they allow basic math operations.
- Offset coordinates may be better for storage.

## [Approximate timing for various operations on a typical PC](https://norvig.com/21-days.html)

<table border="1" cellpadding="2" cellspacing="2"><tbody><tr><td>execute typical instruction</td><td align="right">1/1,000,000,000 sec = 1 nanosec</td></tr><tr><td>fetch from L1 cache memory</td><td align="right">0.5 nanosec</td></tr><tr><td>branch misprediction</td><td align="right">5 nanosec</td></tr><tr><td>fetch from L2 cache memory</td><td align="right">7 nanosec</td></tr><tr><td>Mutex lock/unlock</td><td align="right">25 nanosec</td></tr><tr><td>fetch from main memory</td><td align="right">100 nanosec</td></tr><tr><td>send 2K bytes over 1Gbps network</td><td align="right">20,000 nanosec</td></tr><tr><td>read 1MB sequentially from memory</td><td align="right">250,000 nanosec</td></tr><tr><td>fetch from new disk location (seek)</td><td align="right">8,000,000 nanosec</td></tr><tr><td>read 1MB sequentially from disk</td><td align="right">20,000,000 nanosec</td></tr><tr><td>send packet US to Europe and back</td><td align="right">150 milliseconds = 150,000,000 nanosec</td></tr></tbody></table>

## Crypto

- [the cryptopals crypto challenges](https://cryptopals.com/)
