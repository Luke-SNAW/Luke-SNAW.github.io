---
id: h8arxu6s90wieoccgdj3c1b
title: Don't disable buttons
desc: ""
updated: 1699492266630
created: 1699488011131
---

> https://gomakethings.com/dont-disable-buttons/
>
> `disabled` shouldn't block focus - [danShumway](https://news.ycombinator.com/item?id=38196458)

Today I want to talk about why developers do it, why it’s bad, and what you can do instead. Let’s dig in!

## Why developers disable buttons [#](https://gomakethings.com/dont-disable-buttons/#why-developers-disable-buttons)

Typically, I see the pattern used to prevent a form from being submitted a second time while waiting for the form is processed.

Often, you’re waiting for an API response that may take a few moments, and you don’t want the user to submit the form again until the original response is processed.

```js
form.addEventListener("submit", function (event) {
  // Don't let the form reload the page
  event.preventDefault()

  // Get the submit button and disable it
  let btn = form.querySelector("button")
  btn.addAttribute("disabled", "")

  // Do more form stuff...

  // re-enable the button after the API responds
  btn.removeAttribute("disabled")
})
```

With the `button` disabled, it cannot be clicked again.

## Why this pattern is bad [#](https://gomakethings.com/dont-disable-buttons/#why-this-pattern-is-bad)

For starters, it doesn’t really do what you want it to.

Just because the `button` is `disabled` doesn’t mean the form can’t be submitted. Someone could focus on one of the form fields, then press the `enter` or `return` key, and the form would submit.

But it’s also horrible for accessibility.

Elements with the `disabled` attribute cannot receive focus, which creates confusing situations for screen reader users and people who [navigate the web with a keyboard](https://gomakethings.com/navigating-the-web-with-a-keyboard/).

If the `button` is the current item in focus when you add the `disabled` attribute (for example, if someone just pressed it to submit the form), the element actually loses focus, which shifts to the `document` element.

For a screen reader user, this is particularly jarring, as now you’re in a totally different place on the page.

So to recap, it doesn’t do what you actually want it to _and_ it breaks your application for a segment of your users.

## A better way [#](https://gomakethings.com/dont-disable-buttons/#a-better-way)

So, what should you do instead?

I personally prefer to add an attribute to the `form` as its being submitted, and remove it after all of the form actions are done. Whenever a `submit` event happens, I check for that attribute first. If it exists, I end the event handler early to prevent multiple form submissions.

```js
form.addEventListener("submit", function (event) {
  // Don't let the form reload the page
  event.preventDefault()

  // If the form is already submitting, do nothing
  if (form.hasAttribute("data-submitting")) return

  // Add the [data-submitting] attribute to stop multiple submissions
  form.setAttribute("data-submitting", "")

  // Do more form stuff...

  // Remove the [data-submitting] attribute
  form.removeAttribute("data-submitting")
})
```

This preserves focus on your form elements and avoids any weird accessibility issues, prevents duplication form submissions, and also prevents keyboard actions on other form fields from submitting the form.

You can also style form elements to “appear” disabled using the `[data-submitting]` CSS selector…

```css
[data-submitting] button {
  opacity: 0.8;
}
```

Don’t forget to also include [an ARIA live region](https://gomakethings.com/how-and-why-to-use-aria-live/) and display form status messages throughout the process.
