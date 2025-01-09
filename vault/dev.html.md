---
id: J5O6LCmOghKhFwQFKeoow
title: HTML
desc: ""
updated: 1736382380898
created: 1644885695231
---

## Collections

- [Explain the First 10 Lines of Twitter’s Source Code to Me](https://css-tricks.com/explain-the-first-10-lines-of-twitter-source-code/)
- [Tip - Use fetchpriority=high to load your LCP hero image sooner](https://addyosmani.com/blog/fetch-priority/)
- [So `<HGROUP>` Is Back In HTML 5, And Dumb As Ever!](https://medium.com/codex/so-hgroup-is-back-in-html-5-and-dumb-as-ever-c81e00f6320d)
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
- [Be Careful Using ‘Menu’](https://adrianroselli.com/2023/05/be-careful-using-menu.html)
- [Stop Using ‘Pop-up’](https://adrianroselli.com/2021/07/stop-using-pop-up.html)
- [Effortlessly Support Next Gen Image Formats](https://dennisforbes.ca/articles/jpegxl_just_won_the_image_wars.html)
  - use the `picture` element
- [SSMPL : A Wishful Thinking HTML Replacement Proposal](https://medium.com/codex/ssmpl-a-wishful-thinking-html-replacement-proposal-1e11e8d86bf6)
- [A Blog Post With Every HTML Element](https://www.patrickweaver.net/blog/a-blog-post-with-every-html-element/)
  - `<base>`
- [PSA: Add dir="auto" to your inputs and textareas.](https://mough.xyz/312/psa-add-dir-auto-to-your-inputs-and-textareas)
- [Build a Better Mobile Input](https://better-mobile-inputs.netlify.app/)
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#%3Cinput%3E_types
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inputmode
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete
- [Youtube video embedding harm reduction](https://dustri.org/b/youtube-video-embedding-harm-reduction.html)
  ```html
  <iframe
    credentialless
    allowfullscreen
    referrerpolicy="no-referrer"
    sandbox="allow-scripts allow-same-origin"
    allow="accelerometer 'none'; ambient-light-sensor 'none'; autoplay 'none'; battery 'none'; browsing-topics 'none'; camera 'none'; display-capture 'none'; domain-agent 'none'; document-domain 'none'; encrypted-media 'none'; execution-while-not-rendered 'none'; execution-while-out-of-viewport ''; gamepad 'none'; geolocation 'none'; gyroscope 'none'; hid 'none'; identity-credentials-get 'none'; idle-detection 'none'; local-fonts 'none'; magnetometer 'none'; microphone 'none'; midi 'none'; otp-credentials 'none'; payment 'none'; picture-in-picture 'none'; publickey-credentials-create 'none'; publickey-credentials-get 'none'; screen-wake-lock 'none'; serial 'none'; speaker-selection 'none'; usb 'none'; window-management 'none'; xr-spatial-tracking 'none'"
    ,
    csp="sandbox allow-scripts allow-same-origin;"
    width="560"
    height="315"
    src="https://www.youtube-nocookie.com/embed/jfKfPfyJRdk"
    title="lofi hip hop radio 📚 - beats to relax/study to"
    frameborder="0"
    loading="lazy"
  ></iframe>
  ```
- [State of HTML 2023](https://2023.stateofhtml.com/)
- [EntityCode](https://entitycode.com/)
- [I’ve Been Doing Blockquotes Wrong](https://css-irl.info/ive-been-doing-blockquotes-wrong/)
- [Clarifying the Relationship Between Popovers and Dialogs](https://css-tricks.com/clarifying-the-relationship-between-popovers-and-dialogs/)
  - Popover is an umbrella term for any kind of on-demand popup.
  - Dialog is one type of popover — a kind that creates a new window (or card) to contain some content.
    - Modal: A dialog with an overlay and focus trapping
    - Non-Modal: A dialog with neither an overlay nor focus trapping
    - Alert Dialog: A dialog that alerts screen readers when shown. It can be either modal or non-modal.
- [Exploring the HTML5 <a> Tag Ping Attribute](https://jsdev.space/html-ping-attribute/)
- [Control the Viewport Resize Behavior on mobile with `interactive-widget`](https://htmhell.dev/adventcalendar/2024/4/)
- [The underrated <dl> element](https://htmhell.dev/adventcalendar/2024/26/)
- [The search input: They almost got it right](https://htmhell.dev/adventcalendar/2024/24/)
- [Relatively New Things You Should Know about HTML Heading Into 2025](https://frontendmasters.com/blog/bone-up-html-2025/)
- [The `<details>` and `<summary>` elements are getting an upgrade](https://blog.stephaniestimac.com/posts/2024/10/html-details-and-summary-update/)
- [Use "translate" to turn off element translations](https://www.stefanjudis.com/today-i-learned/non-translatable-html-elements/)
  - `translate="no"` attribute

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

## Forms

- [Forms 101: More tags useful in forms](https://thevalleyofcode.com/forms/5-more-tags-useful-in-forms) - `<fieldset>`, `<legend>`

## Inputs

- [Scripted `<INPUT>` Matching With Native Error Reporting](https://medium.com/codex/scripted-input-matching-with-native-error-reporting-8287dd7ac40a)
  - https://developer.mozilla.org/en-US/docs/Web/API/HTMLObjectElement/setCustomValidity
- [Build an OTP input field](https://phuoc.ng/collection/html-dom/build-an-otp-input-field/)
- [Form fields: File input fields](https://thevalleyofcode.com/form-fields/5-file-input-fields)
- [Form fields: Autocompleting form fields](https://thevalleyofcode.com/form-fields/8-autocompleting-form-fields)
- [Fine-tuning Text Inputs](https://garrettdimon.com/journal/posts/fine-tuning-text-inputs)

## [How to Use Responsive HTML Video (...and Audio!)](https://scottjehl.com//posts/using-responsive-video/)

```html
<video>
  <source media="(min-width: 2000px)" src="large.webm" type="video/webm" />
  <source media="(min-width: 2000px)" src="large.mp4" type="video/mp4" />
  <source media="(min-width: 1000px)" src="medium.webm" type="video/webm" />
  <source media="(min-width: 1000px)" src="medium.mp4" type="video/mp4" />
  <source src="small.webm" type="video/webm" />
  <source src="small.mp4" type="video/mp4" />
</video>
```
