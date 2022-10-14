---
id: 7f3kvsw4fcm0zdpmziip1r1
title: Bdd in 2020
desc: ''
updated: 1665622780916
created: 1665620096869
---

> https://alisterbscott.com/2020/05/28/bdd-in-2020/

The author have found this process seems to work really well for modern software development in 2020:

1. Every new piece of work has a kick-off discussion with the product owner, the tester and the developer(s)
2. The tester usually facilitates this meeting and aims to produce [written lightweight documentation](dev.example-of-lightweight-feature-documentation.md) during the discussion containing the following information: background info, scenarios, business rules, examples (edge cases), questions and decisions.
3. This documentation is enough for development work to begin, and the tester to plan how they’ll test it.
4. The documentation is updated as work progresses: questions arise and decisions are made (and documented).
5. The developer(s) is/are responsible for making sure there is automated test coverage for these business rules at the cheapest level of testing, these are typically automated unit and/or automated integration tests. These aren’t written in business readable language, they’re test code alongside production code.
6. The developer also needs to ensure any existing automated end-to-end (e2e) tests are updated for the work that is happening – CI builds highlight these impacts/failures.
7. When the feature, or a working part of the feature, is ready for testing the developer and tester do a quick handover/walk-through making sure what was done is what was discussed.
8. The tester uses the lightweight documentation as a basis for their testing, but adds extra rigour in testing edge cases/unknowns, other impacted areas, different browsers, performance, and devices and anything else they think could be risky.
9. Bugs that are found and determined by the product owner to be crucial are fixed immediately, some bugs become “fast follows” which are the next thing to ship. Some bugs aren’t fixed.
10. The tester gives a walk-through to the product owner and sometimes UX designer to make sure what’s been done is acceptable – if the feature is new/risky it’s launched to a subset of customers and can be disabled at a flick of a toggle.
11. When an entirely new feature is added to the system and it’s important enough to warrant an (expensive) automated e2e test – the tester works on adding that in amongst their other work. This isn’t a blocker to release and provides a safety blanket for future changes. This isn’t a comprehensive specification of the system – it’s an e2e automated test that covers a business critical flow over multiple moving parts and again doesn’t need to be business readable.
12. The specifications/documentation lives on in a wiki page and can be referred back to when testing future changes to this feature, or when support tickets or bugs are found in production.
