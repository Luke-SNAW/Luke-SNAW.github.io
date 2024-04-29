---
id: 1mi9m99hBJq32lfoqGdNB
title: Test
desc: ""
updated: 1714003735767
created: 1645055059758
---

- QA - 제품 개발단계에서 품질보증 활동 (고품질 확보)
- QC - 제품 양산 단계에서 품질관리 (불량품 제거)
- QE - QA/QC를 수행하기 위한 모든 엔지니어링 활동 (자동화 T/C설계, 테스트용 데이터 생성)

---

## Collections

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

- [Testing on the Toilet: Don't Put Logic in Tests](https://testing.googleblog.com/2014/07/testing-on-toilet-dont-put-logic-in.html)
  > Production code computes outputs from inputs while tests specify concrete input/output pairs. Complex test logic should be moved to helper functions with their own tests, leaving test bodies simple.
- [TDD's Missing Skill: Behavioral Composition](https://tidyfirst.substack.com/p/tdds-missing-skill-behavioral-composition)

## [An External Replication on the Effects of Test-driven Development Using a Multi-site Blind Analysis Approach](https://dl.acm.org/doi/10.1145/2961111.2962592)

- Replication study, 39 professionals, real projects
- No significant difference between test-first and test-last development
- "The claimed benefits of TDD may…rather [be] due to the fact that [it] encourages fine-grained steady steps that improve focus and flow."

## [What Do We Know about Test-Driven Development?](https://ieeexplore.ieee.org/document/5604358)

### How Effective is Test-Driven Development?

…evidence from controlled experiments suggests an improvement in productivity when TDD is used. However…pilot studies provide mixed evidence, some in favor of and others against TDD. In the industrial studies…evidence suggests that TDD yields worse productivity. Even when considering only the more rigorous studies…the evidence is equally split for and against a positive effect.

## [HOW NOT TO WRITE PROPERTY TESTS IN JAVASCRIPT](https://jrsinclair.com/articles/2021/how-not-to-write-property-tests-in-javascript/)

As tests, integration, and end-to-end tests deliver the most value. But like with Test Driven Development (TDD), tests aren’t the point.  
I became enthusiastic about TDD because when I practised it, I wrote better code. The _discipline_ of thinking about tests forced me to clarify my intent. I started writing code in smaller, more comprehensible chunks. Not only did the code need less maintenance, but when it did, I dreaded going back to the old code less.  
Then I discovered property-based testing. It takes all those benefits of TDD and increases them an order of magnitude. I thought I understood my code. Then I started thinking about properties and learned I did not. Instead of thinking about whether my code _worked_ I began to think about whether it’s _correct_.  
Experienced software engineers all give lip service to “thinking through edge cases.” We’re supposed to consider every possible thing the world might throw at our code. Property tests force you to actually do it.  
It’s not just about edge cases though. Thinking about properties is a mindset. And this mindset is so valuable that it’s worth practising, _even if you delete all the tests aftewards._ Sure, you’d then need to write some other tests to catch regressions. But if property tests are slowing your builds, delete them. Copy the properties into code comments or add `.skip` to your tests so you can get them back if you need. The tests aren’t the point, they’re a side-benefit.

## [Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)

### The Difference Between Mocks and Stubs

...

Meszaros uses the term **Test Double** as the generic term for any kind of pretend object used in place of a real object for testing purposes. The name comes from the notion of a Stunt Double in movies. (One of his aims was to avoid using any name that was already widely used.) Meszaros then defined five particular kinds of double:

- **Dummy** objects are passed around but never actually used. Usually they are just used to fill parameter lists.
- **Fake** objects actually have working implementations, but usually take some shortcut which makes them not suitable for production (an [in memory database](https://martinfowler.com/bliki/InMemoryTestDatabase.html) is a good example).
- **Stubs** provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test.
- **Spies** are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.
- **Mocks** are what we are talking about here: objects pre-programmed with expectations which form a specification of the calls they are expected to receive.

Of these kinds of doubles, only mocks insist upon behavior verification. The other doubles can, and usually do, use state verification. Mocks actually do behave like other doubles during the exercise phase, as they need to make the SUT believe it's talking with its real collaborators - but mocks differ in the setup and the verification phases.

## [5 Books for QA Engineers](https://dzone.com/articles/5-books-for-qa-engineers)

### 1. Testing Computer Software, by Cem Kaner, Hung Q. Nguyen, and Jack Falk

[This book](https://www.amazon.com/-/en/Cem-Kaner/dp/0471358460) is a real classic that should be read by specialists, starting at the junior level. It differs from other books for QA engineers primarily in its attachment to the conditions of the real world, using the example of well-known Silicon Valley development companies.

The authors thoroughly consider a wide range of issues, from the organization of the quality assurance process to the actual testing of documentation, code, projects, etc. If you are new to software testing or have some experience but no formal training, this book will provide you with the right tools to approach software testing and will also give you insights that could take you years to learn on your own.

This book does not discuss the testing techniques used in agile development approaches. Also, it may be difficult to focus on what the writers are attempting to express without being sidetracked or shut down by outmoded examples. But, putting that aside, it’s an excellent book for QA engineers.

### 2. Testing Computer Software, by Lee Copeland

One of the greatest books for QA engineers that can be very useful for specialists at various levels. It only covers the design of tests and does not consider issues of planning and organization of the testing processes. However, in this book for QA engineers, you can find both new methods and in-depth descriptions of already-known ones. For example, [Testing Computer Software](https://www.amazon.com/Practitioners-Guide-Software-Test-Design/dp/158053791X) describes seven approaches to testing using the “black box” method and several “white box” methods. There are nothing superfluous here, only useful and practical examples with tables and diagrams, a clear description of techniques, and additional tips. At the end of the book, there´s a section with conclusions and a list of other author's works on the topic that can also be useful. I recommend it if you want to prepare to obtain a professional certification.

In my opinion, this book gives the best account of pairwise testing that I have found, with or without using orthogonal arrays. Besides being detailed, it includes examples to make it clear. The test coverage that can be achieved with well-chosen pairwise test cases seems too good to be true. According to the author, if necessary, some tester prudence should be used to supplement the technique

### 3. How Google Tests Software, by James Whittaker, Jason Arbon, and Jeff Carollo

Oriented more toward senior engineers, this book will show how the best of the best QA specialists conduct their testing. The book gives an overview of the approach Google takes to testing software, followed by chapters dedicated to the two test engineering roles at Google, which are the [Software Engineer in Test](https://www.amazon.com/Google-Tests-Software-James-Whittaker/dp/0321803027) (SET) and Test Engineer (TE) roles. Throughout the book, there are sections and interviews with many other Google employees, with the final chapter being dedicated to some of the thoughts on the direction of testing at Google.

Note that just because something works well at Google doesn’t necessarily mean that it will work well at some other company making some other type of product. Even Google could have made some different choices for some of their testing solutions and been equally successful.

### 4. Lessons Learned in Software Testing, by Cem Kaner, James Bach, and Bret Pettichord

This is one of my favorite books for QA engineers. It’s a fabulous [collection of tips, hints, and techniques](https://www.amazon.es/Lessons-Learned-Software-Testing-Context-Driven/dp/0471081124) for both the new and the experienced person working in a software test department. It covers obvious areas like testing techniques, automated testing (the material about what automated testing can’t do is very high-grade), documenting testing, and managing a test project.

The book starts with the role of a tester. The next chapter relates to how to think as a tester and provides interesting references in completely different knowledge areas that may help testers improve. Another chapter covers different testing techniques and bugs in writing and test automation. There are also chapters that relate to working with others.

### 5 – Agile Testing: A Practical Guide for Testers and Agile Teams, by Lisa Crispin and Janet Gregory

This book talks about using [Agile testing quadrants](https://www.amazon.com/Agile-Testing-Practical-Guide-Testers/dp/0321534468) to figure out what testing is required, who can perform the testing, and what tools can aid in it. Here are some key insights you could learn from this book for QA engineers:

- How to get testers engaged in agile development.
- Where do testers and QA managers fit on an agile team?
- What to look for when hiring an agile tester?
- How to transition from a traditional cycle to agile development.
- How to complete testing activities in short iterations.
- How to use tests to successfully guide development.
- How to overcome barriers to test automation.

I hope you found these books for QA engineers helpful and that they will help you increase your knowledge in different areas to grow as a professional.
