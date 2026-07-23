
https://www.joshwcomeau.com/css/understanding-layout-algorithms/

It's not enough to learn what specific properties do. We need to learn how the layout algorithms work, and how they _use_ the properties we provide to them.

...

When I started digging into the layout algorithms, everything started to make more sense. Mysteries that had bothered me for years were solved. I realized that CSS is actually a pretty darn robust language, and I started to really enjoy writing it!

# Layout algorithms

So, what is a “layout algorithm”? You're probably already familiar with some of them. They include:

- Flexbox
- Positioned (eg. position: absolute)
- Grid
- Table
- Flow

(Technically, they're called layout modes, not layout algorithms. But I find “layout algorithm” to be a more helpful label.)

...

If you had asked me about this a few years ago, I would have said something like:

> You can't use z-index without also setting position to something like “relative” or “absolute”, because the z-index property depends on the position property.

**This isn't exactly wrong, but it's a subtle misunderstanding.** It's more accurate to say that the `z-index` property is _not implemented_ in the Flow layout algorithm, and so we'd need to pick a different layout algorithm if we want this property to have an effect.

...

**This is the critical mental-model shift.** CSS properties on their own are meaningless. It's up to the layout algorithm to _define_ what they do, how they're used in the calculations.

To be clear, there are some CSS properties that work the same in all layout algorithms. `color: red` will produce red text no matter what. But each layout algorithm can override the default behavior for any property. And many properties don't have any default behavior.

...

# Identifying the layout algorithm

# Inline magic space

# Building an intuition

**So, here's the point:** If you were focusing exclusively on studying what specific CSS properties do, you'd never understand where this mysterious space is coming from. It isn't explained in the MDN pages for `display` or `line-height`.

As we've learned in this post, “inline magic space” isn't really magic at all. It's caused by a rule within the Flow layout algorithm that inline elements should be affected by `line-height`. But it seemed magical to me, for many years, because I had this big hole in my mental model.

There are a lot of layout algorithms in CSS, and they all have their own quirks and hidden mechanisms. When we focus on CSS properties, we're only seeing the tip of the iceberg. We never learn about really important concepts like stacking contexts or containing blocks or cascade origins!
