---
id: mdm9l0q7bcpw3otz04otp8s
title: Software Engineering at Google
desc: ""
updated: 1690515661314
created: 1689901150134
published: false
---

> https://abseil.io/resources/swe-book
>
> Code is a liability, not an asset. Code itself doesn’t bring value: it is the functionality that it provides that brings value. That functionality is an asset if it meets a user need: the code that implements this functionality is simply a means to that end.

## Thesis- [What Is Software Engineering?](https://abseil.io/resources/swe-book/html/ch01.html)

> Software engineering differs from programming in that it focuses on maintaining code over longer time periods and at larger scales. This requires planning for change, managing dependencies, and making trade-offs. Sustainability means being able to adapt to changes over the software's lifetime. Hyrums Law states that observable behaviors will be depended upon, regardless of promises. Scaling policies like expertise, automation, and consistency help. Decisions should be based on data, but data is often incomplete so assumptions are needed. While software engineering focuses on longevity, programming focuses on immediate goals; different best practices apply to each.

### [Time and Change](https://abseil.io/resources/swe-book/html/ch01.html#time_and_change)

We also find developers of short-lived code in common industry settings. Mobile apps often have a fairly short life span,6 and for better or worse, full rewrites are relatively common. Engineers at an early-stage startup might rightly choose to focus on immediate goals over long-term investments: the company might not live long enough to reap the benefits of an infrastructure investment that pays off slowly. **A serial startup developer could very reasonably have 10 years of development experience and little or no experience maintaining any piece of software expected to exist for longer than a year or two.**

### [TL;DRs](https://abseil.io/resources/swe-book/html/ch01.html#tlsemicolondr)

- “Software engineering” differs from “programming” in dimensionality: programming is about producing code. Software engineering extends that to include the maintenance of that code for its useful life span.
- There is a factor of at least 100,000 times between the life spans of short-lived code and long-lived code. It is silly to assume that the same best practices apply universally on both ends of that spectrum.
- Software is sustainable when, for the expected life span of the code, we are capable of responding to changes in dependencies, technology, or product requirements. We may choose to not change things, but we need to be capable.
- Hyrum’s Law: with a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody.
- Every task your organization has to do repeatedly should be scalable (linear or better) in terms of human input. Policies are a wonderful tool for making process scalable.
- Process inefficiencies and other software-development tasks tend to scale up slowly. Be careful about boiled-frog problems.
- Expertise pays off particularly well when combined with economies of scale.
- “Because I said so” is a terrible reason to do things.
- Being data driven is a good start, but in reality, most decisions are based on a mix of data, assumption, precedent, and argument. It’s best when objective data makes up the majority of those inputs, but it can rarely be _all_ of them.
- Being data driven over time implies the need to change directions when the data changes (or when assumptions are dispelled). Mistakes or revised plans are inevitable.

## Culture - [How to Work Well on Teams](https://abseil.io/resources/swe-book/html/ch02.html)

> Software engineering requires collaboration and teamwork. However, many engineers dream of being lone geniuses who create world-changing software in isolation. This "genius myth" leads engineers to hide their work from others, which increases the risk of failure and slows progress. Instead, engineers should embrace humility, share their work early, and accept criticism constructively. Working with a team provides rapid feedback, spreads knowledge, and increases the pace of progress. The key to success is creating a high-functioning team where members have behaviors like openness to influence, patience, and a willingness to admit mistakes and learn from failures. Ultimately, a well-functioning team is the foundation for any successful software endeavor.

### TL;DRs

- Be aware of the trade-offs of working in isolation.
- Acknowledge the amount of time that you and your team spend communicating and in interpersonal conflict. A small investment in understanding personalities and working styles of yourself and others can go a long way toward improving productivity.
- If you want to work effectively with a team or a large organization, be aware of your preferred working style and that of others.

## Culture - [Knowledge Sharing](https://abseil.io/resources/swe-book/html/ch03.html)

