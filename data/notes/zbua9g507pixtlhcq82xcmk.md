
## [Smooth scrolling links with only CSS](https://gomakethings.com/smooth-scrolling-links-with-only-css/)

### [Scroll Behavior](https://gomakethings.com/smooth-scrolling-links-with-only-css/#scroll-behavior)

### [Why you might still want to use a JavaScript solution](https://gomakethings.com/smooth-scrolling-links-with-only-css/#why-you-might-still-want-to-use-a-javascript-solution)

I actually expect to use this approach more and more, [my Smooth Scroll plugin](https://github.com/cferdinandi/smooth-scroll) less and less.

1. I’ve found that, for long scrolls, the animation with scroll-behavior can be janky. This is surprising. I would have expected the CSS to tie into the browser’s frame refresh rate to prevent that from happening.
2. The scroll-behavior property has no easing or timing support. If you want to control how fast the animation runs, or the easing pattern in which it animates, you need JavaScript.
3. You always want to it work across browsers. A JavaScript solution can get you more broad browser support.

## [Scroll-Driven Animations: You want overflow: clip, not overflow: hidden](https://www.bram.us/2024/02/14/scroll-driven-animations-you-want-overflow-clip-not-overflow-hidden/)

Because `overflow: hidden` creates a scroll container it can interfere with the Scroll-Driven Animations scroller lookup mechanism. The fix is to use `overflow: clip` instead.
