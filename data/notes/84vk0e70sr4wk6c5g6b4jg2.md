
> https://elisehe.in/2022/10/16/attribute-selectors

I’m a long-time [BEM](https://getbem.com/introduction/) user. The double underscore creeps into my code even when selector collision isn’t an issue. I don’t think it’s BEM, specifically, that I’m drawn to (it just happened to be the methodology I first learned about and grew used to). It’s the fact that a methodology, any methodology, adds structure and semantics to HTML class naming where inherently there isn’t one.

It’s why I always feel a bit lost when using CSS modules or CSS-in-JS libraries. What do you _mean_ I can name my classes or styled components whatever I want? It’s not unheard of for people to [use BEM _with_ CSS modules](https://medium.com/trabe/using-bem-conventions-in-css-modules-leveraging-custom-webpack-loaders-fd985f72bcb2). This might seem silly  —  they solve the same problem, after all. But perhaps it shows that rigid class naming conventions are attractive beyond their power to avoid collisions. For better or worse, they allow us to gauge the role of each selector from the stylesheet alone.

In our preoccupation with classes, it’s easy to think of them as the default selector. Historically, when people have talked about targeting elements by their attributes, it’s been in the context of neat tricks or one liners. You make a mental note to use `a[href^=https://specific-domain.com]` the next time you want to use pink underlines for each link to one specific domain, and promptly forget about it forever. Or, to give a more practical example, attribute selectors have been recommended as a kind of linter or debugger for invalid HTML (`img:not([alt]) { border: 1rem solid red; }`).

More recently, the idea to treat attribute selectors on par with classes as first-class citizens has been proposed more widely. We’re no longer talking about edge cases, but challenging the very defaultness of classes, all while not giving up that sense of structure that many of us look for in CSS naming conventions.

The two articles that have stood out for me are:

- [_Represent state with HTML attributes not class names_](https://www.aleksandrhovhannisyan.com/blog/represent-state-with-html-attributes-not-class-names/) by Aleksandr Hovhannisyan
- [_CSS classes considered harmful_](https://www.keithcirkel.co.uk/css-classes-considered-harmful/) by Keith Cirkel

Aleksandr and Keith both advocate for attribute selectors instead of class names, but while Aleksandr describes the more conservative approach of preferring attribute selectors where one already exists on the HTML element, Keith goes a step further and proposes adding your own `data-*` attribute instead of another class when you need something to hook into.

Let’s look at both more closely.

## Representing native state

Aleksandr Hovhannisyan makes the case that classes are too often used to style different states or variants of an element, where that state might  — or, critically, *should* —  already be semantically represented by other properties such as ARIA attributes or pseudo selectors.

No-one objects that you should prefer `input[disabled]` over `input.is-disabled`, because most of the time it’s unnecessary to add that class name manually when you already have an attribute selector to hook into. We tend to forget that there are plenty of other native ways to represent state that we should be using anyway  — namely ARIA attributes. (Though we don’t get them for free as we do with pseudo classes like `:hover`, `:checked` or `:focus`.)

Compare the following. Using modifier classes:

```html
<a href="/page2/" class="nav-link nav-link--is-active">Page 2</a>

<style>
  .nav-link.nav-link--is-active {
  }
</style>
```

Using ARIA attributes:

```html
<a href="/page2/" class="nav-link" aria-current="page">Page 2</a>

<style>
  .nav-link[aria-current="page"] {
  }
</style>
```

The crucial point here is that `aria-current="page"` should be included regardless of the styling needs of an active link, and I can’t think of a reason why we should ever add an extra class where the state can already be selected for in a different way. Worst case scenario, this would mean you’re implementing state management twice.

This promotes an a11y-first mindset — if there is no attribute or pseudo selector available to represent the state we wish to style, should we add one? Are we using the right HTML element? We are forced to go through a mental flow chart of native, semantic HTML and CSS features we could tap into before resorting to classes.

I’m reminded of [Testing Library’s guiding principle](https://testing-library.com/docs/queries/bytestid/) to only ever reach for the `testId` element selector when you’ve ruled out all other, more semantic querying options. What if we treated classes a bit like test IDs, appreciating them as a robust, generic fallback option that we can reach for when there are no other appropriate, semantic attributes available on the element?

Other people have covered thoroughly the many examples of using ARIA attributes and other semantic selectors for styling, so I won’t cover any more here. Do have a read if you’re interested:

- [_Style with stateful, semantic selectors_](https://benmyers.dev/blog/semantic-selectors/) by Ben Meyers
- [_User facing state_](https://css-tricks.com/user-facing-state/) by Scott O’Hara
- [_Using CSS to enforce accessibility_](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html) by Adrian Roselli

## Representing custom state

Aleksandr Hovhannisyan explains well how the use of attribute selectors can result in better UX. I find it a satisfying coincidence that Keith Cirkel reaches the same conclusions coming from a place of developer experience. He highlights the DX issue with classes:

> Classes, being a list of arbitrary strings, have no key-values, no private state, no complex types (which also means IDE support is quite limited) and rely on custom DSLs like BEM just to make them slightly more usable. We keep trying to implement parameters into a `Set<string>` when what we want is a `Map<string, T>`. ([Keith Cirkel](https://www.keithcirkel.co.uk/css-classes-considered-harmful/))

There’s a well-known fundamental principle in software engineering: [**Make impossible states impossible**](https://kentcdodds.com/blog/make-impossible-states-impossible)[1](https://elisehe.in/2022/10/16/attribute-selectors#fn:impossiblestates).

My impression from Keith’s article is that, at its core, this is the principle that class selectors violate. An element’s classes are never guaranteed to reflect their state (nothing prevents you from adding the class `button--loading` to a button that isn’t, in fact, loading), and classes that are used to represent one of many mutually exclusive variants are never guaranteed to be mutually exclusive (nothing prevents you from adding `button--primary` and `button--secondary` to the same button).

I love how Keith frames this as a type issue. As an example, we can look at the naming of some of [Tailwind’s utility classes](https://tailwindcss.com/docs/responsive-design): using a colon to group related sets of classes could be taken as an attempt to signal mutual exclusivity. `<div class="sm:w-80 sm:w-96">` should sound the alarm bells because the offending logic is immediately visible in the naming.

Keith reminds us that attribute selectors can be some of the most versatile in our CSS toolbelt  — `data-*` attributes, combined with the [rich variation in CSS attribute selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors), could be used to capture strings as well as lists — and he encourages us to embrace them. Here lies the difference between his and Aleksandr’s suggestions: it’s not about merely using the native attributes already present on the element, it’s about adding custom ones — instead of classes — when they’re not.

An example from Keith’s article:

```css
.Card {
  /* ... */
}
.Card[data-size="big"] {
  width: 100%;
}
.Card[data-size="medium"] {
  width: 50%;
}
.Card[data-size="small"] {
  width: 25%;
}

.Card[data-align="left"] {
  text-align: left;
}
.Card[data-align="right"] {
  text-align: right;
}
.Card[data-align="center"] {
  text-align: center;
}
.Card[data-border-collapse~="top"] {
  border-top: 0;
}
.Card[data-border-collapse~="right"] {
  border-right: 0;
}
.Card[data-border-collapse~="bottom"] {
  border-bottom: 0;
}
.Card[data-border-collapse~="left"] {
  border-left: 0;
}
```

It’s much easier to avoid impossible states when you have different “slots” to fill in with the different groups of variants for your element, rather than shoving all of them in a single cobbled up string in `class`, however disciplined your naming may be.

And there’s a reason why `<article class="card" data-align="left" data-size="small" />` looks attractive — it’s mirroring the APIs we’re used to seeing in design systems and component libraries, but bringing it to vanilla HTML and CSS. Indeed, it’s a small step from data attribute selectors to custom pseudo selectors or prop-based selectors when using Web Components (think `<my-card align="left" size="small" />`).

Still, for now, if you’re not yet using custom elements, there’s a big difference between

```html
<article
  class="card"
  data-loading="true"
  data-variant="primary"
  data-size="large"
  data-border="top right"
  data-elevation="high"
/>
```

and

```html
<button
  aria-label="Toggle menu"
  aria-controls="navbar-menu"
  aria-expanded="true"
  disabled
/>
```

While I wholeheartedly agree with using attributes over classes when they’re already present, adding your own may be a harder pill to swallow. Tapping into native attribute selectors doesn’t conflict with any existing CSS methodology you may be using, but adding custom ones may require a bigger commitment and change in the overall naming conventions in your codebase. It may also make it more difficult to gauge from the HTML alone which attributes are for behaviour versus just styling concerns. And, ultimately, there’s that nagging feeling that you’re going against the grain by repurposing data attributes for styling — after all, selecting elements is what classes are _for_, and what browsers optimise for in selector performance.

Even so, it’s an enticing proposal and I’m excited to see how people continue to shape it. [Devon Govett](https://twitter.com/devongovett/status/1576635415024390144) endorses a split where he uses a class for the component itself, but signals all internal variants and state with `data-*` or `aria-*` attributes. There are some great insights in this thread for those who would like to dig deeper.
