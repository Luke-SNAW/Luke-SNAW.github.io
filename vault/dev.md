---
id: ZbdkdApFqLdks4Moq92R9
title: Dev
desc: ""
updated: 1698036939551
created: 1644451403760
---

## Collections

- [Google Style Guides](https://google.github.io/styleguide/)
- [Hibernate should be to programmers what cake mixes are to bakers](https://vimeo.com/28885655) - This is a talk about the problems of creating convoluted abstractions and how not understanding what happens underneath makes things more complex instead of simplifying them.
- [How to transfigure wireframes into HTML](https://www.htmhell.dev/adventcalendar/2022/1/)
- [Does WWW still belong in URLs?](https://css-tricks.com/does-www-still-belong-in-urls/)
  - WWW-less domain concern 1: Leaking cookies to subdomains
  - WWW-less domain concern 2: DNS headaches
  - [WWW-less benefits](https://css-tricks.com/does-www-still-belong-in-urls/#aa-www-less-benefits)
  - [WWW benefits](https://css-tricks.com/does-www-still-belong-in-urls/#aa-www-benefits)
- [roadmap.sh](https://roadmap.sh/) - Community driven roadmaps, articles and resources for developers
- https://github.com/sindresorhus/awesome - 😎 Awesome lists about all kinds of interesting topics
- [test && commit || revert](https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864)
- [Limbo: Scaling Software Collaboration](https://medium.com/@kentbeck_7670/limbo-scaling-software-collaboration-afd4f00db4b)
  > Sort commits into “couldn’t possibly cause problems” (you’ll be mostly right) and “might cause problems”. Treat them differently. Rearrange your workflow so you have mostly “couldn’t possibly cause problems” commits.
- [Software effort estimation is mostly fake research](https://shape-of-code.com/2021/01/17/software-effort-estimation-is-mostly-fake-research/)
  > from [HK news](https://news.ycombinator.com/item?id=36350632)
  >
  > - It's not fake research. It's actually quite an established science in the 24 years I've been doing it.
  > - Take your first guess, double it, double it again if the stakeholder is a poser, add 20% per developer less experience than you, subtract 10% for the features you're going to essentially copy paste, add 15% for sick leave (browsing HN) and then double it for every question you have that are unresolved and divide it by the room temperature multiplied by the amount of people with mechanical keyboards.
  > - That gives you roughly the right estimate for any job, until the next sprint.
- [Nobody ever paid me for code](https://www.bitecode.dev/p/nobody-ever-paid-me-for-code)
  - Don't:
    > We should migrate from SQLite to Postgress. We are getting concurrency errors because too many processes are trying to write orders at the same time and it's not something we can queue because it needs real-time feedback.
  - Do:
    > Some users are getting errors when too many of them order at the same time. We tried workarounds but they make for a bad shopping experience. This is not a trivial change to do. We are currently working on X, but I think this is more urgent. I advise we suspend work on X so that I can evaluate how much we need to do, and then plan for this change.
- [The Worst Programmer I Know](https://dannorth.net/2023/09/02/the-worst-programmer/)
  > Tim wasn’t delivering software; Tim was delivering a team that was delivering software.
- [Measuring developer productivity? A response to McKinsey](https://tidyfirst.substack.com/p/measuring-developer-productivity)
- [Some notes on Local-First Development](https://bricolage.io/some-notes-on-local-first-development/)
  - [cr-sqlite](https://github.com/vlcn-io/cr-sqlite) - Convergent, Replicated, SQLite - "It's like Git, for your data."

### re:Work

[re:Work](https://rework.withgoogle.com/) is a collection of practices, research, and ideas from Google and others to help you put people first.

- [Goal Setting](https://rework.withgoogle.com/subjects/goal-setting/)
  Set goals to align efforts, communicate objectives, and measure process.
- [Hiring](https://rework.withgoogle.com/subjects/hiring/)
  Make better hiring decisions through job descriptions, structured interviewing, hiring committees, and more.
- [Innovation](https://rework.withgoogle.com/subjects/innovation/)
  Learn to build the skills for innovation and make it a part of your workplace.
- [Learning & Development](https://rework.withgoogle.com/subjects/learning-development/)
  Empower your employees to grow and develop by making learning part of everyone’s job.
- [Managers](https://rework.withgoogle.com/subjects/managers/)
  Identify what makes a great manager and offer feedback and development opportunities.
- [People Analytics](https://rework.withgoogle.com/subjects/people-analytics/)
  Make informed, objective people decisions using science and data.
- [Teams](https://rework.withgoogle.com/subjects/teams/)
  Examine team effectiveness and how to foster psychological safety.
- [Unbiasing](https://rework.withgoogle.com/subjects/unbiasing/)
  Reduce the influence of unconscious bias by educating, measuring, and holding everyone accountable.

## Debug

- [Car allergic to vanilla ice cream](http://www.cs.cmu.edu/~wkw/humour/carproblems.txt)
- [We can't send email more than 500 miles](http://web.mit.edu/jemorris/humor/500-miles)
  - https://news.ycombinator.com/item?id=23777700

## Estimation

### [Pushing for a lower dev estimate is like negotiating better weather with a meteorologist](https://smartguess.is/blog/your-estimate-is-less-than-that/)

The article discusses how stakeholders often push development teams to provide lower estimates than initially given, without valid reasons for why the effort would decrease.

- Estimates are based on teams' experience and data, not external opinions.
- Estimates cannot be pushed lower without new information.

The better approach is to have a discussion around budget, uncertainties, and prioritization in order to deliver parts of the feature in a timely manner.

- Teams are encouraged to ask stakeholders if they would tell a meteorologist their forecast is wrong, highlighting that estimates rely on expertise, not opinions.
- With open communication around constraints and tradeoffs, teams can set appropriate expectations and deliver value along the way.
