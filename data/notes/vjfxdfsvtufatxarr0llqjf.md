
## [Clicking `<a>` element using Enter/Space key is not working even though it is focused (accessibility)](https://stackoverflow.com/a/66311677/5163033)

### Short Answer

To call a function you should use a `<button>` and an Event Listener. Use buttons for same page interactivity (calling JS functions) and use `<a href="some-location"...` for anything that causes the URL to update (navigation to a new page or to a location in the current document).

This is important for usability!

### Longer Answer

As you have marked this accessibility I will focus on that.

Any anchor `<a>` must have a valid `href` to be focusable and work as a hyperlink.

I have seen people offering the advice of `<a href="javascript:void(0)"`, **never** do this, this is an anti-pattern.

Also `<a href="#"` is also an anti-pattern as it does not provide any navigation.

This is all a hangover from HTML4 where you couldn't style a `<button>` element and a bad practice that just needs to go away now.

#### So what should I use?

If you are trying to make something that a user can interact with on the same page (something that calls a JavaScript function) then use a `<button>`.

If you are trying make something that causes navigation (either to a new page or to a place in the current document) then use a valid anchor `<a href="some-location">Some Location</a>` or `<a href="#document-fragment">Place in current document</a>`.

### Why does it matter?

For users of assistive technology (mainly screen reader users) the type of element used is important. The use of the correct element for the job is known as _semantics_.

An anchor with a valid `href` tells a screen reader user "Clicking this will result in navigation". It also lets them know that they need to press <kbd>Enter</kbd> to activate the link.

A `<button>` on the other hand tells a screen reader user "I will perform an action on this page". It also lets them know that they can press \`<kbd>Enter</kbd> **or** <kbd>Space</kbd> to activate the button.

This expected behaviour is essential for a screen reader user to not get confused or frustrated while using your website / web app.

It also helps with SEO, makes your mark-up easier to understand etc.

### So how to call a function from a page?

First as I said, use a `<button>`.

Rather than inlining the `click` handler, add it in your JS file.

In the below example I gave the button an `id="searchJavaScript` and then used `document.querySelector('#searchJavaScript');` to grab that button.

In reality you would use a better selector within `querySelector` based on your mark-up.

Then we use `.addEventListener('click'` to listen for any click events on that button.

You can [learn more about `addEventListener` here](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener).

```javascript
let jsButton = document.querySelector("#searchJavaScript")

jsButton.addEventListener("click", function () {
  alert("You clicked the JavaScript Search Button")
})
```

```html
<button id="searchJavaScript">JavaScript</button>
```

### But I need to do something before navigation occurs?

It should still be a valid anchor!

If you need to run some function before navigation occurs we can still easily do that with `event.preventDefault()`.

**You should still have a valid hyperlink**.

```javascript
let link = document.querySelector("a")

link.addEventListener("click", function (e) {
  e.preventDefault()
  console.log(
    "I will appear before navigation so you can set up whatever you need"
  )
  alert("I will appear before navigation")
  window.location.href = this.href
})
```

```html
<a href="https://google.com">Go to Google but run a function first</a>
```