> Knowledge sharing is crucial for organizations to scale and grow. Creating a culture of psychological safety where people feel comfortable asking questions and admitting what they don't know is the foundation. Organizations should make it easy for people to access both human experts and documented references. They should incentivize and reward those who take time to teach and share their expertise. There are no silver bullets, a combination of strategies is needed. Readability, Google's code review program, exemplifies how a human-driven process can scale knowledge across an organization by enforcing best practices and code consistency. Studies show that readability has had a net positive impact on Google's engineering velocity.

## Culture - [Engineering for Equity](https://abseil.io/resources/swe-book/html/ch04.html)

> The passage discusses the importance of diversity and inclusivity in software engineering to design products that work for all users. Bias is common by default, so diverse teams are needed to consider underrepresented groups. Google has failed in the past by not properly designing for all racial groups, showing the need for more diversity in their workforce. Engineers must build multicultural capacity by understanding how their products impact different groups and considering the most difficult use cases first. They should challenge established processes that produce inequitable results and measure equity throughout their systems. While Google values diversity, they have struggled to achieve equitable outcomes, showing that values alone are not enough without proper implementation.

### Conclusion

Developing software, and developing a software organization, is a team effort. As a software organization scales, it must respond and adequately design for its user base, which in the interconnected world of computing today involves everyone, locally and around the world. More effort must be made to make both the development teams that design software and the products that they produce reflect the values of such a diverse and encompassing set of users. And, if an engineering organization wants to scale, it cannot ignore underrepresented groups; not only do such engineers from these groups augment the organization itself, they provide unique and necessary perspectives for the design and implementation of software that is truly useful to the world at large.

### TL;DRs

- Bias is the default.
- Diversity is necessary to design properly for a comprehensive user base.
- Inclusivity is critical not just to improving the hiring pipeline for underrepresented groups, but to providing a truly supportive work environment for all people.
- Product velocity must be evaluated against providing a product that is truly useful to all users. It’s better to slow down than to release a product that might cause harm to some users.

## Culture - [How to Lead a Team](https://abseil.io/resources/swe-book/html/ch05.html)

> The passages discuss effective leadership and management techniques for software engineering teams. Good managers serve their teams through humility, respect and trust. They act as servant leaders, focusing on the social and technical health of the team. They hire people smarter than themselves and give team members autonomy, opportunities for mastery and a sense of purpose to motivate them intrinsically. Tracking employee happiness and career goals helps keep teams productive. Effective managers shield their teams from outside chaos, give positive feedback and say "yes" to new ideas when possible.

### TL;DRs

- Don’t "manage" in the traditional sense; focus on leadership, influence, and serving your team.
- Delegate where possible; don’t DIY (Do It Yourself).
- Pay particular attention to the focus, direction, and velocity of your team.

## Culture - [Leading at Scale](https://abseil.io/resources/swe-book/html/ch06.html)

> Successful leaders must learn to make decisions quickly, delegate tasks, and scale their time and energy effectively as their responsibilities grow. They must identify key trade-offs, decide on a course of action, and iterate as needed. Most importantly, they must build self-sufficient teams that can solve problems without the leader's constant involvement. To scale themselves, leaders must protect their time by focusing on important tasks, delegate work to subordinates, and learn to drop lower priority tasks. They must also manage their energy through vacations, breaks, and mental health days.

95% observation and listening, and 5% making critical adjustments in just the right place.

### Important Versus Urgent

Think back to a time when you weren’t yet a leader, but still a carefree individual contributor. If you used to be a programmer, your life was likely calmer and more panic-free. You had a list of work to do, and each day you’d methodically work down your list, writing code and debugging problems. Prioritizing, planning, and executing your work was straightforward.

