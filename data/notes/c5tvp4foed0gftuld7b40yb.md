
> https://darekkay.com/blog/debugging-dynamic-content/

The following button displays a big outline on hover/focus — **which color value is it exactly**?

CSS effect

We can inspect the hover/focus styles with [browser dev tools](https://umaar.com/dev-tips/43-trigger-pseudo-class/). Press the `:hov` button in the Rules (Firefox) or Styles (Chrome) tab and activate the `:focus` pseudo class:

[Firefox DevTools: Rules panel with the :focus pseudo class active.](https://darekkay.com/blog/css-focus.png)

But how do we debug _dynamic_ changes, i.e., effects triggered by JavaScript? Try debugging the following hover/focus effect:

JavaScript effect

You might notice that the first method doesn't work here, because the effect is based on JavaScript `focus`/`mouseenter` events. That's why debugging tooltips/popovers is often more difficult.

## [Emulate a focused page](https://darekkay.com/blog/debugging-dynamic-content/#emulate-a-focused-page)

There is a setting in Chrome that makes JavaScript `focus` events "semi-persistent" (see a [demo](https://twitter.com/simevidas/status/1376281628260114432) from Šime Vidas). Go to the _"Rendering"_ tab in the DevTools and select the _"Emulate a focused page"_ checkbox. Now, focus styles will remain active even after switching to the element inspector:

[Chrome's 'emulate a focused page' setting](https://darekkay.com/blog/emulation.png)

This method doesn't cover the `:hover` case, and it is only available in Chromium browsers, but it's sufficient in many cases.

## [Trigger debugger on DOM changes](https://darekkay.com/blog/debugging-dynamic-content/#trigger-debugger-on-dom-changes)

Another way to inspect dynamic styles is to [break on DOM tree modifications](https://www.matuzo.at/blog/dev-tools-debugging-dom-tree-modifications/):

1. Right-click the button in the DOM inspector.
2. Select "Break on" and "attribute modification".
3. Trigger the effect (hover or focus the button).

[DevTools screenshot](https://darekkay.com/blog/dom-modifications.png)

The browser will freeze and make the element inspector work out of the box:

[Active Chrome debugger](https://darekkay.com/blog/debugger.png)

## [Trigger debugger after a few seconds](https://darekkay.com/blog/debugging-dynamic-content/#trigger-debugger-after-a-few-seconds)

Finding the right element to "listen" to in the last method is sometimes tricky. Instead, I often prefer the following little hack. Paste the following into the browser dev tools console, trigger the effect and wait for the browser to freeze after 3 seconds (3000 ms):

```js
setTimeout(() => {
  debugger
}, 3000)
```

Try out this **bookmarklet** for easier access: [Debugger](<javascript:(function()%7BsetTimeout(()%20%3D%3E%20%7B%20debugger%20%7D%2C%203000)%7D)()>). Drag and drop this link onto your bookmarks bar, open the browser dev tools and click the bookmark.

Here's a CodePen playground: [https://codepen.io/darekkay/pen/WNoroBb](https://codepen.io/darekkay/pen/WNoroBb)
