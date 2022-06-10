---
id: njnid1kj5jhb9lp6krb9dfr
title: How to prevent buttons from causing a form to submit with HTML
desc: ""
updated: 1654936019634
created: 1654935995253
---

https://gomakethings.com/how-to-prevent-buttons-from-causing-a-form-to-submit-with-html/

By default, a `button` has an innate `type` property of `submit`. When tapped, clicked, or activated inside a form, it will cause that form to submit (and trigger a corresponding `submit` event).

```html
<form id="say-hi">
  <button>Activate Me</button>
</form>
```

```js
let form = document.querySelector("#say-hi");
form.addEventListener("submit", function () {
  console.log("Someone said hi!");
});
```

Every now and then, you have a button inside a form that’s used for some other interaction, and should _not_ cause the form to submit.

I often see people use JavaScript to detect those buttons, and run `event.preventDefault()` to stop the default form submit behavior from running. I used to be one of those people.

```html
<form id="say-hi">
  <button>Activate Me</button>
  <button id="toggle-something">Toggle Something</button>
</form>
```

```js
form.addEventListener("submit", function (event) {
  // Ignore the #toggle-something button
  if (event.submitter.matches("#toggle-something")) {
    event.preventDefault();
  }

  console.log("Someone said hi!");
});
```

A while back, though, [my friend Eric Bailey](https://ericwbailey.design/) taught me a much simpler way to handle this: add `type="button"` to the button.

```html
<form id="say-hi">
  <button>Activate Me</button>
  <button id="toggle-something" type="button">Toggle Something</button>
</form>
```

Now, clicking, tapping, or otherwise activating the `#toggle-something` button will not cause a `submit` event to run.
