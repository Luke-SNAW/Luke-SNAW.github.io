---
id: jcnpotf8rb4l893w4fx3f8e
title: Target=_blank implies rel=noopener
desc: ""
updated: 1716190707337
created: 1716190591462
---

> https://www.stefanjudis.com/today-i-learned/target-blank-implies-rel-noopener/

If you want to be a good web citizen, you might be aware of the `target="_blank"` security issue.

In the old days, when you linked to a site and wanted to open a new tab with `target="_blank"`, the target site could access your site via [`window.opener`](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/noopener). This means in short:

> If window A opens window B, `B.opener` returns A.

If you haven't heard of this behavior, it's pretty wild because it implies that target pages could check if `window.opener` is accessible and if so change the location of your site with trivial JavaScript. This is also known as "reverse tab nabbing".

```javascript
if (window.opener) {
  window.opener.location = "https://you-re-hacked.com"
}
```

Ooooff... And while it's unlikely, someone could now use XSS to inject `target="_blank"` links into your site and, when someone clicks on them, change the URL of the original site (which is now in the background) to a malicious copy to fish credentials.

To prevent this, you could use `rel="noopener"`.

```html
<!-- old school way to turn off `window.opener` -->
<a href="some-site.com" target="_blank" rel="noopener"> Some site </a>
```

But guess what? Because this behavior seemed so off, browsers changed it. In 2024, whenever you use `target="_blank"` `rel="noopener"` is implicit. Yay!

```html
<a href="some-site.com" target="_blank" rel="noopener"> some site </a>

<!-- is the same as -->

<a href="some-site.com" target="_blank"> some site </a>
```

But is this new stuff? Nope.

MDN Compat Data ([source](https://raw.githubusercontent.com/mdn/browser-compat-data/main/html/elements/a.json))

| chrome | chrome_android | edge | firefox | firefox_android | safari | safari_ios | samsunginternet_android | webview_android |
| ------ | -------------- | ---- | ------- | --------------- | ------ | ---------- | ----------------------- | --------------- |
| 88     | 88             | 88   | 79      | 79              | 12.1   | 12.1       | 15.0                    | Nei             |

- [Chromium shipped it **end of 2020**](https://chromestatus.com/feature/6140064063029248).
- [Safari shipped it **end of 2018**](https://webkit.org/blog/8475/release-notes-for-safari-technology-preview-68/).
- [Firefox shipped it **mid 2020**](https://bugzilla.mozilla.org/show_bug.cgi?id=1522083).

Yet, the internet is full of `rel="noopener"` advice, so the legendary `target="_blank"` issue continues to live on.

Let's see if this post will help make it disappear.
