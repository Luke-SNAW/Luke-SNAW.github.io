---
id: 1mi9m99hBJq32lfoqGdNB
title: Test
desc: ""
updated: 1650327191314
created: 1645055059758
---

- QA - 제품 개발단계에서 품질보증 활동 (고품질 확보)
- QC - 제품 양산 단계에서 품질관리 (불량품 제거)
- QE - QA/QC를 수행하기 위한 모든 엔지니어링 활동 (자동화 T/C설계, 테스트용 데이터 생성)

---

- [TDD Changed My Life](https://medium.com/javascript-scene/tdd-changed-my-life-5af0ce099f80)
- [The Cycles of TDD](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)
- [A Comparative Case Study on the Impact of Test-Driven Development on Program Design and Test Coverage](https://ieeexplore.ieee.org/abstract/document/4343755)
- [5 Questions Every Unit Test Must Answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d)
  1. What are you testing?
  2. What should it do?
  3. What is the actual output?
  4. What is the expected output?
  5. How can the test be reproduced?
- [Why I use Tape Instead of Mocha & So Should You](https://medium.com/javascript-scene/why-i-use-tape-instead-of-mocha-so-should-you-6aa105d8eaf4)
- [Rethinking Unit Test Assertions](https://medium.com/javascript-scene/rethinking-unit-test-assertions-55f59358253f)
- [Why I Never Use Shallow Rendering](https://kentcdodds.com/blog/why-i-never-use-shallow-rendering)

  > With shallow rendering, I can refactor my component's implementation and my tests break. With shallow rendering, I can break my application and my tests say everything's still working.

  - [For actual unit testing](https://kentcdodds.com/blog/why-i-never-use-shallow-rendering#for-actual-unittesting)

# [An External Replication on the Effects of Test-driven Development Using a Multi-site Blind Analysis Approach](https://dl.acm.org/doi/10.1145/2961111.2962592)

- Replication study, 39 professionals, real projects
- No significant difference between test-first and test-last development
- "The claimed benefits of TDD may…rather [be] due to the fact that [it] encourages fine-grained steady steps that improve focus and flow."

# [What Do We Know about Test-Driven Development?](https://ieeexplore.ieee.org/document/5604358)

## How Effective is Test-Driven Development?

…evidence from controlled experiments suggests an improvement in productivity when TDD is used. However…pilot studies provide mixed evidence, some in favor of and others against TDD. In the industrial studies…evidence suggests that TDD yields worse productivity. Even when considering only the more rigorous studies…the evidence is equally split for and against a positive effect.

# [HOW NOT TO WRITE PROPERTY TESTS IN JAVASCRIPT](https://jrsinclair.com/articles/2021/how-not-to-write-property-tests-in-javascript/)

As tests, integration, and end-to-end tests deliver the most value. But like with Test Driven Development (TDD), tests aren’t the point.  
I became enthusiastic about TDD because when I practised it, I wrote better code. The _discipline_ of thinking about tests forced me to clarify my intent. I started writing code in smaller, more comprehensible chunks. Not only did the code need less maintenance, but when it did, I dreaded going back to the old code less.  
Then I discovered property-based testing. It takes all those benefits of TDD and increases them an order of magnitude. I thought I understood my code. Then I started thinking about properties and learned I did not. Instead of thinking about whether my code _worked_ I began to think about whether it’s _correct_.  
Experienced software engineers all give lip service to “thinking through edge cases.” We’re supposed to consider every possible thing the world might throw at our code. Property tests force you to actually do it.  
It’s not just about edge cases though. Thinking about properties is a mindset. And this mindset is so valuable that it’s worth practising, _even if you delete all the tests aftewards._ Sure, you’d then need to write some other tests to catch regressions. But if property tests are slowing your builds, delete them. Copy the properties into code comments or add `.skip` to your tests so you can get them back if you need. The tests aren’t the point, they’re a side-benefit.

# [Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)

## The Difference Between Mocks and Stubs

...

Meszaros uses the term **Test Double** as the generic term for any kind of pretend object used in place of a real object for testing purposes. The name comes from the notion of a Stunt Double in movies. (One of his aims was to avoid using any name that was already widely used.) Meszaros then defined five particular kinds of double:

- **Dummy** objects are passed around but never actually used. Usually they are just used to fill parameter lists.
- **Fake** objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an [in memory database](https://martinfowler.com/bliki/InMemoryTestDatabase.html) is a good example).
- **Stubs** provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test.
- **Spies** are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.
- **Mocks** are what we are talking about here: objects pre-programmed with expectations which form a specification of the calls they are expected to receive.

Of these kinds of doubles, only mocks insist upon behavior verification. The other doubles can, and usually do, use state verification. Mocks actually do behave like other doubles during the exercise phase, as they need to make the SUT believe it's talking with its real collaborators - but mocks differ in the setup and the verification phases.
