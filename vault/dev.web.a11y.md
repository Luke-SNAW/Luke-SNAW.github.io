---
id: 7tPeWrJHQmeiMg4HWoymw
title: Accessibility
desc: ""
updated: 1669164683651
created: 1644817740456
---

## Collections

- [레진 웹 접근성 가이드라인](https://github.com/lezhin/accessibility)
- [A11y Automation Tracker > Potential Violations](https://a11y-automation.dev/violations)
- [Accessibility, assistive technology, and JavaScript](https://gomakethings.com/accessibility-assistive-technology-and-javascript/)
  - [A quick note about macOS](https://gomakethings.com/accessibility-assistive-technology-and-javascript/#a-quick-note-about-macos) - On macOS, keyboard focus navigation is off by default. Chromium browsers (like Chrome and Edge) automatically support keyboard navigation anyways, but Firefox and Safari honor the system preferences.
- [Please, stop disabling zoom](https://www.matuzo.at/blog/2022/please-stop-disabling-zoom/)
- [5 takeaways from screen reader usability interviews](https://jessbudd.com/blog/screen-reader-usability-testing-observations/)
  - Usually when we think of alt text, we think "What is this a picture of?" - but in the case of links where the only content is an image, the alt text needs to describe the function of that link. Not the image itself.
- https://webhint.io/docs/user-guide/hints/accessibility/
- [Using ARIA: Roles, states, and properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)
- [Accessibility Solutions](https://a11y-solutions.stevenwoodson.com/)
- 👑 [GOV.UK Design System > Accessibility](https://design-system.service.gov.uk/accessibility/) explains how the team works to ensure the Design System and Frontend are accessible.

## [prefers-reduced-motion](https://news.ycombinator.com/item?id=31765773)

The `prefers-reduced-motion` feature is explicitly[^1] intended to accommodate people with vestibular motion disorders, which are common above age 40.[^2]

[^1]: https://drafts.csswg.org/mediaqueries-5/#prefers-reduced-motion/
[^2]: https://vestibular.org/article/what-is-vestibular/about-vestibular-disorders/
