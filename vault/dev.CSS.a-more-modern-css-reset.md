---
id: 4iqsbvk42j5rig74203rhmy
title: A (more) Modern CSS Reset
desc: ""
updated: 1695262069673
created: 1695262019505
---

> https://andy-bell.co.uk/a-more-modern-css-reset/

I wrote [A Modern CSS Reset](https://andy-bell.co.uk/a-modern-css-reset/) almost 4 years ago and, yeh, it’s not aged overly well. I spotted it being linked up again a few days ago and thought it’s probably a good idea to publish an updated version.

I know I also have a terrible record with open source maintenance, so I thought I’d [archive the original](https://github.com/Andy-set-studio/modern-css-reset) and just post this instead. Do with it what you want!

To be super clear, this is a reset that works for me, personally and us at [Set Studio](https://set.studio/). Whenever I refer to “we”, that’s who I’m referring to.

## The reset in whole

```css
/* Box sizing rules */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Prevent font size inflation */
html {
  -moz-text-size-adjust: none;
  -webkit-text-size-adjust: none;
  text-size-adjust: none;
}

/* Remove default margin in favour of better control in authored CSS */
body,
h1,
h2,
h3,
h4,
p,
figure,
blockquote,
dl,
dd {
  margin: 0;
}

/* Remove list styles on ul, ol elements with a list role, which suggests default styling will be removed */
ul[role="list"],
ol[role="list"] {
  list-style: none;
}

/* Set core body defaults */
body {
  min-height: 100vh;
  line-height: 1.5;
}

/* Set shorter line heights on headings and interactive elements */
h1,
h2,
h3,
h4,
button,
input,
label {
  line-height: 1.1;
}

/* Balance text wrapping on headings */
h1,
h2,
h3,
h4 {
  text-wrap: balance;
}

/* A elements that don't have a class get default styles */
a:not([class]) {
  text-decoration-skip-ink: auto;
  color: currentColor;
}

/* Make images easier to work with */
img,
picture {
  max-width: 100%;
  display: block;
}

/* Inherit fonts for inputs and buttons */
input,
button,
textarea,
select {
  font: inherit;
}

/* Make sure textareas without a rows attribute are not tiny */
textarea:not([rows]) {
  min-height: 10em;
}

/* Anything that has been anchored to should have extra scroll margin */
:target {
  scroll-margin-block: 5ex;
}
```

## Breakdown

As is tradition, let’s break it down:

```css
/* Box sizing rules */
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

This rule is pretty self explanatory, but in short, I’m setting all elements and pseudo-elements to use the `border-box`, [rather than the default `content-box` for sizing](https://web.dev/learn/css/box-model/). Now we’re focussing more on letting the [browser do more work](https://buildexcellentwebsit.es/) with [flexible layouts](https://every-layout.dev/) with [fluid type and space](https://utopia.fyi/), this rule isn’t as useful as it once was. But, it’s rare that a project doesn’t have some explicit sizing somewhere, so it’s still got a place in the reset.

```css
/* Prevent font size inflation */
html {
  -moz-text-size-adjust: none;
  -webkit-text-size-adjust: none;
  text-size-adjust: none;
}
```

The [best explainer for this is by Kilian](https://kilianvalkhof.com/2022/css-html/your-css-reset-needs-text-size-adjust-probably/). He also explains why we still need those ugly prefixes too.

```css
/* Remove default margin in favour of better control in authored CSS */
body,
h1,
h2,
h3,
h4,
p,
figure,
blockquote,
dl,
dd {
  margin: 0;
}
```

I’ll always favour stripping out user agent styles for margin in favour of [defining flow and space at a more macro level](https://andy-bell.co.uk/my-favourite-3-lines-of-css/). With logical properties, I’m removing the end margin now instead of all sides in the older reset. It seems to work well in production.

```css
/* Remove list styles on ul, ol elements with a list role, which suggests default styling will be removed */
ul[role="list"],
ol[role="list"] {
  list-style: none;
}
```

Safari do some wild shit, which includes [this one](https://bugs.webkit.org/show_bug.cgi?id=170179): if you remove list styling, they’ll remove the semantics for VoiceOver. Some will say it’s a feature and some will say it’s a bug. I say it’s daft, but to make sure that a `role` is added, I remove the list styling by default for it as a little reward.

```css
/* Set core body defaults */
body {
  min-height: 100vh;
  line-height: 1.5;
}
```

I like a nice legible line height that gets inherited. Setting a min height as `100vh` on the body is pretty handy too, especially if you’re gonna be setting decorative elements. It might be tempting to use a new unit like `dvh`, but if you [delve deep like Ahmad has](https://ishadeed.com/article/new-viewport-units/#:~:text=Be%20careful%20with%20the%20dvh,is%20scrolling%20up%20or%20down.), you’ll see that can cause more problems than solutions, which is not what you want your reset to be doing!

[The `svh` unit seems better than `dvh`](https://mastodon.social/@simevidas/111088262361593466), but I’m happy with `vh`. Always make sure you understand the newer units before diving head first into them, or recommending them as gospel is my advice. If something is already working for you, there’s no need to change it!

```css
/* Set shorter line heights on headings and interactive elements */
h1,
h2,
h3,
h4,
button,
input,
label {
  line-height: 1.1;
}
```

Just like it’s handy to have a generous `line-height` globally, it’s equally handy to have a shorter `line-height` for headings and buttons etc. It’s definitely worth removing or modifying this rule if your font has large ascenders and descenders though. The last thing you want is those clashing with each other and creating an accessibility issue.

```css
/* Balance text wrapping on headings */
h1,
h2,
h3,
h4 {
  text-wrap: balance;
}
```

This rule is rather specific to our projects, but the newish `text-wrap` property makes headings look lovely. I imagine some people will find this not appropriate, so you might want to remove this one.

```css
/* A elements that don't have a class get default styles */
a:not([class]) {
  text-decoration-skip-ink: auto;
  color: currentColor;
}
```

This rule is first making sure the text decoration doesn’t interfere with ascenders and descenders. I think this is mostly default in browsers now, but it’s a good insurance policy to set it too. We like to set links to inherit the `currentColor` of text too by default at [the studio](https://set.studio/), but if you don’t, you probably want to remove it.

```css
/* Inherit fonts for inputs and buttons */
input,
button,
textarea,
select {
  font: inherit;
}
```

The `font: inherit` shorthand is bloody useful and we certainly find that with inputs and form elements. It’s mostly going to affect `<textarea>` elements, but there’s no harm in applying it to other form elements too because it saves on some CSS later on in a project.

```css
/* Make sure textareas without a rows attribute are not tiny */
textarea:not([rows]) {
  min-height: 10em;
}
```

Speaking of `<textarea>` elements, this rule is handy. By default, if you don’t add a `rows` attribute, they can be super teeny. This isn’t ideal with coarse pointers such as fingers and by proxy, `<textarea>` elements tend to be used for multiple lines of text. It makes sense to make that easier.

```css
/* Anything that has been anchored to should have extra scroll margin */
:target {
  scroll-margin-block: 5ex;
}
```

Finally, if an element is anchored, it makes sense to add a bit more space above it with `scroll-margin`, which is only accounted for if that element is targeted. A little tweak with lots of user experience power! You might want to adjust this if you have a fixed header though.

## Wrapping up

Will this reset last another 4 years? Maybe! The [other one](https://andy-bell.co.uk/a-modern-css-reset/) certainly hasn’t caused issues.

Regardless, it’s pretty useful as a base to start projects, here at [the studio](https://set.studio/). We don’t go back and retroactively update the other reset on client projects either because that one works absolutely fine.

Resets are one of those things that people get worked up about, but really, with browsers being so bloody good now, you probably don’t even need one in the first place. My advice is take bits you like from ones you find on the web and create your own, that **works for you and your team**.