As you moved into leadership, though, you might have noticed that your main mode of work became less predictable and more about firefighting. That is, your job became less _proactive_ and more _reactive._ The higher up in leadership you go, the more escalations you receive. You are the "finally" clause in a long list of code blocks! All of your means of communication—email, chat rooms, meetings—begin to feel like a Denial-of-Service attack against your time and attention. In fact, if you’re not mindful, you end up spending 100% of your time in reactive mode. People are throwing balls at you, and you’re frantically jumping from one ball to the next, trying not to let any of them hit the ground.

A lot of books have discussed this problem. The management author Stephen Covey is famous for talking about the idea of distinguishing between things that are _important_ versus things that are _urgent._ In fact, it was US President Dwight D. Eisenhower who popularized this idea in a famous 1954 quote:

> I have two kinds of problems, the urgent and the important. The urgent are not important, and the important are never urgent.

This tension is one of the biggest dangers to your effectiveness as a leader. If you let yourself slip into pure reactive mode (which happens almost automatically), you spend every moment of your life on _urgent_ things, but almost none of those things are _important_ in the big picture. Remember that your job as a leader is to do things that _only you can do_, like mapping a path through the forest. Building that meta-strategy is incredibly important, but almost never urgent. It’s always easier to respond to that next urgent email.

So how can you force yourself to work mostly on important things, rather than urgent things? Here are a few key techniques:

- Delegate
- Schedule dedicated time
- Find a tracking system that works

### TL;DRs

- Always Be Deciding: Ambiguous problems have no magic answer; they’re all about finding the right _trade-offs_ of the moment, and iterating.
- Always Be Leaving: Your job, as a leader, is to build an organization that automatically solves a class of ambiguous problems—over _time_—without you needing to be present.
- Always Be Scaling: Success generates more responsibility over time, and you must proactively manage the _scaling_ of this work in order to protect your scarce resources of personal time, attention, and energy.

## Culture - [Measuring Engineering Productivity](https://abseil.io/resources/swe-book/html/ch07.html)

> Google relies heavily on data and metrics to improve engineering productivity. They created a team focused on measuring and improving productivity in an efficient manner. Before measuring productivity, they determine if the results will lead to action. They use the GSM framework to select meaningful metrics that map to their goals. They measure multiple aspects of productivity like quality, velocity, and satisfaction using both quantitative and qualitative data. The readability process study showed that while worthwhile, there were opportunities for improvement. The language teams then improved the tools and process based on the recommendations.

### Selecting Meaningful Metrics with Goals and Signals

At Google, we use the Goals/Signals/Metrics (GSM) framework to guide metrics creation.

- A _goal_ is a desired end result. It’s phrased in terms of what you want to understand at a high level and should not contain references to specific ways to measure it.

- A _signal_ is how you might know that you’ve achieved the end result. Signals are things we would _like_ to measure, but they might not be measurable themselves.
- A _metric_ is proxy for a signal. It is the thing we actually can measure. It might not be the ideal measurement, but it is something that we believe is close enough.

...

GSM encourages us to select metrics based on their ability to measure the original goals.

GSM can show us where we have measurement coverage and where we do not.

## Processes - [Style Guides and Rules](https://abseil.io/resources/swe-book/html/ch08.html)

> Google maintains strict style guides for each programming language used to manage their large codebase. The rules aim to optimize for readability, consistency and maintainability over time. Automated tools are used to enforce most rules to minimize human effort and variability. Exceptions to rules are allowed in valid cases to accommodate practical needs. The reasoning behind each rule is documented to help determine when rules need to change. New rules are proposed based on demonstrated problems in code and approved through a review process.

### TL;DRs

- Rules and guidance should aim to support resilience to time and scaling.
- Know the data so that rules can be adjusted.
- Not everything should be a rule.
- Consistency is key.
- Automate enforcement when possible.

## Processes - [Code Review](https://abseil.io/resources/swe-book/html/ch09.html)

