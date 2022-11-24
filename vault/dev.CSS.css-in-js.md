---
id: fk33k4a33a4ttaiu7xj0fzx
title: CSS in JS
desc: ""
updated: 1669177052485
created: 1666654022201
---

## [A Unified Styling Language](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660)

## [Why We're Breaking Up with CSS-in-JS](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b)

Sam Magura - software engineer at [Spot](https://www.spotvirtual.com/) and the 2nd most active maintainer of [Emotion](https://emotion.sh/), a widely-popular CSS-in-JS library for React

### [Bad](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#the-bad)

- CSS-in-JS adds runtime overhead.
- CSS-in-JS increases your bundle size.
- With CSS-in-JS, there's a lot more that can go wrong, especially when using SSR and/or component libraries.
  - Multiple instances of Emotion get loaded at once.
  - Component libraries often do not give you full control over the order in which styles are inserted.
  - ...

### Comments

#### BEM

The problem with BEM isn't BEM itself, it's getting your coworkers, new developers and external agencies to understand and follow the syntax

#### Victor Vincent

I honestly disagree both with the article and some of the comments here. I'd like to address the first of the article. (Respect for the article, it does have valid points and concerns and it's well put together).

I have a lot of experience with a lot of solutions in a lot of different scenarios. A new solution to a current one can always feel better, because it excells in the painpoints the older solution had, those are the problems we're trying to address with the change, but that doesn't necessarly mean that the old solution wasn't performing better on other areas. For me CSS-in-JS (with optional static extraction and/or 0 runtime) is the perfect way, because it addresses many different issues I had through the years the most.

There are solutions that can static extract with 0 runtime and they are able to handle dynamic props using CSS variables, so at the end it's 0 runtime and only class names. I see you mentioned this at the end also, but there are some misconceptions here. The mentioned "problems" are not necessarly unique to 0 runtime libraries, there are solution which aren't suffering from those pain points.

---

##### [The Bad](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#the-bad)

1. **CSS-in-JS adds runtime overhead:** there are many compile time options that have 0 runtime using multiple different kinds of static extraction strategies.
2. **CSS-in-JS increases your bundle size:** Just like the above.
3. CSS-in-JS clutters the React DevTools. Static extracted styles will replace your styles with classNames and/or CSS variables. No clutter (not necessarily true to all solutions).

##### [The Ugly](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#the-ugly)

1. **Frequently inserting CSS rules forces the browser to do a lot of extra work:** static extraction solves this problem.
2. **With CSS-in-JS, there's a lot more that can go wrong, especially when using SSR and/or component libraries:** statically extracted, nothing can really go wrong, becuase there is nothing being done in JS.

##### [Performance](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#performance)

No JS involved, I don't want to go into it more deeply than that.

**Styles are still inserted when a component mounts for the first time...** Not necessarily true. It's really based on the extraction strategy you choose. You can choose to extract everything in a single file. You will end up with the same "problem" using CSS Modules if you don't static extract into a single file btw.

Inline styles are known to cause suboptimal performance when applied to many elements... They can, but it's nothing you should worry about, especially that it's just CSS variables. The overhead of loading an external stylesheet and handling dynamic cases with code (conditions, className concat, etc) will actually perform worse by adding more overhead imo.

---

##### [BEM](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#bem)

I'm incredibly against it. 1 HUGE benefit of CSS-in-JS (inline) is that you no longer need to think of naming and organizing your selectors/styles. Best conventions are the ones that are not needed ;) Naming things, especially using BEM is a huge overhead during development, it significantly interrupts your flow.

##### [CSS Modules](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#css-modules)

- Separate Stylesheets per module still need to be loaded dynamically if you want to bundle split. If you extract per component: extra request + extra style node; if you bundle: extra js size, runtime insert, extra style node.
- Extract into 1 stylesheet: essentially same as a 0 runtime, static extracted CSS-in-JS with the overhead of maintaining styles separately with a separate system and/or language, with a separate config system (often duplicated to access values in js also) for no extra benefit/reason.
- Naming stuff shouldn't be necessary. Less convention ftw!
- "Separation of concerns" is what they say when putting CSS in a separate file. My personal take on this, they are right but apply it wrong. Both JSX and your styles are the same concern: view. Having deeply close together helps you understand and see immediately what your layout does, how it works, how it looks, just by looking there at the code. Separate them will cause slowdowns during development, you need to jump through several files just to check what is `style.container` actually is. Having them inline during development is a huge productivity boost for me.

##### [CSS-in-JS with runtime](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#cssinjs-with-runtime)

