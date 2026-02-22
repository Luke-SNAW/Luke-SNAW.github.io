
> https://adrianroselli.com/2024/02/techniques-to-break-words.html

A few days ago [Benjy Stanton asked about breaking long words in tables](https://mastodon.social/@benjystanton/111985483721389868). I offered a suggestion, which may or may not have worked. I never asked.

My failure to follow up aside, it reminded me that I have had to walk clients through text wrapping and word breaking more than once. I decided I wanted a blog post dated 29 February, so I took a demo I had for word breaking, beat it up a bit, and rushed this post out.

## Demo [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#Demo)

I made a page that allows you to play around with a few variations on breaking words. I use long single words in English, German, Hebrew (right-to-left), Hindi, Japanese, and Arabic (right-to-left). They are probably all terrible examples since I speak none of those. I also have a long web page address and a long email. Then I replicate those each into a table.

The buttons allow you to toggle table layout, which CSS properties you use, and the width of the containers so you can see where else words will break. You can [visit the debug mode](https://cdpn.io/pen/debug/eYoOdrX) and run it full screen if that helps.

## CSS Bits [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#CSS)

The samples are all affected by CSS, but the first of the boxes uses _only_ CSS to achieve the word breaking.

### `table-layout` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#Table)

The tables are set to `100%` wide. With this set, you can toggle [`table-layout: fixed`](https://developer.mozilla.org/en-US/docs/Web/CSS/table-layout#fixed) on and off. When active, the browser tries to fit the table into that defined width, which means all sorts of overflowing and word breaking. This _only_ applies to the tables at the bottom of each block.

When the words break, _how_ they break is affected by what follows.

### `word-break` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#WordBreak)

For this option, I set [`word-break: break-all`](https://developer.mozilla.org/en-US/docs/Web/CSS/word-break#break-all), which breaks words anywhere the browser wants in order to try to fit in the defined width. It ignores any breaking cues you provide. Chinese, Japanese, and Korean (CJK) text is supposed to be exempted from this.

This approach adds no hyphens. It just snaps a word wherever.

### `overflow-wrap` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#OverflowWrap)

I am using [`overflow-wrap: anywhere`](https://developer.mozilla.org/en-US/docs/Web/CSS/overflow-wrap#anywhere) because it is the most aggressive of the `overflow-wrap` values. It will try to honor any breaking cues you provide within the word

This approach also adds no hyphens — unless you provide hints (which I cover below).

### `hyphens` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#Hyphens)

This might be the property you expected. The [`hyphens: auto`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens#auto) will break words and add hyphens based on the language (`lang`) and the browser’s own dictionary.

The browser may not get foreign language hyphenation right.

### `hyphens: manual` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#HyphensManual)

I don’t have a button for this option. The last column has [`hyphens: manual`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens#manual) so you can compare it alongside the other columns. It only works with the soft hyphen character, which is a great opportunity for me to transition…

## HTML Bits [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#HTML)

Columns two, three, and four use HTML to signal where to break words. The same CSS is applied to them as the first column, but you can see different impacts in these three columns.

### `<wbr>` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#WBR)

The word break element, [`<wbr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/wbr), tells a browser that where it sits is a perfectly fine place to break a word. If it wants.

It will not add hyphens. Probably reserve this for web page addresses, emails, code, or other places where transcription accuracy is critical.

Here is the position of all the `<wbr>`s in the English word, the web address, and the email:

```html
super<wbr />cali<wbr />frag<wbr />il<wbr />is<wbr />tic<wbr />ex<wbr />pial<wbr />id<wbr />oc<wbr />ious
https:<wbr />//en<wbr />.wikipedia<wbr />.org<wbr />/wiki<wbr />/The<wbr />_King<wbr />_in<wbr />_Yellow
JR<wbr />-Bob<wbr />.Dobbs<wbr />@CoSG<wbr />.example<wbr />.com
```

### `&shy;` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#SHY)

The soft hyphen isn’t really HTML, but you stuff it into your HTML page in order for it to work. While [`&shy;`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens#suggesting_line_break_opportunities) is meant to work with [`hyphens: manual`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens#manual), it does its job when you don’t set it at all.

Unlike `<wbr>`, you should add `&shy;` only where you know a word should break. You can compare the first and last columns of the demo to see where they mismatch. Probably don’t do it on words in a language you don’t know.

Here is the position of all the `&shy;`s in the English word, the web address, and the email:

```html
super&shy;cali&shy;frag&shy;il&shy;is&shy;tic&shy;ex&shy;pial&shy;id&shy;oc&shy;ious
https:&shy;//en&shy;.wikipedia&shy;.org&shy;/wiki&shy;/The&shy;_King&shy;_in&shy;_Yellow
JR&shy;-Bob&shy;.Dobbs&shy;@CoSG&shy;.example&shy;.com
```

## Other Bits [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#Other)

Rounding out the buttons in the demo.

### `hyphenate-character` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#HyChar)

CSS (and browsers) allow you to override the default character with [`hyphenate-character: <string>`](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphenate-character). I include a field where you can provide you own string, but just for the lulz. Probably never do this unless you are a linguist or one is threatening you.

If you leave the field blank it will revert to `auto`.

### `max-width` [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#MaxWidth)

By default the columns are `6em` wide. You can change that to see other places the words may break. If you leave the field blank the columns revert to `6em`.

## Final Bits [#anchor](https://adrianroselli.com/2024/02/techniques-to-break-words.html#Final)

My suggestions:

- Probably don’t add `&shy;` without guidance from a copywriter.
- Probably don’t add `&shy;` to foreign words without a localization expert or at least a native speaker.
- Probably don’t add `&shy;` to URLs, email addresses, code blocks, and so on.
- Probably restrict `<wbr>` to URLs, email addresses, code blocks, and similar words where technical accuracy is paramount.
- Probably restrict `<wbr>` to _before_ periods and dashes and maybe slashes in URLs and emails so it doesn’t look like the sentence or address has ended.

The demo is simply a demo. It exists solely to let you compare a few styling options and where they intersect with some HTML efforts. My breaks and hyphens are arbitrary. My non-English words are probably laughably wrong (especially where I put the `&shy;` in the Hindi word). I use MDN links throughout, but I encourage you to go directly to the specs once you grok the more human-oriented MDN content.
