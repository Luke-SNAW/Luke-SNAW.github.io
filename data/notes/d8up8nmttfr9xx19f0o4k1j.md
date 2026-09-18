
> https://ashleemboyer.com/blog/should-i-use-a-button-or-a-link

[The answer?](#so-whats-the-answer)

## Existing resources

Before reading the rest of this article, I highly recommend reading the wealth of knowledge that's already out there. Here's a list a small list to get you started:

- [Links vs. Buttons in Modern Web Applications](https://marcysutton.com/links-vs-buttons-in-modern-web-applications) - Marcy Sutton
- [On Link Underlines](https://adrianroselli.com/2016/06/on-link-underlines.html) - Adrian Roselli
- [Why are hyperlinks blue?](https://blog.mozilla.org/en/internet-culture/deep-dives/why-are-hyperlinks-blue/) - Elise Blanchard
- [Revisiting why hyperlinks are blue](https://blog.mozilla.org/en/internet-culture/why-are-hyperlinks-blue-revisited/) - Elise Blanchard
- [Guidelines for Visualizing Links](https://www.nngroup.com/articles/guidelines-for-visualizing-links/) - Jakob Nielsen
- [Formatting Links for Usability](https://baymard.com/blog/formatting-links-for-usability) - Baymard Institute
- [Interaction Cost](https://www.nngroup.com/articles/interaction-cost-definition/) - Raluca Budiu
- [Long-Term Exposure to Flat Design: How the Trend Slowly Decreases User Efficiency](https://www.nngroup.com/articles/flat-design-long-exposure/) - Kate Moran
- [Beyond Blue Links: Making Clickable Elements Recognizable](https://www.nngroup.com/articles/clickable-elements/) - Hoa Loranger
- [Improving text readability for dyslexic users with skip-ink underlines](https://medium.com/@iamhiwelo/improving-text-readability-for-dyslexic-users-with-skip-ink-underlines-bf52a2f3426b) - Damien Senger
- [Accessible Links Re:visited](https://www.filamentgroup.com/lab/a11y-links.html) - Maggie Wachs
- [How To Use Underlined Text To Improve User Experience](https://www.smashingmagazine.com/2017/12/underlined-text-improve-ux/) - Nick Babich
- [HTML5 Accessibility Chops: Just use a (native HTML) button](https://www.tpgi.com/html5-accessibility-chops-just-use-a-button/) - Steve Faulkner

## How do buttons and links behave differently?

### About Links

The HTML Living Standard has [an entire section dedicated to links](https://html.spec.whatwg.org/multipage/links.html#links). Here's the paraphrased definition provided by that document:

> Links are a conceptual construct that represent a connection between two resources.

It goes on to say there are two types of links: [links to external resources](https://html.spec.whatwg.org/multipage/links.html#external-resource-link) and [hyperlinks](https://html.spec.whatwg.org/multipage/links.html#hyperlink). Let's look at some examples of each.

#### Hyperlinks

Hyperlinks are links to resources within the `current site`. Here are some examples:

- Links to another location on the current page, such as a table of contents having a link to a heading element
- Links to another page in the site, such as linking to a related blog post from another
- Links to downloadable files that are intended to be used later, rather than immediately

According to the HTML Living Standard, there are several values for the `rel` property on `<a>` elements that designate the element as a hyperlink: [alternate](https://html.spec.whatwg.org/multipage/links.html#rel-alternate), [author](https://html.spec.whatwg.org/multipage/links.html#link-type-author), [bookmark](https://html.spec.whatwg.org/multipage/links.html#link-type-bookmark), [help](https://html.spec.whatwg.org/multipage/links.html#link-type-help), [license](https://html.spec.whatwg.org/multipage/links.html#link-type-license), [next](https://html.spec.whatwg.org/multipage/links.html#link-type-next), [prev](https://html.spec.whatwg.org/multipage/links.html#link-type-prev), [search](https://html.spec.whatwg.org/multipage/links.html#link-type-search), and [tag](https://html.spec.whatwg.org/multipage/links.html#link-type-tag).

I don't include this long list of values because I think it's important to know each one. I include it so it's more obvious just how much functionality is handled by native `<a>` elements. You may have heard that you can apply `role="link"` to `<button>` elements when you want to turn them into links, but it's just not enough.

There is a major loss in functionality by not using a native `<a>` element when you want to render a link, and this one property we've discussed only brushes the surface. The first rule of ARIA is extremely important to note here:

> If you can use a native HTML element or attribute with the semantics and behaviour you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.

#### The `link` ARIA role

We have one more topic to cover for defining links, and that's [the `link` ARIA role](https://www.w3.org/TR/wai-aria-1.2/#link). `link` is the default role for `<a>` elements. Here's how the role is defined:

> An interactive reference to an internal or external resource that, when activated, causes the user agent to navigate to that resource.

There is also a note that reads:

> If pressing the link triggers an action but does not change browser focus or page location, authors are advised to consider using the button role instead of the link role.

With all of the information we have covered so far, I think we can move forward with the following definition for links: An element that connects two resources and does one of the following when activated: downloads the linked resource, changes the browser focus to another part of the page, or changes the browser's location to another page.

### About Buttons

Let's move on to defining buttons. We've already seen a little bit of information that tells us buttons are different from links, but let's look for some more so we're well equipped for inevitable future buttons vs. links debates. [The HTML Living Standard](https://html.spec.whatwg.org/multipage/form-elements.html#the-button-element) does not give us as much non-technical information about buttons as it does about links, so I'll rely on the MDN Web Docs and WAI-ARIA 1.2 Specification for definitions.

#### The `<button>` element

The MDN Web Docs [definition for the Button element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button) reads:

> The `<button>` HTML element is an interactive element activated by a user with a mouse, keyboard, finger, voice command, or other assistive technology. Once activated, it then performs a programmable action, such as submitting a form or opening a dialog.

_Shameless plug: [I wrote this definition](https://github.com/mdn/content/pull/13834) back in March of 2022. 🥳_

Take a look at the [long list of attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attributes) the button element accepts:

- autofocus
- autocomplete
- disabled
- form
- formaction
- formenctype
- formmethod
- formnovalidate
- formtarget
- name
- type
- value

That is _a lot_ of functionality. This list should serve as another reason why it's not a good idea to mix and match the `<a>` and `<button>` elements. Just applying `role="button"` to `<a>` elements is no where near enough to make the anchor elment match the native implementation of the button element. In fact, just changing a `role` [does not change the look or behavior](https://www.w3.org/TR/using-aria/#role-not) of an element at all if you're not using assistive technology.

#### The `button` ARIA role

The WAI-ARIA 1.2 Specification says [the `button` role is](https://www.w3.org/TR/wai-aria-1.2/#button):

> An input that allows for user-triggered actions when clicked or pressed. \[...\] Buttons are mostly used for discrete actions. Standardizing the appearance of buttons enhances the user's recognition of the widgets as buttons \[...\].

This says that buttons are typically used to perform a single action at a time. It also says that users benefit from their appearance being standardized, so they are recognizable as an interactive element.

### Comparing Links and Buttons

By now, we should have a pretty good idea how different links and buttons are. I'll still list a few more examples of differences:

- Did you know the mouse cursor for buttons and links are different? The mouse cursor for a `<a>` element on hover is `pointer`. For the `<button>` element, it's the default/auto cursor. Read Adam Silver's [Buttons shouldn't have a hand cursor](https://medium.com/simple-human/buttons-shouldnt-have-a-hand-cursor-b11e99ca374b) for more background.
- A native `<button>` is always reachable with the keyboard, even if its role is `link`. A native `<a>` is only reachable by keyboard if it has the `href` attribute defined, even if its role is `button`. This means you have extra work to do to make the keyboard interface work if you decide not to use the native elements for their intended purposes.
- User agents and assistive technology provide navigation lists containing different types of elements. One example of this is [the VoiceOver rotor on Mac](https://support.apple.com/guide/voiceover/with-the-voiceover-rotor-mchlp2719/mac). Buttons are listed under "form controls", and links are listed under "links". If an element is not coded in a way it can be recognized by assistive technology, then users won't be able to navigate a page as they normally should. This is not a failure of screen readers. Native elements are already compatible, so use them!
- User agents and assistive technology also provide commands and gestures for interacting with different types of elements. Not using native elements can interfere with this functionality and cause users to be confused and frustrated. This is not a failure of screen readers. Native elements are already compatible, so use them!
  - For example, VoiceOver has a command for "find the next visited link". This command will not recognize `<button>` elements with `role="link"`.

How many more user agent or assistive technology features are broken by poorly coded elements? I don't know. Do you want to test every single one and find out? I highly doubt it. Just use native HTML elements!

Remember the first rule of ARIA use:

> If you can use a native HTML element or attribute with the semantics and behaviour you require already built in, instead of re-purposing an element and adding an ARIA role, state or property to make it accessible, then do so.

And don't forget the second rule of ARIA use:

> Do not change native semantics, unless you really have to.

The native semantics are present for a reason.

## Why are buttons and links styled differently?

There are [four principles of accessibility](https://www.w3.org/WAI/WCAG21/Understanding/intro#understanding-the-four-principles-of-accessibility) that inform how we must build the web and content for it. You can remember them with the acronym POUR: information and interfaces must be Perceivable, Operable, Understandable, and Robust. The Web Content Accessibility Guidelines (WCAG) are organized under these 4 principles. I'm not taking a deep dive into all of them here, but if you want to start on your own the latest standard is [WCAG 2.1](https://www.w3.org/TR/WCAG21).

Anyways, what does the look of buttons and links have to do with [four principles of accessibility](https://www.w3.org/WAI/WCAG21/Understanding/intro#understanding-the-four-principles-of-accessibility)? Well...

- Before a user can **operate** an interface, they must be able to **perceive** what elements in it are interactive.
- In order for a user to make informed decisions before they operate the interface, it must be **understandable**.
- And in order for a user to operate the interface in many conditions and environments, it must be **robust**.

Here are some WCAG guidelines and success criteria relevant to this topic you may find insightful:

...

## So what's the answer?

I think most people already know the answer to this question, and many of those who scour the internet for a different answer are looking for "permission" to do something they "unconventional". But to end on a very clear note:

- **Use an anchor element** when you need to connect two resources, and one of the following needs to happen when the element is activated:
  - download the linked resource
  - change the browser focus to another part of the page
  - change the browser's location to another page
- **Use a button element** when you need enable a user to perform a programmable action, such as submitting a form or opening a dialog.