I'm not against runtimes tbh. I do have a fairly large social site with millions of contents and several multimedia types and complex user features. The complete client side codebase is 25MB in total bundle size (no gzip), yet my initial JS for a single page is 200k (no gzip), which is mostly React, it uses Styled-Components with CCSS and uses a custom, single file SSR pipeline (no Next or whatsoever) with an isomorphic codebase. I have my Lighthouse scores at 96-100 points. Could be faster w/o runtime? Yes. Would my users notice anything from it? Not really. So why would I choke myself by using a less productive/comfortable solution? :)

##### [Extract on your own](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b#extract-on-your-own)

It's not a too hard thing to write a Babel plugin that extracts the static parts of your `css` prop however you want. By that you save a lot of time spent on refactoring to a new solution on a large codebase.

#### Tom Raviv

We've reached a lot of similar conclusions here at Wix.com too. Our first HTML editor (and following versions) used an in-house CSS-in-JS solution, but eventually the performance costs just got too high.

I'm the team leader working on [Stylable](http://stylable.io/), our solution to this problem space. Stylable is a CSS superset that adds a type-system, automates the BEM scoping part, and provides templating tools to improve developer experience and reduce code duplications.

We've been battle testing it internally at Wix for several years now (used in over 50+ million sites), and are now beginning to reach out to new users and to build our community. We'd love to talk if this sounds interesting to you.

---

Glad you liked what you saw, I'll elaborate a bit on our approach.

Sass and CSS modules are both well proven and battle tested solutions that we absolutely love, but have their downsides too. I would say the most notable differences between Sass modules and Stylable are the following:

- Sass is oriented for CSS and document based projects in its core. CSS modules tries to bend Sass' approach to be more component oriented. Stylable was built with components being treated as first class citizens, allowing stylesheets or their parts to be utilized by our module system in various ways.
- The namespacing that CSS modules provides is there to prevent collisions, and not improve readability or debugging experience (unlike BEM, which in my opinion does both). While Stylable combines both approaches, opting to use a configurable automatic BEM-like namespacing for its output.
- At Wix a single component can have many drastically different use cases - to provide flexibility for such components, Stylable encourages treating your component styling as just another part of its API. Each stylesheet exposes its inner parts allowing to customize and theme any part of the application easily from the outside.
- Stylable adds a type-system to CSS (currently, only at the selector level, with more of the language to come). This allows defining inheritance and relationships across stylesheets, allowing our custom language service a much better understanding of the code, resulting in advanced diagnostics, auto-completions, code navigation and other language features.
- Lastly Stylable namespaces a lot more than just class names, also namespacing keyframes, custom properties, layers and (very soon) container queries to keep you safe from leaks or collisions.

#### Jake Lane

Hey lead on the Compiled CSS-in-JS project here 👋. Just thought I'd clear up some aspects of the Compiled library and our future roadmap.

For the components that are included at runtime, those are intended for use in development only. For production use, we're going to recommend people use stylesheet extraction which moves all the CSS into an atomic stylesheet. That'll mean that all the runtime react components will be stripped out. We haven't fully made this clear in documentation yet as we're still ironing out some issues with dev experience.

The dynamic prop support is intended as a migration feature to allow people to adopt compiled without fully re-writing their code. We required this as part of our migration journey at Atlassian. It does end up with non-optimal performance this way so we're we'll be building more tooling around writing fully static CSS.

At Atlassian, we did a deep dive into whether to use CSS modules or continue with CSS-in-JS. We did end up selecting Compiled as our best path forward for a few reasons, but to simplify:

- Devs are familiar with CSS-in-JS and we can migrate without too much difficulty to a build time CSS-in-JS library. It didn't seem like a good use of time to re-write all our CSS.
- We find CSS-in-JS works really well for our design system and the amount of CSS we have at Atlassian. We'd have a lot of new challenges around ensuring code quality, encapsulation, and reusability without it.
- We can end up with the ~same performance characteristics of CSS modules with Compiled on the CSS prop - possibly better with tooling to make better use of atomic CSS.

#### Martin

Thank you for sharing your insights. I agree (judging from my current view point of past and present projects and experiences) that CSS-modules paired with SASS/SCSS are the cleanest and sanest approach to component styles.  
But I would say it also checks the third point of your three-point list of good things (locally-scoped styles, co-location, JavaScript variables in styles):  
You can share values between styles and js code, in both directions, during build time and during runtime. Each scenario requires its own mechanism (I want to cover this in a blog post but don't know when I will find the time), here is the gist of it:

- from css to js, build time: use `:export`
- from css to js, runtime: use `getComputedStyle()`
- from js to css, build time: use `sass-loader additionalData option`
- from js to css, runtime: use `element.style.setProperty('--some-prop', value)`

In my webpack config I share the colors (in a \*.ts file) with my styles by generating variables like `$primary-main`:

```js
import { colors } from './colors';
import { jsToScss } from './js-to-scss';

{
  loader: 'sass-loader',
  options: {
    additionalData: jsToScss(colors),
  },
},
```
