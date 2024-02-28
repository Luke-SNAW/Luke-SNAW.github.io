---
id: e0t0c0dwkch04d08acj67py
title: Dialogs, modality and popovers seem similar. How are they different?
desc: ""
updated: 1709107651087
created: 1668411407835
---

> https://hidde.blog/dialog-modal-popover-differences/

> _Note: at the time of writing, `popover` is still a proposal and only available as an experiment, behind a flag, and in Chromium. As an Open UI participant, I feel this would be a great feature to have on the web. I hope it becomes part of the HTML spec and a widely supported reality, but this is not sure yet._
>
> _The feature will probably be [renamed](https://github.com/openui/open-ui/issues/627) (from `popup` to `popover`; this post uses `popover` in most places for now)_.

## [The characteristics](https://hidde.blog/dialog-modal-popover-differences/#heading-3)

### Modality / inertness

Some design systems have a component named “modal”, but modality is more of a characteristic than a component itself.

So what does it mean for an element to be _modal_? Basically, when a modal component is open, it is the only thing that is _not_ inert. Only the modal content can be interacted rest with, the _rest of the page_ or application is made inert. Inert content is content that users cannot interact with. It is only really there visually, but you cannot Tab to it, click it, scroll it or access the content via assistive technologies.

Elements that are not modal are called _non-modal_ or _modeless_.

[Not everyone likes modality](https://modalzmodalzmodalz.com/)—as a UI concept, they are very disruptive. Use the pattern sparsely, only when disrupting is very much necessary. If you want to ask the user “Are you sure you want to delete all that?”, go ahead and make it disruptive. If you want to promote your newsletter sign-up or advertising, the disruption is unlikely to be appreciated.

In terms of implementation, you will need to make everything except your modal element inert. The `<dialog>` element (used with `showModal()`) does this for and would be the best to use.

### Light vs explicit dismiss

Another aspect to consider is how users dismiss a component and whether that is affected by other elements: this can be via explicit dismiss or light dismiss.

With ‘explicit dismiss’, a component allows a user to dismiss it, for instance via a close button and the Escape key (when in doubt, best add both).

With ‘light dismiss’, a component disappears automatically on certain conditions, like when users scroll, interact with something else or click outside of the component. Light dismiss doesn't happen when the user `Tab`s out of the element by default (but developers can add it if needed, see [the discussion in openui/open-ui#415](https://github.com/openui/open-ui/issues/415#issuecomment-1261460981) for more details).

Light dismiss is something we can already build in JavaScript today, a lot of websites have components that light dismiss. But with the `popover` attribute, the browser would do it for you (if you use `popover="auto"`).

## [The main patterns](https://hidde.blog/dialog-modal-popover-differences/#heading-4)

### Dialogs

#### What is it

A dialog is a component in a web page or app that usually contains an action or some task to perform (see: [`<dialog>` in HTML specification](https://html.spec.whatwg.org/dev/interactive-elements.html#the-dialog-element)). It is usually not part of the natural flow of other content, for that reason it can (and usually does) cover other content. MDN describes it as a “subwindow”, ARIA Authoring Practices defines it as a “window overlaid on either the primary window or another dialog window”.

A dialog is often displayed when users need to be made aware of something or when they need to choose. Do you want to continue, yes or no? If you want to open a new file, what shall we do with your current file, save or delete? How do you want to crop this image, where is the hot spot?

![dialog that says Would you like to use a dialog? with cancel and ok button](/_images/confirm.png) _Browser dialogs / `confirm()`_

Canonically, dialogs are a lot like `window.confirm()`, `window.alert()` and `window.prompt()`, which the HTML specification lists under ‘[simple dialogs](https://html.spec.whatwg.org/dev/timers-and-user-prompts.html#simple-dialogs)’. But unlike these browser built-in dialogs, custom dialogs offer more flexibility—you get to put whichever content and styling you want inside of them.

Dialogs have a role of `dialog`, which the browser will assign automatically for you when you use the `<dialog>` element.

You can also create dialogs with ARIA: apply `role="dialog"` to an element (like `<div>`). If it is a modal dialog, add `aria-modal="true"` when it shows, and remove it when it is dismissed. You will need to do all the modality work yourself (focus trap, making rest of content inert, etc). Note: `aria-modal` is not supported in IE11 (which [may still be in use among your assistive technology users](https://webaim.org/projects/screenreadersurvey9/#browsers)), there are [issues with `aria-modal` in VoiceOver](https://bugs.webkit.org/show_bug.cgi?id=174667) and it seems [unsupported in Narrator](https://a11ysupport.io/tech/aria/aria-modal_attribute).

You can put a form with `method="dialog"` in a dialog. This form will close its dialog when submitted.

#### Examples

![Insert link dialog with behind it a dimmed background. It has fields for Link Text and URL, buttons to close the dialog or add the link](/_images/add-link.png) _Modal dialog: add a link; nothing behind it can be interacted with while this modal dialog is open._

![travel booking site with in the left bottom corner a chat widget with a chatbot that says Hi Hidde How are you today.](/_images/how-are-you-today.png) _Non modal dialog: while this chat widget is open, I can still access the forms and content underneath._

#### Characteristics

Dialogs can be modal (`<dialog>` when shown with `dialog.showModal()`) or non modal (`<dialog>` when shown with `dialog.show()`). To avoid quirks, you will want to choose which of the two your dialog is, and only call one of these methods per dialog.

When `<dialog>`s are modal, the browser will treat the content outside of the dialog as inert, and prevent keyboard focus from reaching web content outside of the dialog (if you use `role="dialog"`, you have to do this yourself). If a `<dialog>` is not modal, the other content is not treated as inert. This makes modal dialogs a lot more disruptive, so use them only when you have to. You usually don't want to interrupt or disrupt a user's flow.

Dialogs are in the top layer only if they are modal (and only if the `<dialog>` element is used; other elements with `role="dialog"` will not go to the top layer).

Dialogs must have an accessible name (see [WAI-ARIA 1.2, `dialog` role](https://www.w3.org/TR/wai-aria-1.2/#dialog)). Associate your dialog with the visible heading or message (if brief) using [`aria-labelledby`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-labelledby) on the `<dialog>` / `<div role="dialog">`. You could also use `aria-label`, but associating with visible text is ideal, because it creates parity between what folks see and what assistive tech call stuff.

[WAI-ARIA](https://www.w3.org/TR/wai-aria-1.2/#dialog) specifies that when you're using `role="dialog"`, you should include at least one focusable element and move focus to one of the focusable elements when it opens.

Browsers will close modal dialogs when users press `Escape`. Non-modal dialogs don't get this default behaviour, developers can add it where it makes sense.

### Alert dialogs

WAI-ARIA defines a specific type of dialog, which is called “alert dialog”. It is meant for dialogs that contain a brief, important message. Their function is to alert the user—the browser will do that by firing a system alert event to accessibility APIs. They are the ARIA-equivalent of the browser `alert()` dialogs we discussed above.

#### Examples

- After you didn't interact with your online banking environment for 10 minutes, an alert dialog shows and says you will log out in 5 minutes, unless you press “Continue my session”
- You're editing some important content and accidentally press `Command + W`, the shortcut to close the current tab. An alert dialog appears to ask if you really want to “Leave” now or perhaps “Save your changes” first.

#### Characteristics

Alert dialogs are **always modal** and have their **focus trapped**. They also require an **accessible name**. Like with dialogs, if there is a visible title, associate the title's `id` with the alert dialog's `aria-labelledby` attribute. If not, `aria-label` can also be added to an alert dialog.

### Popovers

#### What is it

Popover is a set of behaviors that can be added to any element through the `popover` attribute (like `tabindex` or `contenteditable`). As mentioned, at the time of writing, it is a proposal and not in the HTML specification yet, but there is the [Pop Up API Explainer](https://open-ui.org/components/popup.research.explainer), a [polyfill](https://github.com/oddbird/popup-polyfill) and a [PR to the HTML spec](https://github.com/whatwg/html/pull/8221) ([why is it an attribute and not an element?](https://open-ui.org/components/popup.research.explainer#alternatives-considered)). (Some of this still mentions a `popup` attribute, it has been renamed to `popover` in October 2022)

The `popover` attribute is meant for UI components that are:

- on top of other page content
- not always visible (eg just when they are relevant), also described as “short lived” or “ephemeral”
- usually displayed one at the time

As opposed to `<dialog>`s, a `popover` doesn't come with a built-in role (this is partly why it is an attribute and not an element). It can take on any role that makes sense, or none at all. Sometimes popovers could be (modeless) dialogs, in that case you could use `<dialog popover>`.

The popover attribute is planned to allow for two values, each of which give a slightly different set of characteristics:

- `popover=auto`: light dismisses; when it opens, it force-closes other popovers and hints (except its anchestors); it or its anchestor would usually receive focus
- `popover=manual`: explicit dismiss (via timer, close button or some other script); when it opens, it does not force close anything

(More types may follow)

Full screen content also forces popovers of the “auto” type to close.

#### Examples

An example of a popover is the listbox that shows when a select is opened (conceptually for `<select>` and literally for `<selectmenu>` as it is currently implemented in Chromium).

These are some common examples of components with popover behaviours:

- Datepickers / calendar widgets
- Tooltips and toggletips
- Teaching UI (e.g. to point out parts of your interface when it is first shown)
- Action menus (see example below), using `role="menu"`

There are also popovers that users need to dismiss or that automatically dismiss (like toasts).

So yes, there are lots of different UI patterns that can have “popover” behaviour as a requirement. This is why popover is proposed not as one HTML element, but as an attribute that is meant to be used with an HTML and/or `role` that is most suitable for that pattern. For an action menu, that's a `<div role="menu" popover>`. A tooltip could be `<div role="tooltip" popover>` (depending on context and what it is). In any case: each of these patterns has its own UX expectations.

![CMS image component with preview of an image and its alternative text. Next to the image is a kebab button from which a menu called Replace is expanded, with actions Upload, Browse, Download, Copy original files, Copy URL, Clear field, the last one is red](/_images/change-image.png) _This is an action menu to change an image is a popover. It disappears when you click outside of it._

![image with bottles of fritz kola on Twitter, in the left bottom corner is an ALT badge from which a popover is expanded that says Image Description, describes the bottles and then has a large Dismiss button](/_images/fritz.png)_  
Twitter's alternative text feature is another example of a popover ([implementation has accessibility issues](https://adrianroselli.com/2022/04/keyboard-challenges-for-twitters-new-alt-badge.html))_

#### Characteristics

Popovers are **not modal**. This is another major difference between popovers and dialogs. For this reason, it will be rare (but not impossible) for them to have a backdrop or focus trap.

Popovers can have ‘light dismiss’ behaviour, meaning they close by themselves, except when they are of the “manual” type. Manual popovers could be things like a “toast” notification that is dismissed via a timer or manual button.

Popovers can have a backdrop, which obscures content outside of it. This does not make the popover modal. There are valid use cases for popovers with backdrops, but if you feel like adding a backdrop, it is worth considering a modal dialog instead.

Popovers can have focus trapped in them, for instance in complex widgets where you want to avoid that people accidentally tab out of the widget. A focus trap does not make a popover modal, as users can still access everything else on the page, it is just something that can improve usability in certain cases.

![CMS interface with dimmed out publish button and in the right bottom corner a green box that says 'the document was published', the box has a button with a close icon on the right](/_images/toast.png) _A “toast” notification that dismisses automatically after a couple of seconds and also has a close button in case you want it to go away now (most toasts just disappear, that's also fine; in either case their contents [should be conveyed to assistive tech](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.1#status-messages))._

Popovers also can be opened, closed and toggled without JavaScript: with a `<button>` in HTML and `popovershowtarget`, `popoverhidetarget` and `popovertoggletarget` attributes whose values correspond with the popover's ID, the browser can take care of showing, hiding and toggling.

An example:

```html
<button type="button" popovertoggletarget="datepicker">Pick date</button>
<dialog popover id="datepicker"></dialog>
```

(the div is turned into a popover with the `popover` attribute, the button toggles the popover with `popovertoggletarget`)

To open the popover when the page loads, set `defaultopen` on the popover. This is useful for teaching UI.

To move focus to a popover when it opens, set the `autofocus` attribute on the popover itself, or an element within it. Normally, this attribute sets focus on page load. But if it is used on or within popovers, it only sets focus when the popover is shown (this can be on page load if `defaultopen` is used).

To position a popover, a very exciting proposal called [CSS Anchor Positioning](https://tabatkins.github.io/specs/css-anchor-position/) is in the works. As far as I understand it today, it would allow us popovers that automagically position in the most suitable place, avoiding collisions with the edge of the window. A bit like the [Popper](https://popper.js.org/) library does today, but built into the browser.

If focus management, positioning, JavaScript-less toggling and light dismiss weren't enough, popovers are also easy to animate using CSS: you can set up a transition between `[popover]` and `[popover]:open` (of course, you'll want to adhere to your users' motion settings using[prefers-reduced-motion](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)).

### Overlays

Overlays are more of a characteristic than a component on their own. Often, when developers talk about overlays, they mean dialogs that are modal. In a literal sense, overlays are things that lay on top of other things. Popovers and dialogs can both overlay other things.

### Disclosure widgets

#### What are they

Elements that show and hide things are often called ‘disclosure widget’, as Adrian Roselli describes in [his post about various kinds popover-like controls](https://adrianroselli.com/2021/07/stop-using-pop-up.html). Almost everything in this post is a subset of disclosure widgets… as in, they are pretty much all things that can be shown and hidden. Adrian describes disclosure widgets in more detail in his post [Disclosure widgets](https://adrianroselli.com/2020/05/disclosure-widgets.html).

Disclosure widgets exist in HTML as `<details>`/`<summary>`, but can also be built with `<div>` and the appropriate ARIA attributes. This isn't entirely the same. In [Details/summary, again](https://www.scottohara.me//blog/2022/09/12/details-summary.html), Scott O'Hara suggests that this is more consistent:

> If your goal is to create an absolutely consistent disclosure widget behavior across browsers, i.e., ensuring that all `<summary>`s are exposed as expand/collapse buttons, then you’d be better off creating your own using JavaScript and the necessary ARIA attributes.

But, he adds, your ARIA disclosure widget won't have some of the features `<details>`/`<summary>` brings, like in-page search (Chromium triggers a `<details>`'s element `open` state when an in-page search query is found in its content).

There isn't a specific `role` for disclosure widgets, but there is the `aria-expanded` attribute for triggers and `aria-controls` to connect triggers with the element they trigger. When using `<details`/`summary`, `<dialog>` and (in the future) `popover`, browsers take care of setting up these kinds of accessibility properties for you.

#### Examples

- a Frequently Asked Questions section where the answers are collapsed and you can expand them from the questions
- tables in which individual rows can be expanded (See Adrian Roselli's [Table with Expando Rows](https://adrianroselli.com/2019/09/table-with-expando-rows.html))
- “Toggle tips”, like an “info” button that displays next to complex terminology to open a tooltip that explains the word
- “meganav” style navigation where the main navigation items open more navigations

![wikipedia content with on the right hand side a box called Disability, under which all sections have show buttons, except the first two, which are expanded and have hide buttons next to them](/_images/wiki-disclosure.png) _The show/hide functionality of sections within a category (displayed on the right) are a disclosure widget_

#### Characteristics

There are a lot of different things that qualify as disclosure widgets. What they have in common is that they consist of two parts: one is a _triggering_ element, the other is the _triggered_ element.

Disclosure widgets do not trap focus, have no backdrops and are not modal. They are usually dismissed or collapsed with their trigger or a close-specific button.

## [FAQs](https://hidde.blog/dialog-modal-popover-differences/#heading-5)

### Where should focus move?

When a modal dialog **opens**, keyboard focus should move to the default action. If there's a form, it is probably the first form field. If there is multiple buttons, it could be the one that is least destructive, like if there's “Cancel” and “Confirm” button, a sensible default would be “Cancel”.

When a modal dialog **closes**: if the user triggered it, move focus back to the trigger. The browser does this automatically for `<dialog>`s. For popovers, it only does in cases “where it makes sense” (see the [Popup Explainer](https://open-ui.org/components/popup.research.explainer#focus-management)). If the user did not trigger it, move it to an appropriate position earlier in the DOM.

For all other components (non-modal dialogs, popovers or disclosures), expected focus management differs case by case. The [Popup Explainer's section on focus](https://open-ui.org/components/popup.research.explainer#focus-management) describes some of such cases.

### Are all popovers dialogs?

Not all popovers are `<dialog>` elements or elements with `role="dialog"`. For instance, listboxes, menus, tooltips, grids, lists of links likely have popover behaviours, but not the `dialog` role.

### Are all dialogs popovers?

No, only _non-modal_ dialogs are conceptually popovers (you can implement them with `<dialog>`/`role="dialog"` today). When the popover feature is stable and well-supported in browsers, it makes sense to use `<dialog popover>`, and would be _the_ way to go if you want your non-modal dialog to appear in the top layer and leverage browser-provided light dismiss. In contrast, _modal_ dialogs don't share the set of characteristics popovers have.

### I'm building an X, should it be modal?

It depends. The question to ask is: is this component something that is the only thing your user may pay attention when it is open?

#### Country selector

You are building a check-out form for your online shop. In one of the fields, the user need to select a country. They eventually have to, because it is a required field. Still, while they select the country, they may scroll to something else, or decide to pop to the credit card stuff first. Maybe they need to read the label to check if you need country of birth or residence. This is best **non-modal**, because the user may want to look at other things.

#### Definition popover

You are building a toggle tip that can show definitions for complex words in your content. When the definition icon is clicked, it opens. Your user may want to scroll away or read other content or do other stuff. It is best to keep this **non-modal**.

#### Game over

You are building a game and the user has managed to build a dialog that tells the user they are “game over”. They can't continue playing. It's really over. There's no other thing they can interact with than this dialog. **Modal** it is.

#### Tracking consent

You are building a dialog that asks users if they want to agree that you track them. Your visitor is in an area where the law makes it illegal for you to do so without permission. In this case, there is no point in interacting with anything but the permission screen, so it would make sense to make it **modal**.

#### Fly-out navigation

You are building a “fly-out navigation”. It opens on the side of the viewport and is positioned on top of other content while it is open. When the user opens it, is this the only thing they want to see? This one is tricky, I feel **modal** could work, **non-modal** could work too.

## [Summing up / conclusions](https://hidde.blog/dialog-modal-popover-differences/#heading-6)

OK, so, in summary: _modality_ of a component is a state in which only that component can be used. When something is modal, everything else is _inert_: blocked from access in any way, unfocusable and usually obscured with a backdrop. Making something modal is a substantial decision, it should be used sparingly. _Dialogs_ can be modal or non-modal (also called modeless). `popover`s are being proposed by Open UI as a new way to build non-modal dialogs with a specific set of behaviours and characteristics, like top layer presence, JS-less toggleability and browser-provided light dismiss. Unlike `<dialog>`, a `popover` does not have a built-in role: as a developer, you can add the `popover` attribute to the semantically most relevant element.

Most of the UI patterns that are mentioned in this post fall under the definition of overlays: content that can lay on top of other content (all dialogs and popovers). A lot also fall under the definition of disclosures, when they are patterns where one thing opens another thing.

## [Further reading](https://hidde.blog/dialog-modal-popover-differences/#heading-7)

- [MDN - `<dialog>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog)
- [WAI-ARIA: role=dialog](https://www.w3.org/TR/wai-aria-1.2/#dialog)
- [Having an open dialog](https://www.scottohara.me/blog/2019/03/05/open-dialog.html) by Scott O'Hara on using `<dialog>`
- [Stop using “pop-up”](https://adrianroselli.com/2021/07/stop-using-pop-up.html) by Adrian Roselli, which offers clear distinction between various popup-like patterns
- [Open UI issue 581: \[popup\] Add further clarity that popup is not (presently?) for modal dialogs](https://github.com/openui/open-ui/issues/581)
- [Inert | The CSS Podcast](https://www.youtube.com/watch?v=-gBv12xu4Yo) with Una Kravets and Adam Argyle
