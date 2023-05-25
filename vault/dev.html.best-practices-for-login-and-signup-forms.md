---
id: ae6zb2sr29o5080d3m1uixr
title: 11 HTML best practices for login & sign-up forms
desc: ""
updated: 1684998299336
created: 1684995164447
---

> https://evilmartians.com/chronicles/html-best-practices-for-login-and-signup-forms

Most websites have login or sign-up forms; they’re a critical part of business conversion. However, even popular sites fail to implement the 11 best practices mentioned in this article, and thus have at least one mistake. So, read this post, and then check your forms and improve your UX by using HTML technologies the way they should be used.

In general, sign-in and login forms are very simple. For most websites, they feature just 2 inputs and a submit button. But, even with this simple HTML structure, many websites still have little mistakes.

Since this type of form is simple and has many chances for error, they present a good learning environment both for learning about some new HTML features, and to master the skills needed to produce the best user experience **with any kind of form**.

## Think about a password-less process instead of email/password

Before we get to the practices, a quick note: in this article, we’ll work with a classic email/password form as an example. However, in terms of security, passwords are actually the worst way to have users login, and this method has many, well-known weaknesses. Let’s quickly look at just a couple:

1. [This report on Verison’s 2018 data breach](https://www.researchgate.net/publication/324455350_2018_Verizon_Data_Breach_Investigations_Report) says that over 70% of people reuse passwords across websites. Attackers could potentially find a cross-website shared password in some leaked data from one website and use it to steal an account on another website. Additionally, compared to a password-less option, like those we’ll discuss below, implementing 2FA as a solution would reduce UX.
2. Users constantly forget their passwords, and resetting passwords takes too much time. According to [this report from Transmit Security](https://www.transmitsecurity.com/wp-content/uploads/transmit-security-passwordless-report-the-impact-of-passwords-on-your-business.pdf), 55% of consumers have stopped using a website because the login process was too complex.

> If you want to improve your login form, a first step would be thinking about a password-less option.

Here are my favorite password-less options right now:

1. Instead of a DIY implementation, use a secure, well-engineered and maintained third-party solution, such as [Auth0](https://auth0.com/) or [Amazon Cognito](https://aws.amazon.com/cognito/). For several of our client projects, including the ones with the highest security requirements, we used one of those methods to authenticate.
2. The new **passkey standard** suggested by [Apple](https://developer.apple.com/videos/play/wwdc2022/10092/) and [Google](https://developers.google.com/identity/passkeys). [This demo](https://www.passkeys.io/) and [article in New York Times](https://www.nytimes.com/wirecutter/blog/what-are-passkeys-and-how-they-can-replace-passwords/) explain how it works and why it’s better.
3. Implementing an email with **sign-in link** (many users utiize the `Remember password` feature with every login anyway).

You can also combine these options, for instance, using a passkey for users with new browsers and sign-in links for users without passkeys.

With that out of the way, let’s move on to the 11 best practices for login and sign up forms. (While reading, keep in mind that almost all of these guidelines are also valid for any type of form.)

## 1. Set `autocomplete`

```diff
- <input type="email">
+ <input type="email" autocomplete="username">
- <input type="password">
+ <input type="password" autocomplete="current-password">
  <button>Login</button>
```

Password managers are the only option to reduce security risks on email/password forms (but even they don’t fix all of risks). This is why it is important to give password managers a hand.

The `<input>` tag has the very useful [`autocomplete`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete) attribute. It also allows password managers to distinguish a login form (`current-password`) from a sign-up form (`new-password`).

Let’s take a look:

```diff
  <label>
    New password:
-   <input type="password">
+   <input type="password" autocomplete="new-password">
  </label>
  <label>
    Confirm password:
-   <input type="password">
+   <input type="password" autocomplete="new-password">
  </label>
  <button>Sign Up</button>
```

Don’t set `autocomplete="off"` if you don’t know what are you doing! Doing so could lessen the user experience. We should only use this setting when we need to to hide very sensitive data (like a “symptoms” field on a medical website).

> The [`autocomplete="off"` hack](https://stackoverflow.com/questions/5985839/bug-with-firefox-disabled-attribute-of-input-not-resetting-when-refreshing) addresses that when dynamically setting `disabled`, state is not reset upon refresh. Only set `off` for the submit `<button>`, not the entire form.

## 2. Set `type="email"`

```diff
  <label>
    E-mail:
-   <input type="text" autocomplete="username">
+   <input type="email" autocomplete="username">
  </label>
```

One of the most common mistakes with login forms is using `type="text"` on an e-mail field instead of `type="email"`. Why is this attribute important?

1. Browsers will suggest the user’s email in an autocomplete popup (even if the user is opening a website for a first time).
2. On touch-devices, the user will be prompted with a specific, more comfortable keyboard designed for entering e-mails.
3. It enables built-in e-mail validation.

> If your form allows for entering either a username or email within a single field, then, still, make sure to use [`inputmode="email"`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inputmode) to enable the email keyboard. Overall, this is still way more convenient for users.

If you don’t like the browser’s built-in validation, don’t set `type="text"`. Instead, use the [`novalidate`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form) attribute.

## 3. All clickables should use `<button>` or `<a>`, not `<div>` or `<span>`

```diff
- Forgot your password? <span>Reset it here</span>.
+ Forgot your password? <a href="/restore">Reset it here</a>.

- <div>Login</div>
+ <button>Login</button>
```

Links change the current page, and we should use `<a>` for all links. Buttons don’t change the page’s URL and only change the state on current page; we should use `<button>` for all buttons.

> For more accessibility tips, read this.
>
> [Accessible design from the get-go](https://evilmartians.com/chronicles/accessible-design-from-the-get-go)

Using the `<a>` tag has many benefits compared to `<span onClick={…}>`. For instance, the user can open a link in a new tab or see new the URL before clicking.

By using `<button>` instead of `<div>`, you make your website more accessible and improve keyboard UX: screen-readers will tell users when they’re dealing with a button; buttons will have `:focus` state for an improved keyboard UX.

Also, we should use `<button>` for a show/hide password feature; don’t forget about `aria-label` if you’re using an icon-only button:

```html
<button type="button" aria-label="Show password">
  <div class="eye-icon">
</button>
```

One more thing here: `<a>` and`<button>` are also good for development purposes. By always using `<a>`/`<button>` for interactive elements, you can easier create a CSS selector for all interactive elements:

```css
button,
a {
  cursor: pointer; /* Using pointer is controversial, this is just an example */
}
```

> If you have non-submit buttons in your form (just [don’t use a `Clear`](https://www.nngroup.com/articles/reset-and-cancel-buttons/) button) set `type="button"`; any buttons without `type="button"` will trigger the form’s submit on click.

## 4. Wrap the fields and submit `<button>` within `<form>` tags.

```diff
- <div>
+ <form>
    <label>Email: <input type="email" autocomplete="username"></label>
    <label>Password: <input type="password" autocomplete="current-password"></label>
+   <button>Login</button>
+ <form>
- </div>
- <button>Login</button>
```

Be sure to wrap all the form’s fields and its submit `<button>` within `<form>` tags. Form submission using `Enter` only works if the fields are inside `<form>` tags and there is a single submit button. (Additionally, users taking advantage of screen-readers will appreciate the better navigation this implementation provides.)

## 5. Avoid using `placeholder` as a `<label>`

```diff
- <input placeholder="E-mail" type="email" autocomplete="username">
+ <label>
+   E-mail:
+   <input type="email" autocomplete="username">
+ </label>
```

The `placeholder` attribute was created to show an example of a potential input, not to describe that input. Thus, I would completely advise against using it as a substitute for the `<label>` tag. Moreover, placeholder values will be hidden while users are entering the data, and they also often have contrast issues.

> Even as a `DD/MM/YYYY` format hint it’s better to avoid `placeholder` and write the hint on a separate line.

> ## The placeholder attribute should **not** be used as an alternative to a label.
>
> HTML Living Standard

That said, this is not so critical for short email + password forms, but on larger forms [placeholder’s issues](https://www.smashingmagazine.com/2018/06/placeholder-attribute/) are more obvious.

> Using `for`/`id` in `<label>` isn’t the only option; we can wrap `<input>` tags inside `<label>` without using `for`/`id`.

## 6. Wrap checkbox inputs within `<label>` tags

```diff
- <input type="checkbox"> I agree with the privacy policy
+ <label>
+   <input type="checkbox"> I agree with the privacy policy
+ </label>
```

By default, checkbox inputs have very a small size, and thus a small area where clicks will be detected. This means users need more time to precisely place the cursor where it needs to be. But if a checkbox input is wrapped in `<label>` tags, then clicking on its text will also change the checkbox value. (Also, note that each individual checkbox input will need its own `<label>` tags.)

When doing this, it’s also better to add a clear `:hover` effect to show users that they can click on the text to trigger the input:

```css
label:hover {
  background: oklch(0 0 0 / 10%);
}
```

## 7. Add a visible `:focus` state

```diff
- *:focus {
-   outline: none;
- }
+ button:focus-visible, a:focus-visible, input:focus-visible {
+   outline: 5px solid oklch(60% 0.15 252);
+ }
```

> Read more about the OKLCH colors we’re using here.
>
> [OKLCH in CSS: why we moved from RGB and HSL](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl)

We often forget or neglect keyboard UX in our applications. But when it comes to forms, in general, every user will make use of the keyboard. So, we need to think about how our UIs are accessible from the keyboard.

The first step is to add the contrast `:focus` state to highlight the current field. Users will use their peripheral vision to determine where the focus has been moved. Sara Soueidan wrote a [great guide](https://www.sarasoueidan.com/blog/focus-indicators/) that explains how to make `:focus` indicators clearly visible.

After creating a `:focus` state for input fields and buttons, add this to your `<a>` tags, too. This is the first small step for improving the keyboard accessibility of your website.

> Never disable the `:focus` state in your app.

Another tip: use [`:focus-visible`](https://css-tricks.com/almanac/selectors/f/focus-visible/) if you have SPA and want to remove a `:focus` state after clicking on a menu item.

## 8. Mark invalid fields for screen-readers

```diff
  <input type="email" autocomplete="username"
-         class="invalid">
+         required aria-invalid="true" aria-errormessage="email-error">
  <div id="email-error">Enter a valid email address</div>
```

`aria-invalid` and `aria-errormessage` display validation errors for screen-reader users.

Another note: it’s also nice to warn screen reader users about required fields by using the `required` attribute. If you don’t like the browser’s built-in validation that comes with `required`, be sure to use the `aria-required` attribute when implementing your own.

## 9. Prevent validation in the middle of user input

```diff
- input.addEventListener('keyup', () => {
-   if (validate(input)) {
-     markValid(input)
-   } else {
-     markInvalid(input)
-   }
- })
+ input.addEventListener('input', () => {
+   if (validate(input)) {
+     markValid(input)
+   }
+ })
+ input.addEventListener('change', () => {
+   if (validate(input)) {
+     markValid(input)
+   } else {
+     markInvalid(input)
+   }
+ })
```

We don’t want to distract or confuse users with error animations while they’re inputting data into a form, so don’t display a `Not valid email` error before a user hasn’t finished their input.

As a solution, use `change` instead of `keyup` for validation once the user has finished their input (by moving to another control or by submitting the form). Of course, we can use still `input`/`keyup`, but only to hide errors during input.

Here is [a good guide on inline form validation](https://www.smashingmagazine.com/2022/09/inline-validation-web-forms-ux/). - Reward Early, Punish Late

## 10. Prevent forms from being sent twice

```js
form.addEventListener("submit", () => {
  submit.disabled = true

  // Fix for Firefox. It persists the dynamic disabled state without this hack.
  submit.autocomplete = "off"

  // We are using setTimeout for page-reload submit.
  // For AJAX, use await and try-finally to enable submit the button again.
  setTimeout(() => {
    button.disabled = false
  }, 2000)
})
```

User can often accidentily double-click instead of a single-click. So, to prevent showing some server error, it’s better to disable the button upon form submission.

## 11. With AJAX, think about network latency and server/network errors

```diff
  form.addEventListener('submit', async () => {
-   await fetch(…)
+   try {
+     showLoader()
+     await fetch(…)
+   } catch (e) {
+     showError(e)
+   } finally {
+     hideLoader()
+   }
  })
```

For every AJAX request, there are two things we should always think about:

1. Show a **loading state** to the user. During local development you have 0ms latency, but live users will have up to a few seconds before a server response, so users should see some kind of reaction after clicking on a submit button.
2. Process **network and server errors**. You won’t see them in local development, but on production every user might experience a `WiFi is down` or `Error 500` error from the server; be ready for them, and show some appropriate text to users.

Note: for auth forms, it’s better to submit the form by page reload, this is better as it will save the user’s token to `httpOnly`\-cookie and update all stores in web app.

## Checklist

Let’s quickly wrap things up. Use this checklist on your next pull request review that deals with any form:

1. Set `autocomplete` to input fields
2. Select the correct `type` value for input fields
3. All clickable elements should use `<button>` or `<a>`, not `<div>` or `<span>`
4. Wrap input fields and the submit `<button>` inside `<form>` tags
5. Connect `<label>` and `<input>` tags, avoid `placeholder`
6. Wrap checkboxes inside `<label>` tags
7. Set visible `:focus` state to UI
8. Mark invalid fields for screen-readers
9. Prevent validation in the middle of input
10. Prevent forms from being sent twice
11. Think about network latency and server/network errors

---

## [Don’t Use The Placeholder Attribute](https://www.smashingmagazine.com/2018/06/placeholder-attribute/)

- Can’t be automatically translated;
- Is oftentimes used in place of a label, locking out assistive technology;
- Can hide important information when content is entered;
- Can be too light-colored to be legible;
- Has limited styling options;
- May look like pre-filled information and be skipped over.
