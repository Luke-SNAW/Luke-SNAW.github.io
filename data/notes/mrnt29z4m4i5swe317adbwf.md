
> https://nolanlawson.com/2022/05/21/the-balance-has-shifted-away-from-spas/
> There’s a feeling in the air. A zeitgeist. SPAs are no longer the cool kids they once were 10 years ago.

Hip new frameworks like [Astro](https://astro.build/), [Qwik](https://qwik.builder.io/docs/overview), and [Elder.js](https://elderguide.com/tech/elderjs/) are touting their MPA capabilities with “0kB JavaScript by default.” Blog posts are making the rounds listing [all the challenges](https://dev.to/tigt/routing-im-not-smart-enough-for-a-spa-5hki) with SPAs: history, focus management, scroll restoration, Cmd/Ctrl-click, memory leaks, etc. [Gleeful potshots](https://williamkennedy.ninja/javascript/2022/05/03/in-defence-of-the-single-page-application/) are being taken against SPAs.

I think what’s less discussed, though, is how the context has changed in recent years to give MPAs more of an upper hand against SPAs. In particular:

1. Chrome implemented [paint holding](https://developer.chrome.com/blog/paint-holding/) – no more “flash of white” when navigating between MPA pages. ([Safari already did this.](https://twitter.com/xeenon/status/1125981836591620097))
2. Chrome implemented [back-forward caching](https://web.dev/bfcache/) – now all major browsers have this optimization, which makes navigating back and forth in an MPA almost instant.
3. Service Workers – once experimental, now effectively [100% available](https://caniuse.com/serviceworkers) for those of us targeting modern browsers – allow for offline navigation without needing to implement a client-side router (and all the complexity therein).
4. [Shared Element Transitions](https://github.com/WICG/shared-element-transitions/), if accepted and implemented across browsers, would also give us a way to animate between MPA navigations – something previously only possible (although difficult) with SPAs.

This is not to say that SPAs don’t have their place. Rich Harris has [a great talk](https://www.youtube.com/watch?v=860d8usGC0o) on “transitional apps,” which outlines some reasons you may still want to go with an SPA. For instance, you might want an omnipresent element that survives page navigations, such as an audio/video player or a chat widget. Or you may have an infinite-loading list that, on pressing the back button, returns to the previous position in the list.

Even teams that are not explicitly using these features may still choose to go with an SPA, just because of the “unknown” factor. “What if we want to implement navigation animations some day?” “What if we want to add an omnipresent video player?” “What if there’s some customization we want that’s not supported by existing browser APIs?” Choosing an MPA is a big architectural decision that may effectively cut off the future possibility of taking control of the page in cases where the browser APIs are not quite up to snuff. At the end of the day, an SPA gives you full control, and many teams are hesitant to give that up.

That said, we’ve seen a similar scenario play out before. For a long time, jQuery provided APIs that the browser didn’t, and teams that wanted to sleep soundly at night chose jQuery. Eventually browsers caught up, giving us APIs like [`querySelector`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector) and [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/fetch), and jQuery started to seem like unnecessary baggage.

I suspect a similar story may play out with SPAs. To illustrate, let’s consider Rich’s examples of things you’d “need” an SPA for:

- **Omnipresent chat widget:** use Shared Element Transitions to keep the widget painted during MPA navigations.
- **Infinite list that restores scroll position on back button:** use [`content-visibility`](https://web.dev/content-visibility/) and maybe store the state in the Service Worker if necessary.
- **Omnipresent audio/video player that keeps playing during navigations:** not possible today in an MPA, but who knows? Maybe the [Picture-in-Picture API](https://developer.mozilla.org/en-US/docs/Web/API/Picture-in-Picture_API) will support this someday.

To be clear, though, I don’t think SPAs are going to go away entirely. I’m not sure how you could reasonably implement something like Photoshop or Figma as an MPA. But if new browser APIs and features keep landing that slowly chip away at SPAs’ advantages, then more and more teams in the future will probably choose to build MPAs.

Personally I think it’s exciting that we have so many options available to us (and they’re all so much better than they were 10 years ago!). I hope folks keep an open mind, and keep pushing both SPAs and MPAs (and “transitional apps,” or whatever we’re going to call the next thing) to be better in the future.

_**Follow-up:** [More thoughts on SPAs](https://nolanlawson.com/2022/05/25/more-thoughts-on-spas/)_
