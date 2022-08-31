---
id: 8w5mxswu48wwne2lisingsc
title: 'Using :has() as a CSS Parent Selector and much more'
desc: ''
updated: 1661748214738
created: 1661745381272
---

> https://webkit.org/blog/13096/css-has-pseudo-class/

Over the last [twenty years](https://lists.w3.org/Archives/Public/www-style/2002May/0037.html), the CSS Working Group discussed the possibility many, many times. The need was clear and well understood. Defining syntax was a doable task. But figuring out how a browser engine could handle potentially very complex circular patterns, and get through the calculations fast enough seemed impossible. Early versions of a parent selector were drafted for CSS3, only to be deferred. Finally, the `:has()` pseudo-class was officially defined in [CSS Selectors level 4](https://www.w3.org/TR/selectors-4/#relational). But having a web standard alone didn’t make `:has()` a reality. We still needed a browser team to figure out the very real performance challenge. In the meantime, computers continued to get more powerful and faster year after year.

In 2021, [Igalia](https://www.igalia.com/) started advocating for `:has()` among browser engineering teams, [prototyping](https://bkardell.com/blog/canihas.html) their ideas and [documenting](https://github.com/Igalia/explainers/tree/main/css/has) their findings regarding performance. The renewed attention on `:has()` caught the attention of engineers who work on WebKit at Apple. We started implementing the pseudo-class, thinking through possibilities for the needed performance enhancements to make this work. We debated whether to start with a faster version with a very limited and narrow scope of what it could do, and then try to remove those limits if possible… or to start with something that had no limits, and only apply restrictions as required. We went for it, and implemented the more powerful version. We developed a number of novel `:has`\-specific caching and filtering optimizations, and leveraged the existing advanced optimization strategies of our CSS engine. And our approach worked, proving that after a two decade wait, it is finally possible to implement such a selector with [fantastic performance](https://twitter.com/anttikoivisto/status/1473251189181591554), even in the presence of large DOM trees and large numbers of `:has()` selectors.

## The basics of how to use :has() as a parent selector

```css
figure:has(pre) {
  background: rgb(252, 232, 255);
  border: 3px solid white;
  padding: 1rem;
}
```

And I use a Selector Feature Query to hide a reminder about browser support whenever the current browser supports `:has()`.

```css
@supports selector(:has(img)) {
  small {
    display: none;
  }
}
```

The `@supports selector()` at-rule is itself [very well supported](https://caniuse.com/mdn-css_at-rules_supports_selector). It can be incredibly useful anytime you want to use a [feature query](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Conditional_Rules/Using_Feature_Queries) to test for browser support of a particular selector.

And finally, in this first demo, I also write a complex selector using the [`:not() pseudo-class`](https://developer.mozilla.org/en-US/docs/Web/CSS/:not). I want to apply `display: flex` to the figure — but only if an image is the sole content. Flexbox makes the image stretch to fill all available space.

I use a selector to target any `figure` that does _not_ have any element that is _not_ an image. If the `figure` has a `figcaption`, `pre`, `p`, or an `h1` — or any element at all besides `img` — then the selector doesn’t apply.

```css
figure:not(:has(:not(img))) {
  display: flex;
}
```

`:has()` is a powerful thing.

## Using :has() with the child combinator

First, a quick review of the difference between the [descendant combinator](https://www.w3.org/TR/selectors-4/#descendant-combinators) and the [child combinator](https://www.w3.org/TR/selectors-4/#child-combinators) (`>`).

```css
a:has(img) {
  ...;
}
```

```css
a:has(> img) {
  ...;
}
```

The first selects any `a` element with an `img` inside — any place in the HTML structure. While the second selects an element only if the `img` is a direct child of the `a`.

## Using :has() with sibling combinators

Let’s review the two selectors with sibling relationships. There’s the [next-sibling combinator](https://www.w3.org/TR/selectors-4/#adjacent-sibling-combinators) (`+`) and the [subsequent-sibling combinator](https://www.w3.org/TR/selectors-4/#general-sibling-combinators) (`~`).

The next-sibling combinator (`+`) selects only the paragraphs that come _directly_ after an `h2` element.

```css
h2 + p
```

```html
<h2>Headline</h2>
<p>Paragraph that is selected by `h2 + p`, because it's directly after `h2`.</p>
```

The subsequent-sibling combinator (`~`) selects all paragraphs that come after an `h2` element. They must be siblings, but there can be any number of other HTML elements in between.

```css
h2 ~ p
```

```html
<h2>Headline</h2>
<h3>Something else</h3>
<p>Paragraph that is selected by `h2 ~ p`.</p>
<p>This paragraph is also selected.</p>
```

Note that both `h2 + p` and `h2 ~ p` select the paragraph elements, and not the `h2` headlines. Like other selectors (think of `a img`), it’s the last element listed that is targeted by the selector. But what if we want to target the `h2`? We can use sibling combinators with `:has().`

How often have you wanted to adjust the margins on a headline based on the element following it? Now it’s easy. This code allows us to select any `h2` with a `p` immediately after it.

```css
h2:has(+ p) {
  margin-bottom: 0;
}
```

Amazing.

What if we want to do this for all six headline elements, without writing out six copies of the selector. We can use [`:is`](https://developer.mozilla.org/en-US/docs/Web/CSS/:is) to simplify our code.

```css
:is(h1, h2, h3, h4, h5, h6):has(+ p) {
  margin-bottom: 0;
}
```

Or what if we want to write this code for more elements than just paragrapahs? Let’s eliminate the bottom margin of all headlines whenever they are followed by paragraphs, captions, code examples and lists.

```css
:is(h1, h2, h3, h4, h5, h6):has(+ :is(p, figcaption, pre, dl, ul, ol)) {
  margin-bottom: 0;
}
```

Combining `:has()` with [descendant combinators](https://www.w3.org/TR/selectors-4/#descendant-combinators), [child combinators](https://www.w3.org/TR/selectors-4/#child-combinators) (`>`), [next-sibling combinators](https://www.w3.org/TR/selectors-4/#adjacent-sibling-combinators) (`+`), and [subsequent-sibling combinators](https://www.w3.org/TR/selectors-4/#general-sibling-combinators) (`~`) opens up a world of possibilities. But oh, this is _still_ just the beginning.

## Styling form states without JS

There are a lot of fantastic [pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) that can be used inside has:(). In fact, it revolutionizes what pseudo-classes can do. Previously, pseudo-classes were only used for styling an element based on a special state — or styling one of its children. Now, pseudo-classes can be used to capture state, without JavaScript, and style anything in the DOM based on that state.

Form input fields provide a powerful way to capture such a state. Form-specific pseudo-classes include `:autofill`, `:enabled`, `:disabled`, `:read-only`, `:read-write`, `:placeholder-shown`, `:default`, `:checked`, `:indeterminate`, `:valid`, `:invalid`, `:in-range`, `:out-of-range`, `:required` and `:optional`.

Let’s solve one of the use cases I described in the introduction — the long-standing need to style a form label based on the state of the input field. Let’s start with a basic form.

```html
<form>
  <div>
    <label for="name">Name</label>
    <input type="text" id="name" />
  </div>
  <div>
    <label for="site">Website</label>
    <input type="url" id="site" />
  </div>
  <div>
    <label for="email">Email</label>
    <input type="email" id="email" />
  </div>
</form>
```

I’d like to apply a background to the whole form whenever one of the fields is in focus.

```css
form:has(:focus-visible) {
  background: antiquewhite;
}
```

Now I could have used `form:focus-within` instead, but it would behave like `form:has(:focus)`. The [`:focus`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus) pseudo-class always applies CSS whenever a field is in focus. The [`:focus-visible`](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible) pseudo-class provides a reliable way to style a focus indicator only when the browser would draw one natively, using the same [complex heuristics the browser uses](https://webkit.org/blog/12179/the-focus-indicated-pseudo-class-focus-visible/) to determine whether or not to apply a focus-ring.

Now, let’s imagine I want to style the other fields, the ones _not_ in focus — changing their label text color and the input border color. Before `:has()`, this required JavaScript. Now we can use this CSS.

```css
form:has(:focus-visible) div:has(input:not(:focus-visible)) label {
  color: peru;
}
form:has(:focus-visible) div:has(input:not(:focus-visible)) input {
  border: 2px solid peru;
}
```

What does that selector say? If one of the controls inside this form has focus, and the input element for this particular form control does not have focus, then change the color of this label’s text to `peru`. And change the border of the input field to be `2px solid peru`.

```css
input:invalid {
  outline: 4px solid red;
  border: 2px solid red;
}
```

Now with `:has()`, we can turn the label text red as well:

```css
div:has(input:invalid) label {
  color: red;
}
```

You can see the result by typing something in the website or email field that’s not a fully-formed URL or email address. Both are invalid, and so both will trigger a red border and red label, with an “X”.

## And more

Looking through other [pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes), there are so many that can be combined with `:has()`. Imagine the possibilities with `:nth-child`, `:nth-last-child`, `:first-child`, `:last-child`, `:only-child`, `:nth-of-type`, `:nth-last-of-type`, `:first-of-type`, `:last-of-type`, `:only-of-type`. The brand new [`:modal`](https://developer.mozilla.org/en-US/docs/Web/CSS/:modal) pseudo-class is triggered when a `dialog` is in the open state. With `:has(:modal)` you can style anything in the DOM based on whether the `dialog` is open or closed.

However, not every pseudo-class is currently supported inside `:has()` in every browser, so do try out your code in multiple browsers. Currently the dynamic media pseudo-classes don’t work — like `:playing`, `:paused`, `:muted`, etc. They very well may work in the future, so if you are reading this in the future, test them out! Also, form invalidation support is currently missing in certain specific situations, so dynamic state changes to those pseudo-classes may not update with `:has()`.

Safari 16 will add support for `:has(:target)` opening up interesting possibilities for writing code that looks at the current URL for a fragment that matches the ID of a specific element. For example, if a user clicks on a table of contents at the top of a document, and jumps down to the section of the page matching that link, [`:target`](https://developer.mozilla.org/en-US/docs/Web/CSS/:target) provides a way to style that content uniquely, based on the fact the user clicked the link to get there. And `:has()` opens up what such styling can do.

Something to note — the CSS Working Group [resolved](https://github.com/w3c/csswg-drafts/issues/7463) to disallow all existing pseudo-elements inside of `:has()`. For example, `article:has(p::first-line)` and `ol:has(li::marker)` won’t work. Same with `::before` and `::after.`
