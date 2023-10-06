---
id: 0pt1h99anrpns3e7xkundxk
title: Draggable objects
desc: ""
updated: 1696396260373
created: 1696395596841
---

> [from Red Blob Games](https://www.redblobgames.com/making-of/draggable/)

Many of my interactive pages have a _draggable object_. I want the reader to move the object around, and I want the diagram to respond in some way. Here I’ll document the code I use to make this work with both mouse and touch input, using browser features that are widely supported since 2020. Here’s a common case I want to support:

Drag me

Drag the circle with mouse or touch

This is the simple model in my head:

[state.svg](https://www.redblobgames.com/making-of/draggable/build/state.svg)

However it’s not so simple! Mouses have multiple buttons. Touch events can include multiple fingers. Events can go to multiple destinations. Right click can trigger the context menu. I ended up with this basic recipe:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

- [ ] Text inside draggable
- [ ] Multiple fingers on same draggable
- [ ] Nested draggable elements

Like other recipes, it’s something that works for many cases, but is **meant to be modified**. On the rest of the page I’ll show how I got here and then variants of this recipe, including [how to handle text selection](https://www.redblobgames.com/making-of/draggable/#variant-text). I also use this same recipe to handle situations where I’m _not_ dragging an object around, like dragging this number left/right: `123`, or [painting on a canvas](https://www.redblobgames.com/making-of/draggable/targets.html#canvas-drag-to-paint).

I’ve tested this code on Gecko/Firefox (Mac, Windows, Linux, Android), Blink/Chrome (Mac, Windows, Linux, Android), and WebKit/Safari (Mac, iPhone, iPad). I have _not_ tested on hoverable stylus, hybrid touch+mouse devices, or voice input.

Also see my other pages:

1. [List of edge cases and list of dragging tests](https://www.redblobgames.com/making-of/draggable/targets.html)
2. [Test page to log the events, and unorganized notes](https://www.redblobgames.com/x/2251-draggable/)
3. [How I handled dragging events 2015–2018](https://www.redblobgames.com/x/1845-draggable/)

Note that this is _not_ the HTML [Drag and Drop API](https://www.redblobgames.com/x/2310-drag-drop-api/), which involves dragging an element _onto_ another element. For my diagrams, I’m dragging but _not_ dropping, and the scrubbable number example shows how I’m not necessarily even moving something around. So I need to read the mouse/touch events directly.

## 1 [🖱️ Mouse events only](https://www.redblobgames.com/making-of/draggable/#mouse-events)[#](https://www.redblobgames.com/making-of/draggable/#mouse-events)

When I first started implementing interactive diagrams ~20 years ago, touch devices weren’t common. I used `mousedown`, `mouseup`, and `mousemove` event handlers on the draggable element. If the move occurs while dragging, move the circle to the mouse position.

[mouse-local.svg](https://www.redblobgames.com/making-of/draggable/build/mouse-local.svg)

```js
function makeDraggableMouseLocal(state, el) {
  function mousedown(_event) {
    state.dragging = true
  }
  function mouseup(_event) {
    state.dragging = null
  }
  function mousemove(event) {
    if (!state.dragging) return
    state.pos = state.eventToCoordinates(event)
  }

  el.addEventListener("mousedown", mousedown)
  el.addEventListener("mouseup", mouseup)
  el.addEventListener("mousemove", mousemove)
}
```

**Try** the demo with a mouse:

Drag me

Drag using mouse events on circle

This might seem like it works but it works poorly.

- If you move the pointer quickly it is no longer over the circle, it stops receiving events.
- If you release the button while not on the circle, it will get stuck in the “dragging” state.

To fix these problems use `mousedown` on the circle to add `mousemove` and `mouseup` on the _document_. Then on `mouseup` remove the `mousemove` and `mouseup` from the document.

[mouse-document.svg](https://www.redblobgames.com/making-of/draggable/build/mouse-document.svg)

```js
function makeDraggableMouseGlobal(state, el) {
  function globalMousemove(event) {
    state.pos = state.eventToCoordinates(event)
    state.dragging = true
  }
  function globalMouseup(_event) {
    document.removeEventListener("mousemove", globalMousemove)
    document.removeEventListener("mouseup", globalMouseup)
    state.dragging = null
  }

  function mousedown(event) {
    document.addEventListener("mousemove", globalMousemove)
    document.addEventListener("mouseup", globalMouseup)
  }

  el.addEventListener("mousedown", mousedown)
}
```

Try it out. It works better.

Drag me

Drag using mouse events on document

This code doesn’t handle touch events.

## 2 [👆 Touch events](https://www.redblobgames.com/making-of/draggable/#touch-events)[#](https://www.redblobgames.com/making-of/draggable/#touch-events)

Mouse events use `mousedown`, `mouseup`, `mousemove`. Touch events instead use `touchstart`, `touchend`, `touchmove`. They behave a little differently. Touch events automatically _capture_ on `touchstart` and direct all `touchmove` events to the original element. This means we _don’t_ have to temporarily put an event handler on `document`. We can go back to the simpler logic in the first mouse example. If for any reason the browser needs to cancel the touch sequence, it sends `touchcancel`.

[touch.svg](https://www.redblobgames.com/making-of/draggable/build/touch.svg)

```js
function makeDraggableTouch(state, el) {
  function start(event) {
    event.preventDefault() // prevent scrolling
    state.dragging = true
  }
  function end(_event) {
    state.dragging = false
  }
  function move(event) {
    if (!state.dragging) return
    state.pos = state.eventToCoordinates(event.changedTouches[0])
  }

  el.addEventListener("touchstart", start)
  el.addEventListener("touchend", end)
  el.addEventListener("touchcancel", end)
  el.addEventListener("touchmove", move)
}
```

**Try** the demo with a touch device:

Drag me

Drag using touch events

This code doesn’t handle mouse events.

## 3 [🖱️👆 Pointer events](https://www.redblobgames.com/making-of/draggable/#pointer-events)[#](https://www.redblobgames.com/making-of/draggable/#pointer-events)

Handling both mouse and touch events requires lots of event handlers, and that’s what I used before 2021. Details→

From 2011 to 2014 I used [d3-drag](https://github.com/d3/d3-drag)<sup class="print-endnote">[1]</sup> in projects where I used d3. For my non-d3 projects, I ended up developing my own mouse+touch code, which I wrote about [in 2018](https://www.redblobgames.com/x/1845-draggable/).

By 2012 MS IE had added support for [pointer events](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events)<sup class="print-endnote">[2]</sup> which unify and simplify mouse+touch handling. [Chrome added support in 2017; Firefox in 2018; Safari in 2020](https://caniuse.com/pointer)<sup class="print-endnote">[3]</sup>.

Over the years browsers have changed the rules, including in 2017 when [Chrome changed some events to default to passive mode](https://developer.chrome.com/blog/scrolling-intervention/)<sup class="print-endnote">[4]</sup> which causes the page to scroll while trying to drag the object. This [broke some pages](https://github.com/WICG/interventions/issues/18#issuecomment-276531695)<sup class="print-endnote">[5]</sup>. Safari [made this change in 2018](https://github.com/WICG/interventions/issues/18#issuecomment-368703063)<sup class="print-endnote">[6]</sup>. Firefox also [made this change in 2018](https://bugzilla.mozilla.org/show_bug.cgi?id=1449268)<sup class="print-endnote">[7]</sup>.

[mouse-and-touch.svg](https://www.redblobgames.com/making-of/draggable/build/mouse-and-touch.svg)

Pointer events attempt to unify mouse and touch events. The [pointer capture](https://developer.mozilla.org/en-US/docs/Web/API/Element/setPointerCapture)<sup class="print-endnote">[8]</sup> feature lets us use the simpler logic that doesn’t require us to add/remove global event handlers to the document like we had to with mouse events.

[pointer.svg](https://www.redblobgames.com/making-of/draggable/build/pointer.svg)

This recipe is the starting point:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = true
  }

  function end(event) {
    state.dragging = false
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x, y }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
}
```

Much simpler! However, I almost always want to handle some extras, so I start with this instead:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

**Try** the demo with either a mouse or touch device:

Drag me

Drag using pointer events

Let’s look at each of the extras.

### 3.1. 🖱️ Fix: capture the mouse[#](https://www.redblobgames.com/making-of/draggable/#fix-capture)

The pointer capture feature lets us track the pointer even when it’s not on the circle, the diagram, or even the browser window. With mouse events we had to put event handlers on `document`, but pointer capture is simpler.

| Try this                                   | Watch for  | Circle 1 | Circle 2 |
| ------------------------------------------ | ---------- | -------- | -------- |
| drag quickly back and forth                | drag stops | yes ⛌    | no ✓     |
| drag outside diagram, come back in         | drag stops | yes ⛌    | no ✓     |
| drag outside diagram, let go               | drag stops | no ⛌     | yes ✓    |
| drag outside diagram, let go, come back in | drag stops | no ⛌     | yes ✓    |
| drag, alt+tab to another window            | drag stops | no ⛌     | yes ✓    |

Drag 1 Drag 2

Dragging without and with pointer capture

**Try** this demo with a mouse.

- Circle 1 doesn’t use pointer capture on mouse. Pointer capture is the default on touch devices.
- Circle 2 uses pointer capture on both mouse and touch devices.

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

### 3.2. 👆 Fix: scrolling with touch[#](https://www.redblobgames.com/making-of/draggable/#fix-scroll)

On touch devices, single-finger drag will scroll the page. But single-finger drag _also_ drags the circle. By default, it will do _both_! The simplest fix is to add CSS <kbd>touch-action: none</kbd> on the diagram. But this prevents scrolling _anywhere_ in the diagram:

Drag 1

Stop touch from scrolling anywhere on the diagram

**Try** dragging the circle on a touch device. It shouldn’t scroll. But then try scrolling by dragging the diagram. It doesn’t scroll either, but I want it to. I want to stop scrolling _only_ if dragging the circle, not when dragging the diagram.

| Try this     | Watch for    | Circle 1 | Circle 2 | Circle 3 | Circle 4 |
| ------------ | ------------ | -------- | -------- | -------- | -------- |
| drag circle  | page scrolls | no ✓     | yes ⛌    | yes ⛌    | no ✓     |
| drag diagram | page scrolls | no ⛌     | yes ✓    | yes ✓    | yes ✓    |

Drag 2 Drag 3 Drag 4

Dragging affects scrolling

**Try** these on a touch device.

- Circle 1 (<kbd>touch-action: none</kbd> on the diagram) stops scrolling on the circle and also on the diagram.
- Circle 2 (default) doesn’t stop scrolling on either.
- Circle 3 (<kbd>touch-action: none</kbd> on the circle only) behaves badly. It looks like the CSS has to be on the diagram to have an effect; applying it only to the circle is not enough.
- Circle 4 (<kbd>.preventDefault()</kbd> on `touchstart`) behaves the way I want, and this is the code for it:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

I use the <kbd>.preventDefault()</kbd> solution. Note that it needs to be on `touchstart`, not on `pointerstart`. It works in most situations but I’ve run into situations where it did not stop scrolling on certain systems.

### 3.3. 🖱️ Feature: handle drag offset[#](https://www.redblobgames.com/making-of/draggable/#feature-offset)

This isn’t necessary but it makes dragging feel nicer. If you pick up the edge of an object then you want to keep holding it at _that_ point, not from the center of the object. The solution is to remember where the center is relative to where the drag started. Then when moving the object, add that offset back in.

| Try this                 | Watch for    | Circle 1 | Circle 2 |
| ------------------------ | ------------ | -------- | -------- |
| drag from edge of circle | circle jumps | yes ⛌    | no ✓     |

Drag 1 Drag 2

Dragging feels better if relative to the initial pickup point

**Try** with the mouse: drag the circle from the edge. Watch Circle 1 jump whereas Circle 2 does not. The same effect happens on touch devices but your finger might hide the jump. The fix is to change the `dragging` state from `true` / `false` to the relative position where the object was picked up, and then use that offset when later setting the position:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

Tracking the offset makes dragging feel better. I’ve also written about this [on my page about little details](https://www.redblobgames.com/making-of/little-things/#drag-point).

### 3.4. 🖱️ Fix: context menu[#](https://www.redblobgames.com/making-of/draggable/#fix-contextmenu)

Context menus are different across platforms, and that makes handling it tricky. I want to allow context menus without them interfering with dragging the circle.

| System  | Activation                                                   |
| ------- | ------------------------------------------------------------ |
| Windows | right click (down+up), <kbd>Shift</kbd> + <kbd>F10</kbd> key |
| Linux   | right button down, <kbd>Shift</kbd> + <kbd>F10</kbd> key     |
| Mac     | right button down, <kbd>Ctrl</kbd> + left click              |
| iOS     | long press on text only                                      |
| Android | long press on anything                                       |

One problem is that I will see a `pointerdown` event and only _sometimes_ a `pointerup` event. That means I might think the button is still down when it’s not. It’s frustrating! I realized that I should only set the dragging state on _left_ mouse button, and ignore the right mouse button. Then I don’t have to worry about most of the differences.

I made some notes during testing, but most of them don’t matter for my use case.

Across platforms, it looks like Firefox lets the page see events outside the menu overlay, whereas Chrome doesn’t let the page see any events while the menu is up.

Windows, right click, no capture:

Firefox, Chrome, Edge

`pointerdown`, `pointerup`, `auxclick`, `contextmenu`

Windows, right click, capture:

Firefox

`pointerdown`, `gotpointercapture`, `pointerup`, `lostpointercapture`, `auxclick`, `contextmenu`

Chrome, Edge

`pointerdown`, `gotpointercapture`, `pointerup`, `auxclick`, `lostpointercapture`, `contextmenu`

Linux right click, no capture:

Firefox

`pointerdown`, `contextmenu`, `pointermove` while menu is up

Chrome

`pointerdown`, `contextmenu`, no `pointermove` while menu is up

Linux hold right down, no capture:

Firefox

`pointerdown`, `contextmenu`, `pointermove` while menu is up

Chrome

`pointerdown`, `contextmenu`, no `pointermove` while menu is up

Linux right click, capture:

Firefox

`pointerdown`, `contextmenu`, `gotpointercapture`, `pointermove` while menu is up tells us button released

Chrome

`pointerdown`, `contextmenu`, `gotpointercapture`; not until another click do we get `pointerup`, `lostpointercapture`

Linux hold right down, capture:

Firefox

`pointerdown`, `contextmenu`, `gotpointercapture`, `pointermove` while menu is up tells us button released; when releasing button, menu stays up but we get `pointerup`, `lostpointercapture`

Chrome

`pointerdown`, `contextmenu`, `gotpointercapture`, no `pointermove` while menu is up; when releasing button, menu stays up but we don’t get `pointerup`; not until another click do we get `pointerup`, click, `lostpointercapture`

Mac, ctrl + left click:

Firefox

`pointermove` with buttons≠0, `contextmenu` (no `pointerdown` or `pointerup`)

Chrome

`pointerdown` with button=left, `contextmenu` (no `pointerup`)

Safari

`pointerdown` with button=left, `contextmenu` (no `pointerup`); but subsequent clicks only fire `contextmenu`

Mac, right button down:

Firefox

`pointerdown` with button=right, `contextmenu` (no `pointerup`)

Chrome

`pointerdown` with button=right, `contextmenu` (no `pointerup`)

Safari

`pointerdown` with button=right, `contextmenu` (no `pointerup`); but subsequent right clicks only fire `contextmenu`

If we capture events on `pointerdown`, Firefox and Safari will keep the capture even after the button is released. Chrome will keep capture until you move the mouse, and then it will release capture. \[This seems like a Firefox/Safari bug to me, as pointer capture is supposed to be automatically released on mouse up\]

It’s frustrating that on Mac, there’s no `pointerup` or `pointercapture` when releasing the mouse button. On Linux, the `pointerup` only shows up if you click to exit the context menu. It doesn’t show up if you press <kbd>Esc</kbd> to exit. The workaround is to watch `pointermove` events to see when no buttons are set. Windows doesn’t seem to have these issues, as both `pointerdown` and `pointerup` are delivered before the context menu.

Android, long press:

Firefox

`pointerdown`, get capture, `contextmenu`, `pointerup`, lose capture

Chrome

`pointerdown`, get capture, `contextmenu`, `pointerup` or `pointercancel` (if the finger moves at all, this starts a scroll event which cancels the captured pointer), lose capture

What are my options?

- [The spec says about pointerdown](https://www.w3.org/TR/pointerevents/#the-pointerdown-event)<sup class="print-endnote">[9]</sup> that `preventDefault()`_not_ stop click or `contextmenu` events. I can `preventDefault()` on `contextmenu` to prevent the menu. But I still want to get `pointerup` and/or `pointercancel`! I think I have to treat `contextmenu` as the up event which means I’ll get multiple up events on Windows.
- [The spec says about the button property](https://w3c.github.io/pointerevents/#the-button-property)<sup class="print-endnote">[10]</sup> that `button` = 0 indicates the primary button. This is how I will exclude the middle and right buttons. But I still get a `pointerdown.left` on Mac/Chrome and Mac/Safari (but not on Mac/Firefox) so I also have to check for the <kbd>Ctrl</kbd> key.
- Button changes not communicated through `pointerdown` or `pointerup` can still be sent on `pointermove`. It’s mentioned as a workaround on [W3C’s pointerevents issues page](https://github.com/w3c/pointerevents/issues/408)<sup class="print-endnote">[11]</sup>.

| Try this         | Watch for          | Circle 1 | Circle 2 | Circle 3 | Circle 4 |
| ---------------- | ------------------ | -------- | -------- | -------- | -------- |
| right click      | circle turns blue  | yes ⛌    | yes      | no ✓     | no ✓     |
| right click      | context menu       | yes ⛌    | no       | no ✓     | no ✓     |
| middle click     | circle turns blue  | yes ⛌    | yes ⛌    | no ✓     | no ✓     |
| right drag       | circle is blue     | yes ⛌    | yes      | no ✓     | no ✓     |
| middle drag      | circle is blue     | yes ⛌    | yes      | no ✓     | no ✓     |
| ctrl+click (mac) | circle turns blue¹ | yes ⛌    | no ✓     | yes ⛌    | no ✓     |
| ctrl+click (mac) | context menu       | yes ⛌    | no ✓     | yes ⛌    | no ✓     |

¹ it will turn blue in Chrome and Safari but not in Firefox, which treats <kbd>Ctrl</kbd> + click differently

Drag 1 Drag 2 Drag 3 (Mac) Drag 4

Right mouse button down interferes with drag

**Try** with the mouse: right click or drag on the circles. Try dismissing the menu with a click elsewhere, or by pressing <kbd>Esc</kbd>. Behavior varies across browsers and operating systems.

- Circle 1 sometimes get stuck in a dragging state.
- Circle 2 uses <kbd>.preventDefault()</kbd> on `contextmenu`. This allows the right button to be used for dragging. However, it interferes with the default operation of middle click or drag, which is used for scrolling on some systems.
- Circle 3 drags only with the left button, but on Mac <kbd>Ctrl</kbd> + click on Chrome/Safari will trigger drag.
- Circle 4 drags only with the left button, if <kbd>Ctrl</kbd> isn’t pressed.

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    if (event.ctrlKey) return // ignore ctrl+click
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = true
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = false
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x, y }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

## 4 [🖱️ Variant: draggable text/images](https://www.redblobgames.com/making-of/draggable/#variant-text)[#](https://www.redblobgames.com/making-of/draggable/#variant-text)

These changes are needed if you have text or images inside your draggable element:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
    el.style.userSelect = "none" // if there's text
    el.style.webkitUserSelect = "none" // safari
  }

  function end(event) {
    state.dragging = null
    el.style.userSelect = "" // if there's text
    el.style.webkitUserSelect = "" // safari
  }

  function move(event) {
    if (!state.dragging) return
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
  el.addEventListener("dragstart", (e) => e.preventDefault())
}
```

### 4.1. 🖱️ Fix: text selection[#](https://www.redblobgames.com/making-of/draggable/#fix-user-select)

When dragging the circle, the text inside gets selected sometimes. To fix this, use CSS <kbd>user-select: none</kbd> on the circle. There are two choices: either we can apply it _all_ the time, or apply it _only_ while dragging. If I apply it all the time, then the text won’t ever be selectable.

| Try this        | Watch for        | Circle 1 | Circle 2 | Circle 3 |
| --------------- | ---------------- | -------- | -------- | -------- |
| drag circle     | text is selected | yes ⛌    | no ✓     | no ✓     |
| select all text | text is selected | yes      | no       | yes      |

Drag text 1 Drag text 2 Drag text 3

Dragging affects text selection

**Try** dragging quickly with the mouse. **Try** selecting all text on the page to see whether the text inside the circle is selectable when not dragging.

- Circle 1 never uses <kbd>user-select: none</kbd>
- Circle 2 always uses <kbd>user-select: none</kbd>
- Circle 3 uses <kbd>user-select: none</kbd> only when dragging

I think either Circle 2 or Circle 3’s behavior is a reasonable choice. Note that as of early 2023, Safari *still*  [doesn’t support the unprefixed version](https://caniuse.com/?search=user-select)<sup class="print-endnote">[12]</sup> ([tracking bug](https://bugs.webkit.org/show_bug.cgi?id=208677)<sup class="print-endnote">[13]</sup>), so we have to also set the prefixed version.

### 4.2. 🖱️ Fix: text and image drag[#](https://www.redblobgames.com/making-of/draggable/#fix-systemdrag)

Windows, Linux, and Mac support inter-application _drag and drop_ of text and images, and an alternative to copy/paste. This interferes with the object dragging on my pages. The fix is to <kbd>preventDefault()</kbd> on `dragstart`.

| Try this                 | Watch for       | Circle 1 | Circle 2 |
| ------------------------ | --------------- | -------- | -------- |
| select text, drag circle | page text drags | yes ⛌    | no ✓     |

**Select text** → \[from here

1 2

to here\] ←

Selected text interferes with dragging

**Try** this demo with a mouse. Select the text around the diagram, then drag Circle 1. On most desktop systems I’ve tested, text or image dragging takes priority over the circle dragging by default. Circle 2 prioritizes the circle dragging. Behavior varies a little bit across browsers and operating systems. The fix is one extra line:

## 5 [More cases](https://www.redblobgames.com/making-of/draggable/#more-cases)[#](https://www.redblobgames.com/making-of/draggable/#more-cases)

### 5.1. 👆 Feature: simultaneous dragging[#](https://www.redblobgames.com/making-of/draggable/#feature-simultaneous-dragging)

I think this is an edge case, but I was curious what it would take to support. Can we drag multiple objects at once, using different fingers or different mice?

For touch, the code I presented should already work! Go back to one of the previous demos and try it. However the code doesn’t handle using two fingers to drag the _same_ object. The fix is when handling `pointerdown`, save <kbd>event.pointerId</kbd> to `state.dragging`. Then when handling `pointermove`, ignore the even if it’s not the same `pointerId`. I don’t have that implemented here, but try it out [on my canvas dragging test](https://www.redblobgames.com/making-of/draggable/targets.html#canvas-drag-a-handle).

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    state.pointerId = event.pointerId // keep track of finger
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    if (state.pointerId !== event.pointerId) return // check finger id
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

What about mice? The [Pointer Events spec](https://www.w3.org/TR/pointerevents/#the-primary-pointer)<sup class="print-endnote">[14]</sup> says

> Current operating systems and user agents don’t usually have a concept of multiple mouse inputs. When more than one mouse device is present (for instance, on a laptop with both a trackpad and an external mouse), all mouse devices are generally treated as a single device - movements on any of the devices are translated to movement of a single mouse pointer, and there is no distinction between button presses on different mouse devices. For this reason, there will usually only be a single mouse pointer, and that pointer will be primary.

I think there isn’t any way to drag different objects with different mice.

### 5.2. 🖱️ Edge case: chorded button presses[#](https://www.redblobgames.com/making-of/draggable/#fix-chords)

So here’s a tricky one. If you are using multiple buttons at the same time, what happens? Mouse Events send `mousedown` for each button press and `mouseup` for each button release. But Pointer Events work differently. The [Pointer Events spec](https://www.w3.org/TR/pointerevents/#chorded-button-interactions)<sup class="print-endnote">[15]</sup> says that the _first_ button that was pressed leads to a `pointerdown` event, and the _last_ one that was released leads to a `pointerup` event. But that means we might get a up event on a different button than the down event!

[multiple-buttons.svg](https://www.redblobgames.com/making-of/draggable/build/multiple-buttons.svg)

| Try this                       | Watch for | Circle 1 | Circle 2 |
| ------------------------------ | --------- | -------- | -------- |
| left down, right down, left up | dragging  | yes ⛌    | no ✓     |

Drag 1 Drag 2

Multiple button presses is tricky

**Try** with the mouse: press the left button, press the right button (this may bring up a context menu but ignore it), then release the left button. Is the circle still dragging?

The fix is to check the button state in `pointermove`:

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    if (!(event.buttons & 1)) return end(event) // edge case: chords
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

Separately, the _pointer capture_ continues until you release _all_ the buttons, unless you explicitly release capture. I’m not handling this or many other edge cases.

### 5.3. 🖱️👆 Variant: nested dragging[#](https://www.redblobgames.com/making-of/draggable/#variant-nesting)

If the draggable element contains _another_ draggable element inside of it, both elements will handle the dragging. The fix is to add <kbd>.stopPropagation()</kbd> to prevent the inner draggable from passing events up to outer draggable. I don’t have a demo here, but [I made one elsewhere](https://play.vuejs.org/#eNq1Vk1zmzAQ/SsqkxnsqUOcyY06nbZpDumhzbQ5JDMcQswalICkkYSNS/nvXUngQOLaTT/sA9Lbt2L37bJQe++FCJYleKE3U3NJhSYKdCneRowWgktNaiJhQRqykLwgPlL9iEVszpnSpCKnxjqajjtk/QxZ0URnLXo8fcQzoGmmB4bOlMg4RUMdMWLXKWVpSBZxrmBiMMEp0yATvmIjWALTY8clRGdUBZ2LOSKpQlIFyzgvgRwSSw7mOcXL9YQk65CstxpvmjfuwBYspcTrVSxT0AEKdOkiOIuFLiW4III2rItkbJ2bfqyl2BOpze65X8GX7fEbT7ogo1cD9zFqiHGwNuYu39NhvuT18KZBUrUOnQZDh5vnDutNgE1XKwmKfjeu/6Raq9D1yy8rloVt4/y3snXOSnNxKbmI01hTzkZ/V9QXnPonJd91OBlIurcpVq3TQOa9nZH1O2N25EYJDhHcaChEHmvAHSGzhC5JqPQ6h9PIq7WMmVpwWYTk1q4NcXRQV42oJgf1Gi/j24lLACkHtV0hiqAL0KJu6eC7eP6QSl6yJCT+GvKcr/wJ8UsF8lBBDnPto4FxBggLrqiRChEJeG+6NCj2jeISMVMKv4k8pwj+3vWaOchhoTEJI0LXRAbfQi/FE14ptrDM3Z7wDNRnal7OM6VjiW0rbUnQoUewGhPy0QzQAkjt9PoxbZrrulXJbBzrSS16WsR3iuelNlpIJ7I/xfUd15pjqeymrYl/PBUVbrtqdPtBGSQkfVnZSsGhGxx71XW039F3yNyl8JD5Uo03Ks+OUEDX1e1qdtRrdvf3Jp5WOCoXNA3uFWf4orUPdeTNeSFoDvKLMKqryAu7xz3yYtO2nyymZenmqPXJYP6wBb9XlcEi7xJzA2kS2tgwExx/znz+7TNUuN4YC56UObJ3GL+CbQaM0dE+YE0x7B7PRnthPxdwGFyp80oDU11SJtDHIRd5+AlxtiP1x3BPghPrhzPFa34CpcvwOQ==)<sup class="print-endnote">[16]</sup>, where the red draggable is a child of the yellow draggable.

```js
function makeDraggable(state, el, options) {
  function start(event) {
    if (event.button !== 0) return // left button only
    event.stopPropagation() // for nested draggables
    let { x, y } = state.eventToCoordinates(event)
    state.dragging = { dx: state.pos.x - x, dy: state.pos.y - y }
    el.setPointerCapture(event.pointerId)
  }

  function end(event) {
    state.dragging = null
  }

  function move(event) {
    if (!state.dragging) return
    event.stopPropagation() // for nested draggables
    let { x, y } = state.eventToCoordinates(event)
    state.pos = { x: x + state.dragging.dx, y: y + state.dragging.dy }
  }

  el.addEventListener("pointerdown", start)
  el.addEventListener("pointerup", end)
  el.addEventListener("pointercancel", end)
  el.addEventListener("pointermove", move)
  el.addEventListener("touchstart", (e) => e.preventDefault())
}
```

### 5.4. 🖱️👆 Variant: dragging on canvas[#](https://www.redblobgames.com/making-of/draggable/#variant-canvas)

I normally work with SVG, but if working with a `<canvas>` (either 2D Canvas or WebGL), I can’t set the event handlers or mouse pointer shape on the _draggable_ element only. So I set the event handler on the `<canvas>` and then:

1. `pointerdown`, `touchstart`, `dragstart`: early <kbd>return</kbd> if not over a draggable object
2. `pointermove`: set the cursor based on whether it’s over a draggable object

### 5.5. Variant: hover with mouse[#](https://www.redblobgames.com/making-of/draggable/#variant-hover)

Sometimes I want to act on _hover_ with the mouse (no buttons pressed) but that doesn’t work with touch devices, so I use _drag_ with touch. I modify the recipe by removing the <kbd>if (!state.dragging)</kbd> line from `pointermove`.

{ DEMO? }

Do I need to release the capture? **Yes** releasing capture turns out to be important on many of my pages, like responsive-design

### 5.6. Variant: toggle paint

{ idea is that in addition to `dragging` I also want to capture the state of the first grid space I’m on, and then use that for all the move events; maybe this should go on a different page }

### 5.7. TODO: lostpointercapture

I know that `lostpointercapture` can be used to detect that we lost pointer capture, but I haven’t yet figured out all the situations in which it fires, and what I should do about them.

## 6 [Vue component](https://www.redblobgames.com/making-of/draggable/#vue)[#](https://www.redblobgames.com/making-of/draggable/#vue)

Here’s an attempt at a `<Draggable>` component in Vue v3, Options API:

```html
<template>
  <g
    :transform="`translate(${modelValue.x},${modelValue.y})`"
    @pointerdown.left="start"
    @pointerup="end"
    @pointercancel="end"
    @pointermove="dragging ? move($event) : null"
    @touchstart.prevent=""
    @dragstart.prevent=""
    :class="{dragging}"
  >
    <slot />
  </g>
</template>

<script>
  import { convertPixelToSvgCoord } from "./svgcoords.js"

  export default {
    props: { modelValue: Object }, // should be {x, y}
    data() {
      return { dragging: false }
    },
    methods: {
      start(event) {
        if (event.ctrlKey) return
        let { x, y } = convertPixelToSvgCoord(event)
        this.dragging = { dx: this.modelValue.x - x, dy: this.modelValue.y - y }
        event.currentTarget.setPointerCapture(event.pointerId)
      },
      end(_event) {
        this.dragging = null
      },
      move(event) {
        let { x, y } = convertPixelToSvgCoord(event)
        this.$emit("update:modelValue", {
          x: x + this.dragging.dx,
          y: y + this.dragging.dy,
        })
      },
    },
  }
</script>

<style scoped>
  g {
    cursor: grab;
  }
  g.dragging {
    user-select: none;
    cursor: grabbing;
  }
</style>
```

and here’s the same thing in the Composition API:

```html
<template>
  <g
    :transform="`translate(${modelValue.x},${modelValue.y})`"
    @pointerdown.left="start"
    @pointerup="end"
    @pointercancel="end"
    @pointermove="dragging ? move($event) : null"
    @touchstart.prevent=""
    @dragstart.prevent=""
    :class="{dragging}"
  >
    <slot />
  </g>
</template>

<script setup>
  import { ref } from "vue"
  import { convertPixelToSvgCoord } from "./svgcoords.js"

  const props = defineProps({
    modelValue: Object, // should be {x, y}
  })

  const emit = defineEmits(["update:modelValue"])

  const dragging = ref(false)

  function start(event) {
    if (event.ctrlKey) return
    let { x, y } = convertPixelToSvgCoord(event)
    dragging.value = { dx: props.modelValue.x - x, dy: props.modelValue.y - y }
    event.currentTarget.setPointerCapture(event.pointerId)
  }

  function end(event) {
    dragging.value = null
  }

  function move(event) {
    let { x, y } = convertPixelToSvgCoord(event)
    emit("update:modelValue", {
      x: x + dragging.value.dx,
      y: y + dragging.value.dy,
    })
  }
</script>

<style scoped>
  g {
    cursor: grab;
  }
  g.dragging {
    user-select: none;
    cursor: grabbing;
  }
</style>
```

This component only handles SVG elements, as that’s my primary need. You’ll have to modify it if you’re dragging HTML elements. You can use _computed setters_ on the model value if you want to apply constraints like bounds checking or grid snapping. If you’re using Vue v2 (whether Options API or Composition API), you’ll need to change the v-model prop from `modelValue` to `value` and the event from `update:modelValue` to `input`.

To use this component, create position variables (`data` in Options API or `ref` in Composition API) of type `{x, y}`, and then draw the desired shape as the child slot of the draggable component. In this example, I have `redCircle` and `blueSquare` positions:

```html
<svg viewBox="-100 -100 200 200" style="background: #eee">
  <Draggable v-model="redCircle">
    <circle r="10" fill="hsl(0 50% 50%)" />
  </Draggable>
  <Draggable v-model="blueSquare">
    <rect x="-10" y="-10" width="20" height="20" fill="hsl(220 50% 50%)" />
  </Draggable>
</svg>
```

I put a full example of this [on the Vue Playground](https://play.vuejs.org/#eNrtV2tv2zYU/SsXXofImS2lAfbFSfbyimEYhgZIUGyYh1WWrmQ2kqiRlB8z/N93SD0sO26WtRj2pQZsi+S5l/d5RG4H35alv6x4MBkE58TrMC8zJplQrMKUwiLGgywpkYr0MiXOOOfC6KtZQURRWNCcKZexSATHZCStpHqglTALWpg86/BYkrWMZsaSKfUkCFarla84nmdynoY5az+SeZCHD6JIxzIJrAlpOM84oPNgVsyKax0pURroMFX5lVUn8lIqQ1vFyY4SJXM6gzNnbqsgaJe/bxU1ED/oZl6XRshC2xDUUv8sMpWAaGHl9mL2G0GRITg0FSqC5A2eE2+7ntCXFyPaTGh8ebEbOngNnWcV3/1ZhaqPHTfgBnsd1E7DXQwMIz+hYef8tc3IUvDqO7m+mQ3GLy8urDQkLwjPswFps8kYS/MwekiVrIp4Qp8x82zgFEDF3s/lGHnkDOjOgw4GYFT7pLD+0qpORGaxC515F/Dvc/sdYj5oNe8D9tRe+xD0N1McGWp8gs5N97QSsVlgdGkHCxbpwrSjnkGXl88yCaFdpni6DnphHYwG78s0euQoAWmteGJUWGj0SA4D3rqBxXgvts7NNyGc9Ne70cF4sxu+nQ1qBd+UUhSGVSxXhZ9xYp3SJlTmGFCVWOEihlftFJowcqF004fwXC5t+l0joanoa/TqEnbxEk05pAkVVZZ1QkZW0cJt65fKQSBrd7Lyj+cb36Ms1BoT23aX3b66dCZNE/7r4FGojxu67qKnWrpdQ/ssWZlbsebsXt4t06mUKm7hvs1rZGe0/04f92cJPtPot5gTUfCtHXnb2t59dib0ev7OFiFIRC9klcWW6LZrdObOYps23mvlXJhO6SsMtPfbWVXG8HSyV3v2+9C63Qp1eam7PwkzzVaxRSRVEdnCQw8j8F6TscZQkVA940dGZT/xZggFplJFzbGUMYLkjIXq08FqNDYCrSX+0poJoW0MKnKh8vs1TGOC2hj09Ghtg7XNrtHXGFcphf/7UKVsfCT5ti7LaVjCWG5caGr1x7g2BvE98B9lfeT9I2NtFZ+UddV+KPyvQ2Mz651I5ajVSIRQremLI7v8eD1qAYjX5gRg0wCaaoL1h2zv6Jt0JEuOXROltCUEVUs1oVSF8ysrg2m/q6QtVZrVWOPFGxn0tyz46kBkDpQTw1ZW/RHl9d6Hn+juP6K7g5PLh1EZr5006CasMmhx88b15IR6YW95bDd6H5OhnUITeuiPhkLw0Lo2IUdJtEPBoFRnBhTJZiFju0lb26f46Tkc9UHNaD9mIfS+4BuqcpOnmep46YCoPpKsXPd2bW6p6o/HkTg2uKOrQ+kTZPVxMXrxDOrq0deBmX326jHYEaYlsB6J9X3a2Z//mdn6/eMuOec0rYNYt5gLHeIKiCgQJ9JlGDF5eHuYBVMZpjy0F5u7Nz/0ULDtvEXa246o0dhsRAtZSGUtVqxLcKlY4tjMWvyFuVF9gg3qo6sN07m7ZDWn+KG76DTN3b3Fnkr6CFesmxMF3JVQfdKwN4UbQH0wLiv48qq+mPXOCyUAgPmRYjgIiKt/r81qiZaChnqnTODvl25lc7Tya7uC+dLPQ6PE+r59Z3h2E1h4h424mN7/7A19YR3U7A3b3RoqKjFEQge7vwFtIua8)<sup class="print-endnote">[17]</sup>, with both Options API and Composition API components.
