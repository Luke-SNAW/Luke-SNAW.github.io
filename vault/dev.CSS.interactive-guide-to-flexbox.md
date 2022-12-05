---
id: mgyobc2e4in12fahp3y3el7
title: An Interactive Guide to Flexbox
desc: ""
updated: 1670223354453
created: 1670221005197
---

> https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/

This demo is heavily inspired by Adam Argyle’s incredible [“4 layouts for the price of 1”](https://codepen.io/argyleink/pen/LYEegOO) codepen. _It uses no media/container queries._ Instead of setting arbitrary breakpoints, it uses _fluid principles_ to create a layout that flows seamlessly.

Here's the relevant CSS:

```css
form {
  display: flex;
  align-items: flex-end;
  flex-wrap: wrap;
  gap: 16px;
}
.name {
  flex-grow: 1;
  flex-basis: 160px;
}
.email {
  flex-grow: 3;
  flex-basis: 200px;
}
button {
  flex-grow: 1;
  flex-basis: 80px;
}
form {
  display: flex;
  align-items: flex-end;
  flex-wrap: wrap;
  gap: 16px;
}
.name {
  flex-grow: 1;
  flex-basis: 160px;
}
.email {
  flex-grow: 3;
  flex-basis: 200px;
}
button {
  flex-grow: 1;
  flex-basis: 80px;
}
```

## [Introduction to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#introduction-to-flexbox)

...

**Each layout algorithm is designed to solve a specific problem.** The default “Flow” layout is meant to create digital documents; it's essentially the _Microsoft Word_ layout algorithm. Headings and paragraphs stack vertically as blocks, while things like text, links, and images sit inconspicuously within these blocks.

**So, what problem does Flexbox solve?** Flexbox is all about arranging a group of items in a row or column, and giving us a _ridiculous_ amount of control over the distribution and alignment of those items. As the name suggests, Flexbox is all about _flexibility_. We can control whether items grow or shrink, how the extra space is distributed, and more.

> **Is it still relevant?**
>
> You might be wondering: now that CSS Grid is well-supported in modern browsers, isn't Flexbox obsolete?
>
> CSS Grid is a wonderful layout mode, **but it solves different problems than Flexbox.** We should learn _both_ layout modes, and use the right tool for the job.
>
> Flexbox still reigns supreme when it comes to dynamic, fluid UIs that arrange items in a vertical or horizontal list. We'll see an example in this guide, the _deconstructed pancake_, that can't easily be accomplished with CSS Grid.
>
> Honestly, as someone comfortable with both CSS Grid and Flexbox, I still find myself reaching for Flexbox quite often!

## [Alignment](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#alignment)

...

### [Content vs. items](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#content-vs-items)

So, based on what we've learned so far, Flexbox might seem pretty arbitrary. Why is it `justify-content` and `align-items`, and not `justify-_items_`, or `align-_content_`?

For that matter, why is there an `align-self`, but not a `_justify_-self`??

**These questions get at one of the most important and misunderstood things about Flexbox.** To help me explain, I'd like to use a metaphor.

In Flexbox, items are distributed along the primary axis. By default, they're nicely lined up, side-by-side. I can draw a straight horizontal line that skewers _all_ of the children, like a kebab?:

The cross axis is different, though. A straight vertical line will only ever intersect _one_ of the children.

It's less like a kebab, and more like a group of cocktail wieners?:

There's a significant difference here. With the cocktail wieners, each item can move along its stick _without interfering_ with any of the other items:

By contrast, with our primary axis skewering each sibling, a single item _can’t_ move along its stick without bumping into its siblings! **Try dragging the middle piece side to side:**

**This is the fundamental difference between the primary/cross axis.** When we're talking about alignment in the _cross_ axis, each item can do whatever it wants. In the _primary_ axis, though, we can only think about how to distribute the _group_.

**That's why there's no** `justify-self`**.** What would it mean for that middle piece to set `justify-self: flex-start`? There's already another piece there!

With all of this context in mind, let's give a proper definition to all 4 terms we've been talking about:

- `justify` — to position something along the _primary axis_.
- `align` — to position something along the _cross axis_.
- `content` — a group of “stuff” that can be distributed.
- `items` — single items that can be positioned individually.

**And so:** we have `justify-content` to control the distribution of the group along the primary axis, and we have `align-items` to position each item individually along the cross axis. These are the two main properties we use to manage layout with Flexbox.

There's no `justify-items` for the same reason that there's no `justify-self`; when it comes to the primary axis, _we have to think of the items as a group,_ as content that can be distributed.

What about `align-content`? Actually, this _does_ exist within Flexbox! We'll cover it a little later on, when we talk about the `flex-wrap` property.

## [Hypothetical size](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#hypothetical-size)

Let's talk about one of the most eye-opening realizations I've had about Flexbox.

Suppose I have the following CSS:

```css
.item {
  width: 2000px;
}
```

A reasonable person might look at this and say: “alright, so we'll get an item that is 2000 pixels wide”. _But will that always be true?_

Let's test it:

### Code Playground

```html
<style>
  .flex-wrapper {
    display: flex;
  }
  .item {
    width: 2000px;
  }
</style>

<div class="item"></div>
<div class="flex-wrapper"><div class="item"></div></div>
```

This is interesting, isn't it?

**Both items have the exact same CSS applied.** They each have `width: 2000px`. And yet, the first item is much wider than the second!

The difference is the _layout mode_. The first item is being rendered using Flow layout, and in Flow layout, `width` is a _hard constraint_. When we set `width: 2000px`, we'll get a 2000-pixel wide element, even if it has to burst through the side of the viewport like the Kool-Aid guy.

In _Flexbox_, however, the `width` property is implemented differently. It's more of a suggestion than a hard constraint.

The specification has a name for this: the _hypothetical size_. It's the size an element _would_ be, in a perfect utopian world, with nothing getting in the way.

Alas, things are rarely so simple. In this case, the limiting factor is that the parent _doesn't have room_ for a 2000px-wide child. And so, the child's size is reduced so that it fits.

This is a core part of the Flexbox philosophy. Things are fluid and flexible and can adjust to the constraints of the world.

> **Inputs for the algorithms**
>
> We tend to think of the CSS language as a collection of properties, but **I think that's the wrong mental model.** As we've seen, the `width` property behaves differently depending on the layout mode used!
>
> Instead, I like to think of CSS as a collection of layout modes. Each layout mode is an algorithm that can _implement or redefine_ each CSS property. We provide an algorithm with our CSS declarations (key/value pairs), and the algorithm decides how to use them.
>
> In other words, **the CSS we write is an input for these algorithms**, like arguments passed to a function. If we want to _truly_ feel comfortable with CSS, it's not enough to learn the properties; we have to learn how the algorithms _use_ these properties.
>
> This is the central philosophy taken by my course, [**CSS for JavaScript Developers**](https://css-for-js.dev/). Rather than have you memorize a bunch of inscrutable CSS snippets, we pop the hood on the language and learn how all of the layout modes work.

## [Growing and shrinking](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#growing-and-shrinking)

So, we've seen that the Flexbox algorithm has some built-in flexibility, with _hypothetical sizes_. But to _really_ see how fluid Flexbox can be, we need to talk about 3 properties: `flex-grow`, `flex-shrink`, and `flex-basis`.

Let's look at each property.

### [flex-basis](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#flex-basis)

I admit it: for a long time, I didn't really understand what the _deal_ was with `flex-basis`. 😅

**To put it simply:** In a Flex row, `flex-basis` does the same thing as `width`. In a Flex column, `flex-basis` does the same thing as `height`.

As we've learned, everything in Flexbox is _pegged to the primary/cross axis_. For example, `justify-content` will distribute the children along the primary axis, and it works exactly the same way whether the primary axis runs horizontally or vertically.

`width` and `height` don't follow this rule, though! `width` will always affect the horizontal size. It doesn't suddenly become `height` when we flip `flex-direction` from `row` to `column`.

**And so, the Flexbox authors created a generic “size” property called `flex-basis`.** It's like `width` or `height`, but pegged to the _primary axis_, like everything else. It allows us to set the _hypothetical size_ of an element in the primary-axis direction, regardless of whether that's horizontal or vertical.

Like we saw with `width`, `flex-basis` is more of a suggestion than a hard constraint. At a certain point, there just isn't enough space for all of the elements to sit at their assigned size, and so they have to compromise, in order to avoid an overflow.

> **Not _exactly_ the same**
>
> In general, we can use `width` and `flex-basis` interchangeably in a Flex row, but there are some exceptions. For example, the `width` property affects replaced elements like images differently than `flex-basis`. Also, `width` can reduce an item below its _minimum_ size, while `flex-basis` can't.
>
> It's well outside the scope of this blog post, but I wanted to mention it, because you may occasionally run into edge-cases where the two properties have different effects.

### flex-grow

By default, elements in a Flex context will shrink down to their minimum comfortable size along the primary axis. This often creates extra space.

We can specify how that space should be consumed with the flex-grow property.

The default value for `flex-grow` is 0, which means that growing is opt-in. If we want a child to gobble up any extra space in the container, we need to explicitly tell it so.

**What if _multiple_ children set `flex-grow`?** In this case, the extra space is divvied up between children, proportionally based on their `flex-grow` value.

I think it'll be easier to explain visually. Try incrementing/decrementing each child. https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#flex-grow

### flex-shrink

In most of the examples we've seen so far, we've had extra space to work with. But what if our children are _too big_ for their container?

**Let's test it.** Try shrinking the container to see what happens:
https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#flex-shrink

Interesting, right? Both items shrink, **but they shrink proportionally.** The first child is always 2x the width of the second child.\*

As a friendly reminder, `flex-basis` serves the same purpose as `width`. We'll use `flex-basis` because it's conventional, but we'd get the **exact same result** if we used `width`!

`flex-basis` and `width` set the elements' _hypothetical size_. The Flexbox algorithm might shrink elements below this desired size, but by default, they'll always scale together, preserving the ratio between both elements.

Now, what if we _don't_ want our elements to scale down proportionally? **That's where the `flex-shrink` property comes in.**

Take a couple of minutes and poke at this demo. **See if you can figure out what's going on here.** We'll explore below.
https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#flex-shrink

**The `flex-shrink` property lets us decide how that balance is paid.**

Like `flex-grow`, it's a ratio. By default, both children have `flex-shrink: 1`, and so each child pays ½ of the balance. They each forfeit 50px, their actual size shrinking from 250px to 200px.

Note that the absolute values don't matter, **it's all about the ratio.** If both children have `flex-shrink: 1`, each child will pay ½ of the total deficit. If both children are cranked up to `flex-shrink: 1000`, each child will pay 1000/2000 of the total deficit. Either way, it works out to the same thing.

### Preventing shrinking

Sometimes, we don't _want_ some of our Flex children to shrink.

I notice this all the time with SVG icons and shapes. Let's look at a simplified example: https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#preventing-shrinking

When the container gets narrow, our two circles get squashed into gross ovals. **What if we want them to stay circular?**

We can do this by setting `flex-shrink: 0`:
https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#preventing-shrinking

> **A simpler approach?**
>
> So, I teach this concept in [my course](https://css-for-js.dev/), and every now and then, someone will wonder why we're going through all the trouble of using `flex-shrink` when there's a simpler approach available:

```css
.item.ball {
  min-width: 32px;
}
```

> A few years ago, I would have agreed. If we set a minimum width, the item won't be able to shrink below that point! We're adding a hard constraint, instead of the soft constraint of `width` / `flex-basis`.
>
> I think this is one of those situations where it's easy to confuse “familiar” with “simple”. You're probably much more comfortable with `min-width` than `flex-shrink`, but that doesn't mean `flex-shrink` is more complicated!
>
> After a few years of practice, I actually feel like setting `flex-shrink: 0` is the more straightforward / direct solution to this particular problem. Though, `min-width` still has an important role to play in the Flexbox algorithm! We'll talk about that next.

## The minimum size gotcha

There's _one more thing_ we need to talk about here, and it's super important. It may be the single most helpful thing in this entire article!

Let's suppose we're building a fluid search form for an e-commerce store: https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#the-minimum-size-gotcha

When the container shrinks below a certain point, **the content overflows!**

_But why??_ `flex-shrink` has a default value of `1`, and we haven't removed it, so the search input _should_ be able to shrink as much as it needs to! Why is it refusing to shrink?

**Here's the deal:** In addition to the _hypothetical_ size, there's another important size that the Flexbox algorithm cares about: _the minimum size_.

The Flexbox algorithm refuses to shrink a child below its minimum size. The content will overflow rather than shrink further, _no matter how high we crank `flex-shrink`!_

Text inputs have a default minimum size of 170px-200px (it varies between browsers). That's the limitation we're running into above.

**Here's the good news:** We can redefine the minimum size with the `min-width` property.

> **Proceed with caution**
>
> It's worth noting that the built-in minimum size _does_ serve a purpose. It's meant to act as a guardrail, to prevent something even worse from happening.
>
> For example: when we apply `min-width: 0px` to our text-containing Flex children, things break in an even worse way: https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#the-minimum-size-gotcha

> With great power comes great responsibility, and `min-width` is a particularly powerful property when it comes to Flexbox. It's gotten me out of a jam more than once, but I'm always careful to make sure I'm not making things worse!

### Auto margins

There's one other spacing-related trick I want to share. It's been around since the early days of Flexbox, but it's relatively obscure, and it _blew my mind_ when I first discovered it.

The `margin` property is used to add space around a specific element. In some layout modes, like Flow and Positioned, it can even be used to center an element, with `margin: auto`.

Auto margins are much more interesting in Flexbox: https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#auto-margins

Auto margins will **gobble up the extra space, and apply it to the element's margin.** It gives us precise control over where to distribute the extra space.

## Wrapping

So far, all of our items have sat side-by-side, in a single row/column. The `flex-wrap` property allows us to change that.

Each row is its own mini Flexbox environment. `align-items` will move each item up or down within the invisible box that wraps around each row.

But what if we want to _align the rows themselves_? We can do that with the `align-content` property: https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/#wrapping

To summarize what's happening here:

- `flex-wrap: wrap` gives us two rows of stuff.
- Within each row, `align-items` lets us slide each individual child up or down
- Zooming out, however, we have these two rows within a single Flex context! The cross axis will now intersect _two_ rows, not one. And so, we can't move the rows individually, we need to distribute them _as a group_.
- Using our definitions from above, we're dealing with _content_, not _items_. But we're also still talking about the cross axis! And so the property we want is `align-content`.