> Code review is an essential process at Google where almost every change is reviewed before being committed. It helps ensure code correctness, catch bugs early, promote consistency, and enables knowledge sharing. Keeping reviews small and focused helps the process scale. While checking code is important, ensuring the code is understandable and maintainable over time is even more critical. The process also has psychological benefits by promoting team ownership and validating engineers' work. Automation and proper tooling help make code review scalable across a large organization.

### TL;DRs

- Code review has many benefits, including ensuring code correctness, comprehension, and consistency across a codebase.
- Always check your assumptions through someone else; optimize for the reader.
- Provide the opportunity for critical feedback while remaining professional.
- Code review is important for knowledge sharing throughout an organization.
- Automation is critical for scaling the process.
- The code review itself provides a historical record.

## Process - [Documentation](https://abseil.io/resources/swe-book/html/ch10.html)

> Documentation is important for software engineers but often neglected. Making documentation easier to write and maintain can help improve its quality. Engineers should treat documentation like code, placing it under source control and reviewing changes. While engineers do not need to be expert writers, they should identify their audience and write clearly for them. Different types of documentation serve different purposes and should be kept separate. Regularly reviewing and updating documentation can help keep it relevant and useful over time. With the right tools and processes, engineers can produce high-quality documentation that improves code comprehension and maintainability.

### Documentation Reviews

At Google, all code needs to be reviewed, and our code review process is well understood and accepted. In general, documentation also needs review (though this is less universally accepted). If you want to “test” whether your documentation works, you should generally have someone else review it.

A technical document benefits from three different types of reviews, each emphasizing different aspects:

- A technical review, for accuracy. This review is usually done by a subject matter expert, often another member of your team. Often, this is part of a code review itself.
- An audience review, for clarity. This is usually someone unfamiliar with the domain. This might be someone new to your team or a customer of your API.
- A writing review, for consistency. This is often a technical writer or volunteer.

### TL;DRs

- Documentation is hugely important over time and scale.
- Documentation changes should leverage the existing developer workflow.
- Keep documents focused on one purpose.
- Write for your audience, not yourself.

## Process - [Testing Overview](https://abseil.io/resources/swe-book/html/ch11.html)

> Testing is seen as critical to ensuring the quality and reliability of Google's products and services. Initially, Google did not emphasize testing but after some high-profile issues, testing became a priority. Google now encourages all engineers to write automated tests and has developed strategies to make tests fast, reliable and maintainable at scale. These include classifying tests by size, scope and coverage. Over time, through training, initiatives like "Testing on the Toilet" and cultural changes, Google has transformed testing into an engineering norm. Google's focus is on writing the right mix of tests to balance productivity, confidence and quality.

### TL;DRs

- Automated testing is foundational to enabling software to change.
- For tests to scale, they must be automated.
- A balanced test suite is necessary for maintaining healthy test coverage.
- “If you liked it, you should have put a test on it.”
- Changing the testing culture in organizations takes time.

## Process - [Unit Testing](https://abseil.io/resources/swe-book/html/ch12.html)

> Unit tests are an important tool for ensuring software quality, but they must be written carefully to be effective. Tests should avoid being brittle by testing public APIs instead of implementation details. They should strive for clarity by being concise, using behavior-driven names, avoiding logic, and writing clear failure messages. While some code sharing is useful, tests should favor being descriptive and meaningful over being DRY. Following these practices can help make tests more maintainable and valuable over time.

### Don’t Put Logic in Tests

Clear tests are trivially correct upon inspection; that is, it is obvious that a test is doing the correct thing just from glancing at it. This is possible in test code because each test needs to handle only a particular set of inputs, whereas production code must be generalized to handle any input.

Complexity is most often introduced in the form of logic. Logic is defined via the imperative parts of programming languages such as operators, loops, and conditionals. When a piece of code contains logic, you need to do a bit of mental computation to determine its result instead of just reading it off of the screen.

### TL;DRs

