---
id: 7tPeWrJHQmeiMg4HWoymw
title: Accessibility
desc: ""
updated: 1716257720364
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
- [Improving Web Accessibility with Semantic HTML and Testing Techniques and Tools](https://www.infoq.com/news/2023/04/web-accessibility/)
- [`display: contents` considered harmful](https://ericwbailey.website/published/display-contents-considered-harmful/)
- [Don't Use Fixed CSS height or width on Buttons, Links, or Any Other Text Containers](https://ashleemboyer.com/blog/don-t-use-fixed-css-height-or-width-on-text-containers)
  > Despite some web design tools specifying CSS `height` values for elements like buttons, setting `height` or `max-height` can actually put you at risk for failing [WCAG 2.2 Success Criterion 1.4.4 Resize Text](https://www.w3.org/TR/WCAG22/#resize-text).
- [Accessible notifications with ARIA Live Regions (Part 1)](https://www.sarasoueidan.com/blog/accessible-notifications-with-aria-live-regions-part-1/)
- [Accessible notifications with ARIA Live Regions (Part 2)](https://www.sarasoueidan.com/blog/accessible-notifications-with-aria-live-regions-part-2/)
- [Designing better target sizes](https://ishadeed.com/article/target-size/)
- [You Want border-color: transparent, Not border: none](https://frontendmasters.com/blog/you-want-border-color-transparent-not-border-none/)
  - `@media (forced-colors: active)`

## Text

- [Lost in Translation: Tips for Multilingual Web Accessibility](https://benmyers.dev/blog/multilingual-web-accessibility/)
- [A Brief Note on Highlighted Text](https://adrianroselli.com/2024/05/a-brief-note-on-highlighted-text.html)
  > If you plan to style text highlighted by the browser, you must give it sufficient contrast — 3:1 for the highlight block against its background and (probably) 4.5:1 for the text within that highlighted block against that background.
- [Rethinking Text Resizing on Web](https://medium.com/airbnb-engineering/rethinking-text-resizing-on-web-1047b12d2881)
  - Airbnb has made improving web accessibility a priority, focusing on the WCAG 1.4.4 Resize Text guideline. This guideline is important for users with low vision, as it requires web content to be maintained when text is scaled 200%.

## [prefers-reduced-motion](https://news.ycombinator.com/item?id=31765773)

The `prefers-reduced-motion` feature is explicitly[^1] intended to accommodate people with vestibular motion disorders, which are common above age 40.[^2]

[^1]: https://drafts.csswg.org/mediaqueries-5/#prefers-reduced-motion/
[^2]: https://vestibular.org/article/what-is-vestibular/about-vestibular-disorders/

## [Unchain My Inaccessibly-Labelled Heart](https://css-tricks.com/unchain-my-inaccessibly-labelled-heart/)

```html
<h2 id="article1-heading">All About Dragons</h2>
<p>I like dragons. Blah blah blah blah blah.</p>
<p>
  <a
    id="article1-read-more"
    aria-labelledby="article1-read-more article1-heading"
  >
    Read more
  </a>
</p>
```

What happens there is a screenreader will replace the existing semantic label between the link tags and use the content from both elements and announce them together as a single string of text:

```html
Read more All About Dragons
```
