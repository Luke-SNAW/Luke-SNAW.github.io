---
id: 9tsxxuetkq02weun4dll71z
title: "So <HGROUP> Is Back In HTML 5, And Dumb As Ever!"
desc: ""
updated: 1686613002270
created: 1686612570579
published: false
---

> https://medium.com/codex/so-hgroup-is-back-in-html-5-and-dumb-as-ever-c81e00f6320d

Well over a decade ago when the WhatWG was first working on HTML 5 they introduced the `<hgroup>` tag to group together numbered headings for things like title and tagline. This immediately raised the ire of people who understood HTML semantics since putting H1+H2 together that way is ignorant broken nonsense. Many — _myself included_ — took it as **proof** — _alongside acceptance of_ `<embed>` _into the spec, their new_ `<aside>` _tag that had nothing to do with grammatical/literary asides and instead indicated presentation, the pointless `<video>` \_and_ `<audio>` _that were redundant to_ `<object>` — that the people creating HTML 5 didn’t know enough about HTML 4 to be making its successor.

Because this:

```html
<hgroup>
  <h1>Site Title</h1>
  <h2>TagLine</h2>
</hgroup>
```

Is ignorant incompetent dumbass rubbish [if you understand that a H1 is **the** _(singular)_ head**ING** _(singular)_ that all H2 on the page mark the start of subsections of. The first H2 on a page marking the start of the main content if you don’t use <main>. H3 mark the start of a subsection of the H2 preceding it and so forth.](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements) They do not mean fonts in different weights and sizes, they establish a navigable document structure with landings. _A concept very important for users of screen readers and braille readers, as well as for search engines._

For this reason it was made “obsolete” almost as fast as HTML 5 was adopted by the W3C when they shelved their own plans. _Yes, they did have their own plan before the WhatWG beat them to it._ And that’s the thing, “obsolete” as in “do not use, browser support might disappear entirely” and not “‘deprecated” as in “do not use”. _Gah, deprecated, another example of the W3C using the wrong word. We’re not talking down to those tags like they were petulant children._

## So How And Why Is It Back?

Well, it looks like they tried — and failed — to fix it. It no longer only accepts numbered headings as its children, and in fact now only accepts ONE such heading. For further heading lines, you’re to use Paragraphs… **and ONLY paragraphs.**

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hgroup

Check out the “permitted content”

> Permitted content: Zero or more [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) elements, followed by one [`<h1>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), [`<h2>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), [`<h3>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), [`<h4>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), [`<h5>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), or [`<h6>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements) element, followed by zero or more [`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p) elements.

Content before the actual heading is utter gibberish, a failure to even understand what numbered headings are or are even for. Worse though, most of the examples you find… well, let’s use MDN’s.

```html
<hgroup id="document-title">
  <h1>HTML: Living Standard</h1>
  <p>Last Updated 12 July 2022</p>
</hgroup>
```

What makes a two word label and a date a complete sentence, much less “one or more complete sentences encompassing a single thought”… aka what a <p>aragraph tag is **FOR?** Aka what a paragraph **IS?** I mean if I tried to apply that to my own site:

```html
<hgroup>
  <h1>CutCodeDown</h1>
  <p>Minimalist Semantic Markup</p>
</hgroup>
```

That’s garbage nonsense because that’s NOT a complete paragraph. It’s not even a sentence fragment! /FAIL/ at understanding HTML semantics.

Now admittedly, the alternative practice commonly used has its problems:

```html
<h1>
  Cutcodedown<br />
  <small>Minimalist Semantic Markup</small>
</h1>
```

But makes way more sense because it’s ALL that depth heading,. **ALL OF IT!** Some folks might object to the use of <small> for de-emphasis, but as we have no “deem” tag and small means “would be smaller for structural or grammatical reasons” and **not** “show this text smaller”, it’s fine and we don’t need HGROUP. If it “really’ bothers you, use a <span>. Of the two, I guarantee you screen readers and braille readers will be a lot clearer if you don’t crap paragraphs around non-paragraph content, and actually bother making your heading — **ALL of your heading** — a single freaking heading tag!

But what if you actually have paragraphs… or maybe a list? Or maybe some other tag that <hgroup> doesn’t allow inside it. If only they had already created a tag for headers that contain multiple block level tags.

Oh wait, they already did!

```html
<header>
  <h1>Some Title</h1>
  <p>
    Let's say you actually had a paragraph worth of stuff in your header group.
    Well, here you go!
  </p>
</header>
```

**Thus the new <hgroup> is redundant to <header>!**

I’m not sure why they felt the need to resurrect this monument to stupidity, in a manner as broken, silly, and ignorant as it originally was… but this is the WhatWG we’re talking about. Time and time again they have proven themselves unfit, uninformed, and unaware enough of semantic markup to have created HTML 4 Strict’s successor.

## It Also Illustrates Another Major Problem

Until very recently the validation service would tell you that hgroup is obsolete. Now it tells you that you have the wrong content on older pages. But there is no way to tell what standard — original, obsolete, new — those pages were actually written for!

The entire notion of this “living document” malarkey with zero way to track in the document what version of the specification it was written for is shortsighted, poorly thought out, and just plain **DUMBASS!** It’s what I keep talking about when I say that thanks to this special flavor of “WhatWG Stupid” a year ago’s valid HTML 5 can be invalid today, and today’s valid HTML 5 can be invalid tomorrow.

No matter how you want to spin that, it’s part of what makes even calling HTML 5 a “specification” a cruel joke. For this reason alone I think it’s time for us to abandon confidence in the W3C and WhatWG moving forward. There’s a reason other “standards bodies” point their finger at the W3C and laugh, making them sit at the kids table whenever there’s a gathering.

It may be time for someone else to seize the reigns for a while. Maybe someone competent, capable, and a track record of making genuine improvements to existing technologies like the ECMA?
