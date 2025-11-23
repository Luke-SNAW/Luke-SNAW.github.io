---
id: 7plyjsn42io97r7tzs26old
title: Toasts pose significant accessibility concerns and are not recommended for use
desc: ""
updated: 1763688800385
created: 1763688414042
---

> GitHub no longer uses toasts because of their accessibility and usability issues.
>
> - https://primer.style/accessibility/toasts/

- Usability problems with toasts include obscuring content, being missed on large displays, and causing distractions.
- Auto-dismissing toasts risk being unread, especially for users who multitask or are easily distracted.
- Users who rely on screen magnification may not see toast notifications.
- The ephemeral nature of toasts can lead to information loss for users with limited working memory.
- Overuse of toasts can lead to 'banner blindness,' where users are taught to ignore and avoid their content, as it is often low-quality or unrelated to their immediate task at hand.
- Instead of toasts, GitHub recommends using more accessible UI patterns like banners and dialogs for user feedback, depending on the use case.
  - [Flowchart of choosing a message type](https://github.com/user-attachments/assets/b8635f19-629c-42d6-9102-0014257288e5)

---

## [Overview](https://primer.style/accessibility/toasts/#overview)

Toasts are small, rectangular notifications that pop up on the screen, triggered either by a user or system behavior. They commonly show up on the bottom left or right-hand side of the viewport and disappear after a preset amount of time.

While it can be tempting to use toast UI as a solution for your task, know that there are many accessibility and usability issues inherent with this pattern. Because of this, **GitHub recommends using other more established, effective, and accessible ways of communicating with users**.

## [What to use instead of toasts](https://primer.style/accessibility/toasts/#what-to-use-instead-of-toasts)

Primer offers a variety of solutions for informing users about updates. Consider:

- What kind of outcome you want to achieve, and
- How the UI will best enable a user to do that.

Are you attempting to highlight a successful or unsuccessful form submission? Give feedback that an action was successfully undertaken? Alert someone that a long-running task has finished?

Thinking through your use case can help select a UI treatment that not only best serves our users, but also reinforces the internal consistency of experience within the overall GitHub platform.

### [Successfully-completed simple actions](https://primer.style/accessibility/toasts/#successfully-completed-simple-actions)

User and system initiated actions that are direct and straightforward should be successfully completed as a matter of course. An example of this is creating an Issue, and then seeing the Issue show up on the list of Repo Issues.

There does not need to be a secondary form of reinforcement to communicate success, as it should be self-evident—including a toast to communicate this success may ironically lessen a sense of trust.

### [Successfully-completed complex actions](https://primer.style/accessibility/toasts/#successfully-completed-complex-actions)

User and system-initiated actions that require more complicated interaction may need additional feedback mechanisms to help inform the user that their request was successfully enacted. An example of this is the bulk creation of Issues.

Complex interactions may benefit from a secondary form of feedback to communicate success. The manner in which this secondary feedback is expressed depends on the design, but two common approaches are:

1.  Using [banners](https://primer.style/product/ui-patterns/notification-messaging/) to provide a summary of what was performed.
2.  Progressively showing content as it is formed as part of a multi-step or progressive disclosure process.

Note that both approaches persist feedback information and do not auto-dismiss it.

### [Unsuccessful simple and complex actions](https://primer.style/accessibility/toasts/#unsuccessful-simple-and-complex-actions)

[Banners](https://primer.style/product/ui-patterns/notification-messaging/) and [dialogs](https://primer.style/product/components/dialog/) can provide feedback about user and system error as a result of an undertaken action. Banners are useful when the error information needs to be passively available, while dialogs are useful for deliberately interrupting the user to get their attention.

### [Successfully-completed forms](https://primer.style/accessibility/toasts/#successfully-completed-forms)

Simple forms may not need any other confirmation state other than creating and displaying what the user requested.

More complicated forms can utilize an interstitial confirmation page or [banner](https://primer.style/product/ui-patterns/notification-messaging/) that informs the user about what is being done with the data they submitted.

### [Other form validation](https://primer.style/accessibility/toasts/#other-form-validation)

Primer already has a robust set of components and guidance for [handling input validation](https://primer.style/product/ui-patterns/forms/#validation-message). Using these offerings helps GitHub to feel consistent across the entire surface area of the site.

### [Long-running tasks](https://primer.style/accessibility/toasts/#long-running-tasks)

Actions that take a long time to complete should [utilize banners](https://primer.style/product/ui-patterns/notification-messaging/) to inform the user of task completion or failure. Also consider ways to notify the user in other communication channels such as email, [notifications](https://github.com/notifications), or a push notification in the GitHub app.

### [Application state](https://primer.style/accessibility/toasts/#application-state)

There is the potential for a client’s session to become desynchronized, especially if a browser tab has been left open for a long time on a part of GitHub where a lot of dynamic updates are present. [Dialogs](https://primer.style/product/components/dialog/) and [banners](https://primer.style/product/ui-patterns/notification-messaging/) can be used to inform the user that a refresh is needed to resynchronize the client and server.

## [Accessibility considerations](https://primer.style/accessibility/toasts/#accessibility-considerations)

Toast UI risks violating the following [Web Content Accessibility Guideline](https://www.w3.org/TR/WCAG22/) (WCAG) Success Criteria (SC). Each of these SCs has one of three levels for support, and represent friction or a hard barrier for our users. GitHub honors the first two levels: A and AA.

### [Primary considerations](https://primer.style/accessibility/toasts/#primary-considerations)

These are aspects of toast UI that potentially represent large barriers for our users:

#### [2.2.1: Timing Adjustable](https://primer.style/accessibility/toasts/#221-timing-adjustable)

- [Understanding SC 2.2.1: Timing Adjustable](https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable.html)
- Level A

A mechanism needs to be present to extend the toast UI’s presence indefinitely until manually dismissed by the user. This is a guarantee that the toast’s duration is a length that allows all users to be able to navigate to, read, and potentially take action on the toast UI content.

#### [1.3.2: Meaningful Sequence](https://primer.style/accessibility/toasts/#132-meaningful-sequence)

- [Understanding 1.3.2: Meaningful Sequence](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence.html)
- Level A

Toast message code is commonly placed at the start or the end of the DOM. Many forms of assistive technology work by reading the DOM in sequence, so there will be a disconnect between what triggers the toast UI and the toast UI itself. This impedes discovery and understanding.

#### [2.1.1: Keyboard](https://primer.style/accessibility/toasts/#211-keyboard)

- [Understanding 2.1.1: Keyboard](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html)
- Level A

Toasts UI started as a mechanism to display passive notifications, but evolved to include interactive controls.

All interactive controls placed inside a toast UI need to be operable via keyboard, as well as accessing the toast UI container itself. This includes a mechanism for dismissing the toast, as well as managing focus when it is removed from the DOM.

#### [4.1.3: Status Messages](https://primer.style/accessibility/toasts/#413-status-messages)

- [Understanding 4.1.3: Status Messages](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html)
- Level AA

Toast UIs should make their presence known to assistive technology in a way that is not disruptive to a user’s regular workflow or working context.

### [Secondary considerations](https://primer.style/accessibility/toasts/#secondary-considerations)

These are other potential success criteria that using toast UI may violate depending on its context:

#### [1.4.4: Resize text](https://primer.style/accessibility/toasts/#144-resize-text)

- [Understanding 1.4.4: Resize text](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html)
- Level AA

Increasing the text size on the browser or operating system level runs into three potential risks for toast UI.

First is making the toast so large that it obscures the rest of the page content. Second is creating horizontal overflow in an attempt to prevent obscuring the underlying page content. Third is attempting to block text resizing on a toast component to prevent both of the previous risks.

#### [1.4.10: Reflow](https://primer.style/accessibility/toasts/#1410-reflow)

- [Understanding 1.4.10: Reflow](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html)
- Level AA

If horizontal overflow is created as a result of using toast UI, it needs to be able to be scrollable via keyboard interaction.

#### [2.4.3: Focus Order](https://primer.style/accessibility/toasts/#243-focus-order)

- [Understanding 2.4.3: Focus Order](https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html)
- Level A

A toast that contains interactive elements needs those elements to be able to receive keyboard focus. Additionally, the toast’s position in the DOM may make the order of focus not make sense compared to the interactive content that comes before or after it.

#### [3.2.4: Consistent Identification](https://primer.style/accessibility/toasts/#324-consistent-identification)

- [Understanding 3.2.4: Consistent Identification](https://www.w3.org/WAI/WCAG22/Understanding/consistent-identification.html)
- Level AA

The underlying code for toast notifications should be the same, regardless of where they are used or what team owns the service.

## [Usability considerations](https://primer.style/accessibility/toasts/#usability-considerations)

In addition to accessibility issues, there are also usability issues to consider for toasts:

### [Large displays](https://primer.style/accessibility/toasts/#large-displays)

Many developers work on a larger display, in order to have more screen real estate to work with. Toasts could be placed in such a way that they go unnoticed, in that they sit outside of a user’s immediate field of view.

### [Distractions and multitasking](https://primer.style/accessibility/toasts/#distractions-and-multitasking)

Toasts that automatically dismiss themselves risk being unread if a user is distracted or is actively switching between tabs and applications.

### [Blocking UI](https://primer.style/accessibility/toasts/#blocking-ui)

Since toasts “float” above the rest of the UI, there is a chance that they can obscure underlying content.

This obscuring effect is especially worth considering given that important UI such as form submission buttons tend to also be placed at the bottom corner of the viewport. The effect also becomes more pronounced if multiple toasts stack on top of each other.

### [Screen magnification](https://primer.style/accessibility/toasts/#screen-magnification)

Some users rely on a software or hardware-based magnification solution in order to be able to use a computer. Toast notifications may not be seen by the user, in that they are displayed outside of the range of the magnification window.

### [Working memory](https://primer.style/accessibility/toasts/#working-memory)

Toasts that both display important information and automatically dismiss themselves may create a situation where a user is given important information, but then has no way to go back and review the information.

### [Banner blindness](https://primer.style/accessibility/toasts/#banner-blindness)

Toasts are an over-used interaction pattern on the web. This leads to a phenomenon where users are taught to ignore and avoid their content, as it is often low-quality or unrelated to their immediate task at hand.

### [Disconnection](https://primer.style/accessibility/toasts/#disconnection)

A toast’s placement may be far away from the UI that triggered it. This violation of the gestalt principle of proximity means there is more of a chance a user does not understand the relationship between the toast message and its related piece of content.

### [Accidental dismissal](https://primer.style/accessibility/toasts/#accidental-dismissal)

Users pressing Esc to dismiss a toast may accidentally dismiss another piece of UI, if multiple keyboard-dismissable pieces of content are present. The opposite also applies, where a user may dismiss a toast containing important information while trying to dismiss an unrelated piece of UI.

## [Further reading](https://primer.style/accessibility/toasts/#further-reading)

- [Notification messaging - Primer](https://primer.style/product/ui-patterns/notification-messaging/)
- [Engineering Explorations on an Accessible Toast Prototype - GitHub (staff only)](https://github.com/github/accessibility/blob/main/docs/coaching-recommendations/toast-flash-banner/toasts/accessible-toast-prototype.md)
- [Celebrating with The Perfect Toast - TPGi](https://www.tpgi.com/celebrating-with-the-perfect-toast/)
- [A toast to an accessible toast… - Scott O’Hara](https://www.scottohara.me/blog/2019/07/08/a-toast-to-a11y-toasts.html)
- [Defining ‘Toast’ Messages - Adrian Roselli](https://adrianroselli.com/2020/01/defining-toast-messages.html)
- [The problem with toast messages and what to do instead - Adam Silver](https://adamsilver.io/blog/the-problem-with-toast-messages-and-what-to-do-instead/)
