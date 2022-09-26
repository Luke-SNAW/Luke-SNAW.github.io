---
id: 4obagyb1i3h3unfou3qdvn2
title: MR (PR) submission standard
desc: ""
updated: 1664154156011
created: 1647307459487
---

https://news.ycombinator.com/item?id=30578033

# paradite

I'm a senior frontend engineer doing a lot of code reviews and my team loves my MR (PR) submission standard:

- Require the author to attach screenshots of the feature in a markdown table format showing the before and after comparison. This is enforced using a MR template.
- Require the author to attach screen recording for complex user interactions.

Overall effect is that it saves everyone's time.

- The author has to verify that the feature works anyway, so taking screenshots / recordings doesn't take much additional efforts.
- The reviewer can focus on code itself instead of checking whether the code works.
- Easy for both parties to spot design and UX issues/regressions visually.

## bradwood

Code review != Testing.
A lot of people conflate these IMHO. Code review should not really be about whether it "works" or not. That's what tests are for.

Code reviews are about checking for code complexity, good use of abstractions, readability, etc.
