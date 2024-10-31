
> https://chriscoyier.net/2023/06/06/modern-css-in-real-life/

## [Logical Properties & Layout](https://chriscoyier.net/2023/06/06/modern-css-in-real-life/#logical-properties-layout)

Logical Properties make for a slightly easier-to-understand model because the words are more consistently used.

- `margin-right`: Translated to RTL, spacing problem. use `margin-inline-end` (or `gap`).
- `img` alt: With that brief information, perhaps someone might be able to, say, recognize the exact pier in the photo if they had been there before or the like.

## [Cascade Layers](https://chriscoyier.net/2023/06/06/modern-css-in-real-life/#logical-properties-layout)

- higher layer will win, regardless of specificity.

Consider [Bootstrap](https://getbootstrap.com/). Tons of people have used it and mostly successfully.

But haven’t you heard horror stories too? Or lived one? Sometimes the _way_ it gets implemented is really strange or problematic. Like loading the entire library when only a little bit is used. Like trying to customize it but struggling with that and not being sure how to upgrade after monkey patching. Like loading multiple copies of it because omg who even knows what is happening anymore. But the most common problem I’ve heard about? (I’d like to think I’m qualified to know about people’s problems as I’ve had [a write-in-question web development podcast](https://shoptalkshow.com/) for a decade): **overrides**.

```css
@import url("https://cdn.com/bootstrap.css");

h5 {
  /* nope */
  margin-bottom: 2rem;
}
```

The problem is that people use Bootstrap, then need to override some aspect of it, and instead of doing that in some chill, normal, maintainable way, they use super powerful CSS selectors to override things (then do it again, and again). Or they use `!important` rules. This is born out of not knowing exactly how best safely and maintainable override the CSS that Bootstrap provides. (And I hope this is clear: this applies to any CSS library or even a project’s own CSS).

So what can you do? How does cascade layers apply to this?

We can use cascade layers to essentially _demote_ the entirety of Bootstrap.

Here, my `@import` of Bootstrap is plunked onto a layer. Note: we don’t even have to name it, and we can use this keyword instead of `@layer` while importing.

```css
@import url("https://cdn.com/bootstrap.css") layer;

h5 {
  /* winner winner chicken dinner */
  margin-bottom: 2rem;
}
```

Now my super weak CSS selector in which I’m trying to override header margin _does_ win. It wins because “un”-layered styles are the most powerful, like the “highest” layer. Wild. My guess is that if you did this on a new project, over time, you’ve have less annoying CSS selector conflicts, escalating specfiicty, and `!important` wars.

```css
@layer reset, default, themes, patterns, layouts, components, utilities;
```
