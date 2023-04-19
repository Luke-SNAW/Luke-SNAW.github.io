---
id: J5O6LCmOghKhFwQFKeoow
title: HTML
desc: ""
updated: 1681888213521
created: 1644885695231
---

## Collections

- [Explain the First 10 Lines of Twitter’s Source Code to Me](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/)
- [Tip - Use fetchpriority=high to load your LCP hero image sooner](https://addyosmani.com/blog/fetch-priority/)
- [Scripted `<INPUT>` Matching With Native Error Reporting](https://medium.com/codex/scripted-input-matching-with-native-error-reporting-8287dd7ac40a)
  - https://developer.mozilla.org/en-US/docs/Web/API/HTMLObjectElement/setCustomValidity
- [So <HGROUP> Is Back In HTML 5, And Dumb As Ever!](https://medium.com/codex/so-hgroup-is-back-in-html-5-and-dumb-as-ever-c81e00f6320d)
- [Responsive Images 101, Part 4: Srcset Width Descriptors](https://cloudfour.com/thinks/responsive-images-101-part-4-srcset-width-descriptors/)
  - width of the image sources
- [Building the main navigation for a website](https://web.dev/website-navigation/)
- [Table Like It's 2023](https://www.htmhell.dev/adventcalendar/2022/14/)
- [Two ways to safely break a long word in HTML](https://www.amitmerchant.com/two-ways-to-safely-break-a-long-word-in-html/)
  - `<wbr>`
  - `&shy;`
  - [CSS hyphens](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens)
- [Three attributes for better web forms](https://adactio.com/journal/19842)
  - inputmode, enterkeyhint, and autocomplete.
- [Jumping HTML tags. Another reason to validate your markup](https://pepelsbey.dev/articles/jumping-html-tags/)
- [HTMHell](https://www.htmhell.dev/) - A collection of bad practices in HTML, copied from real websites.
- [Modern HTML email (tables no longer required)](https://fullystacked.net/posts/modern-html-email/)
- [Can I Email](https://www.caniemail.com/clients/)

## [Amazing HTML5 Features That Just 3% of Developers Knows](https://halimshams.medium.com/amazing-html5-features-that-just-3-of-developers-knows-easy-and-surprising-ac67ff598162)

- datalist
- `<input type="file" accept=".png, .jpg">`
- details
- meter
- progress

## [Working with forms with vanilla JavaScript](https://gomakethings.com/working-with-forms-with-vanilla-javascript/)

... Form fields must have a `name` attribute to be included in the object. Otherwise, they’re skipped. The `id` property doesn’t count.

## [Those HTML Attributes You Never Use](https://www.smashingmagazine.com/2022/03/html-attributes-you-never-use/)

- The `enterkeyhint` Attribute For Virtual Keyboards
- The `title` Attribute On Stylesheets
- The `cite` Attribute For The `<blockquote>` And `<q>` Elements
- Attributes For Custom Ordered Lists
  - reversed, start, type, value
- The `download` Attribute For The `<a>` Element
- The `decoding` Attribute For The `<img>` Element
- The `loading` Attribute For The `<iframe>` Element
- The `form` Attribute For Form Fields
- The `cite` And `datetime` Attributes For Deletions/Insertions
- The `label` Attribute For The `<optgroup>` Element
- The `imagesizes` And `imagesrcset` Attributes For Preloading Responsive Images
- The `crossorigin` attribute which can apply to multiple elements, including `<audio>`, `<img>`, `<link>`, `<script>`, and `<video>`, providing support for cross-origin resource sharing (CORS);
- The `title` attribute for `<dfn>` and `<abbr>`;
- The new `disablepictureinpicture` attribute for the `<video>` element;
- The `integrity` attribute for scripts, which helps the browser verify that the resource hasn’t been improperly manipulated;
- The `disabled` attribute for the `<fieldset>` element, to easily disable multiple form elements simultaneously;
- The `multiple` attribute for email and file inputs.

## template

> https://news.ycombinator.com/item?id=33089975

`<template>` is special, very different from display: none; and definitely has a few advantages:

- The elements in it are parsed into a different document and are inert until cloned or adopted into the main document. Images don't load, scripts don't run, styles don't apply, etc. This is very important.

- The content model validation is turned off, so a `<template>` can contain a <td\>

- Mutation observers and events are not fired for parsed content.

- The `<template>` element itself can appear anywhere, including restricted content elements like <table\>

- Other HTML processing libraries generally know to ignore `<template>`, unlike other content just hidden with CSS.

This makes parsing faster and guaranteed to have no side effects, and conveys the correct semantics to the browser and tools.

### Semantics

In addition - “template” also conveys correct semantics to the other developers working on the codebase. If I see an html at the bottom with “display: none” it’s very possible that the intended usage is to leave it there and set “display: block”, ie a modal. “display: none” doesn’t convey “clone me”, but “template” does.
