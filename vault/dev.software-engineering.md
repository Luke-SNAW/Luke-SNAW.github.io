---
id: j0N1aVKxe96dktmyADG9U
title: Software Engineering
desc: ""
updated: 1672790204993
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
