
> https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/

Anchor links (also called jump links) are an easy way to provide in-page navigation. For example, a table of contents could use anchor links to take readers straight to various sections in a page.

They’re super easy to set up, but sprinkle a little CSS on top and you can really make them shine. Let’s start with the basics and build from there.

## [A Humble Anchor Link](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#a-humble-anchor-link)

To create a page anchor, give an element an `id`. That’s it. You can use all sorts of elements as page anchors, though it’s pretty common to use headings.

```html
<h1 id="my-anchor">Page anchor</h1>
```

Now you can link to the page anchor by using `#` with the `id` as an `href`.

```html
<a href="#my-anchor">Jump to the page anchor</a>
```

There are two special values you can use as the `href` of an anchor link: `#top` or simply `#`. They both do the same thing, taking you to the very top of the page. No need to create a page anchor for these.

Let’s see these anchor links in action.

> **Demo**[Anchor Link: Basic](https://codersblock.com/assets/demos/anchor-links/basic)

Notice in the demo how clicking an anchor link adds a hash (like `#my-anchor`) to the page’s URL in the address bar — which can be copied and used to link directly to a page anchor, [like this](https://codersblock.com/assets/demos/anchor-links/basic#my-anchor).

Now let’s see what adding a little CSS can do.

## [Adding Smooth Scrolling](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#adding-smooth-scrolling)

In the previous demo, the jump to the page anchor is instant, which can be a little disorienting. Fortunately, we can enable smooth scrolling with just CSS.

```css
html {
  scroll-behavior: smooth;
}
```

Now give those anchor links another go.

> **Demo**[Anchor Link: Smooth](https://codersblock.com/assets/demos/anchor-links/smooth)

## [Adding Scroll Margin](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#adding-scroll-margin)

Our anchor links so far have scrolled the page anchor to the very top edge of the viewport. Wouldn’t it be nice if there was a little breathing room there? We can make that happen by setting `scroll-margin-top` on the page anchor.

```css
h1 {
  scroll-margin-top: 40px;
}
```

This will leave `40px` of space between the top of the viewport and the page anchor. Check it out.

> **Demo**[Anchor Link: Smooth + Margin](https://codersblock.com/assets/demos/anchor-links/smooth-and-margin)

This trick is super useful when you have a sticky header, to push page anchors down a bit so they aren’t positioned behind it.

## [Adding Targeted Page Anchor Styles](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#adding-targeted-page-anchor-styles)

You can use the CSS `:target` pseudo-class to add styling to a page anchor when jumping to it.

```css
h1:target {
  color: #71a819; /* green */
}
```

In this demo, clicking “Jump to the page anchor” enables the CSS above, making the page anchor text green. Clicking “Jump back to top” causes the `<h1>` to no longer be targeted, so the text will no longer be green.

> **Demo**[Anchor Link: Smooth + Margin + Styling](https://codersblock.com/assets/demos/anchor-links/smooth-and-margin-and-styling)

## [Fancier Target Styling](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#fancier-target-styling)

We can do more complex things with `:target` than just changing text color. Here’s a demo that highlights areas of content and animates a “Back to top” link into view.

> **Demo**[Anchor Link: Fancier Styling](https://codersblock.com/assets/demos/anchor-links/fancier-styling)

Here’s the (abbreviated) HTML to show how things are set up.

```html
<nav>
  <a href="#kiwis">Kiwis</a>
  <a href="#limes">Limes</a>
  <a href="#pears">Pears</a>
</nav>

<article>
  <h1 id="kiwis">Kiwis</h1>
  <p><!-- blurb about kiwis --></p>
</article>

<!-- more article elements here -->

<a class="back-to-top" href="#top">Back to top</a>
```

The article highlighting is accomplished with this CSS.

```css
/* border is initially transparent */
article {
  border: 3px solid transparent;
}

/* border turns green for an article when the targeted h1 is within */
article:has(h1:target) {
  border-color: #71a819;
}
```

And here’s the CSS to show/hide the “Back to top” link.

```css
.back-to-top {
  /* position link to be fixed in top right corner */
  position: fixed;
  top: 10px;
  right: 10px;

  /* link is initially faded out and shifted off right edge of viewport */
  opacity: 0;
  translate: calc(100% + 10px);

  /* half a second transition duration */
  transition: all 0.5s;
}

/* when body has a targeted h1 within, fade link in and shift into view */
body:has(h1:target) .back-to-top {
  opacity: 1;
  translate: 0px;
}
```

## [Nested Scrolling](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#nested-scrolling)

All the examples so far had a single scroll container: the page itself. However, it’s possible to have nested scroll containers — for example, a scrollable `<div>` in the page. If you put a page anchor within a nested scroll container, anchor links pointing to it will scroll all necessary containers to bring the target into view. Neat!

Here’s a demo. Note that the scroll positions feel a bit off — `scroll-margin` hasn’t been added. We’ll talk about why next.

> **Demo**[Nested Scroll Anchor Link: Without Padding](https://codersblock.com/assets/demos/anchor-links/nested-scroll-without-padding)

## [Scroll Margin vs. Scroll Padding](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#scroll-margin-vs-scroll-padding)

Now let’s fix those scroll positions. We’ve used `scroll-margin-top` before, but in Chrome and Edge, it won’t work here. The scroll margin won’t extend outside of the nested scroll container.

Fortunately, there’s another way to handle this. Instead of `scroll-margin`, we can use `scroll-padding`. They both give similar results, but the difference is:

- `scroll-margin` is used on the page anchor.
- `scroll-padding` is used on the scroll container.

Let’s update that demo with some `scroll-padding`.

```css
html {
  scroll-padding-top: 130px;
}

.slide-container {
  scroll-padding-inline: 20px;
}
```

This adds some generous top scroll padding to the page so the buttons stay in view. It also adds some inline (left and right) scroll padding to the scrollable `<div>` so each slide is nicely centered in the scroll container.

> **Demo**[Nested Scroll Anchor Link: With Padding](https://codersblock.com/assets/demos/anchor-links/nested-scroll-with-padding)

## [Scroll Into View with JavaScript](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#scroll-into-view-with-javascript)

You can also use JavaScript to scroll to a page anchor by calling `scrollIntoView()`. At its simplest, it looks something like this.

```javascript
const anchor = document.getElementById("my-anchor")
anchor.scrollIntoView()
```

Actually, you don’t even need a page anchor with an `id` on it. You can use `scrollIntoView()` to scroll to any element.

```javascript
const element = document.querySelector(".whatever")
element.scrollIntoView()
```

In either case, the scrolling will be the same as we’ve seen so far, but with some caveats.

1. The page’s URL in the address bar won’t be updated with a hash.
2. The element that is scrolled to is not considered targeted, so the CSS `:target` pseudo-class won’t work.
3. In Chrome, Firefox, and Edge, when `scrollIntoView()` is used inside an iframe, it can “break out” and also affect the scroll position of the parent page.

If these are showstoppers for you, and you really need to use JavaScript, there is a workaround.

```javascript
window.location.assign("#my-anchor")
```

This will behave as if an anchor link to `#my-anchor` was clicked.

## [ScrollIntoView() Options](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#scrollintoview-options)

Let’s talk more about `scrollIntoView()`. You can fine-tune how it scrolls by providing an (optional) object parameter. Here’s what it looks like with default values.

```javascript
element.scrollIntoView({
  behavior: "auto",
  block: "start",
  inline: "nearest",
})
```

The `behavior` property determines whether scrolling is instant or smooth.

- `'auto'` - Uses the value of `scroll-behavior` in CSS.
- `'instant'` - Jumps instantly to the element.
- `'smooth'` - Scrolls smoothly to the element.

The `block` property determines the vertical scroll alignment.

- `'start'` - Scrolls the top of the element to the top of the scroll container.
- `'center'` - Scrolls the center of the element to the center of the scroll container.
- `'end'` - Scrolls the bottom of the element to the bottom of the scroll container.
- `'nearest'` - Scrolls just enough to make the element fully visible within the scroll container — or if the element is taller than the scroll container, scrolls just enough so that the element fills the scroll container. If the element is already within or completely filling the scroll container, nothing happens.

The `inline` property has similar logic, but for horizontal scroll alignment.

- `'start'` - Scrolls the left of the element to the left of the scroll container.
- `'center'` - Scrolls the center of the element to the center of the scroll container.
- `'end'` - Scrolls the right of the element to the right of the scroll container.
- `'nearest'` - Scrolls just enough to make the element fully visible within the scroll container — or if the element is wider than the scroll container, scrolls just enough so that the element fills the scroll container. If the element is already within or completely filling the scroll container, nothing happens.

There can be situations where the scroll alignment you ask for cannot be achieved — usually when an element is at the edge of a scroll container and there’s not enough scroll space to do it. Your browser will still scroll as close as it can.

Alright, that was a lot of words. It’s probably easier to see for yourself, so here’s a scrolling playground to test things out.

> **Demo**[ScrollIntoView() Playground](https://codersblock.com/assets/demos/anchor-links/scroll-into-view-playground)

## [Behind-the-Scenes Notes](https://codersblock.com/blog/anchor-links-and-how-to-make-them-awesome/#behind-the-scenes-notes)

I’ll end with some technical notes from making this article. There were some quirky things I had to deal with that I want to share.

I usually embed Codepen demos right into my articles, using `<iframe>`. As you can see, I didn’t do that this time, for two reasons.

1. Clicked anchor links counts as navigation, which go into your browser’s history. This is true even when those links are inside an `<iframe>`. So if you clicked a couple anchor links in embedded demos, then tried to hit the back button on your browser, you’d still be on this blog page.
2. This was briefly mentioned earlier, but using `scrollIntoView()` in an `<iframe>` will affect the scroll position of the parent page. There is no sandbox option to fix this. Especially with the last “playground” demo, it was super weird playing with an embedded demo and having the entire page move around. In my testing, Safari was the only browser to not do this.

Another note, when I was researching `scroll-margin` and `scroll-padding`, I saw a lot of sources that confusingly only talked about their relevance to [scroll snapping](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_scroll_snap), to the point that I wondered if using them for page anchors was an unintentional hack. This is not the case, as I discovered that the CSS scroll snap spec itself was [amended to address this confusion specifically](https://www.w3.org/TR/css-scroll-snap-1/#change-2019-clarify-nonsnapping).