- Strive for unchanging tests.
- Test via public APIs.
- Test state, not interactions.
- Make your tests complete and concise.
- Test behaviors, not methods.
- Structure tests to emphasize behaviors.
- Name tests after the behavior being tested.
- Don’t put logic in tests.
- Write clear failure messages.
- Follow DAMP over DRY when sharing code for tests.

## Process - [Test Doubles](https://abseil.io/resources/swe-book/html/ch13.html)

> Test doubles like fakes, stubs, and mocks can help make tests run faster and more isolated. However, overusing them can lead to brittle tests that are unclear and ineffective. Real implementations are generally preferred as they provide more realistic tests with higher fidelity. Fakes are the best option when real implementations cannot be used, but they require effort to create and maintain. Stubbing and interaction testing should only be used when necessary due to their limitations. Overall, test doubles are useful tools when applied properly according to best practices.

### TL;DRs

- A real implementation should be preferred over a test double.
- A fake is often the ideal solution if a real implementation can’t be used in a test.
- Overuse of stubbing leads to tests that are unclear and brittle.
- Interaction testing should be avoided when possible: it leads to tests that are brittle because it exposes implementation details of the system under test.

## Process - [Larger Testing](https://abseil.io/resources/swe-book/html/ch14.html)

> Larger tests, like integration and end-to-end tests, are necessary to ensure the overall system works as intended. They provide higher fidelity than unit tests but are more complex and slower to run. Google uses various types of larger tests, from functional testing to A/B diff testing to chaos engineering. While unit tests are owned by individual engineers, larger tests require dedicated owners to ensure they are properly maintained and run. Careful consideration of the system under test, test data, and verification methods can improve the effectiveness of larger tests. Overall, a comprehensive test suite requires both unit tests and larger tests to achieve high test coverage.

### TL;DRs

- Larger tests cover things unit tests cannot.
- Large tests are composed of a System Under Test, Data, Action, and Verification.
- A good design includes a test strategy that identifies risks and larger tests that mitigate them.
- Extra effort must be made with larger tests to keep them from creating friction in the developer workflow.

## Process - [Deprecation](https://abseil.io/resources/swe-book/html/ch15.html)

> 1. Software systems age and become obsolete over time, requiring continued maintenance and expertise.
> 2. Deprecation is the process of removing obsolete systems in an orderly manner to reduce costs and improve efficiency.
> 3. Removing systems is difficult due to unexpected dependencies and emotional attachment to old code.
> 4. Systems can be designed for easier deprecation by making dependencies replaceable and incremental.
> 5. Deprecations range from advisory, with no deadline, to compulsory, with a removal deadline.
> 6. Compulsory deprecations require a specialized team to help users migrate away from the old system.
> 7. Deprecation warnings should be actionable and relevant to encourage users to migrate.
> 8. Deprecation projects require explicit owners, milestones, and tooling for discovery, migration, and backsliding prevention.
> 9. Removing obsolete systems improves the software ecosystem by reducing maintenance overhead and cognitive burden.
> 10. A complete deprecation process manages both social and technical challenges through policy and tooling.

> Earlier we made the assertion that “code is a liability, not an asset.” If that is true, why have we spent most of this book discussing the most efficient way to build software systems that can live for decades? Why put all that effort into creating more code when it’s simply going to end up on the liability side of the balance sheet?  
> Code itself doesn’t bring value: it is the functionality that it provides that brings value. That functionality is an asset if it meets a user need: the code that implements this functionality is simply a means to that end. If we could get the same functionality from a single line of maintainable, understandable code as 10,000 lines of convoluted spaghetti code, we would prefer the former. Code itself carries a cost—the simpler the code is, while maintaining the same amount of functionality, the better.  
> Instead of focusing on how much code we can produce, or how large is our codebase, we should instead focus on how much functionality it can deliver per unit of code and try to maximize that metric. One of the easiest ways to do so isn’t writing more code and hoping to get more functionality; it’s removing excess code and systems that are no longer needed. Deprecation policies and procedures make this possible.
