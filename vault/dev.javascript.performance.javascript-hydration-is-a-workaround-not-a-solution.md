---
id: cyzyd34z7l76mm9k1bgajq0
title: JavaScript Hydration Is a Workaround Not a Solution
desc: ""
updated: 1655856336906
created: 1655856282339
---

> https://thenewstack.io/javascript-hydration-is-a-workaround-not-a-solution/

In web development, [Hydration](https://www.builder.io/blog/why-progressive-hydration-is-harder-than-you-think) is a technique to add interactivity to server-rendered HTML. It’s a technique in which client-side JavaScript converts a static HTML web page into a dynamic web page by attaching event handlers to the HTML elements.

However, attaching event handlers to the Document Object Model (DOM) is not the most challenging or expensive part of hydration.

In this article, I’ll explain why I believe hydration is overhead. It’s not the solution; it’s a hack that consumes memory and slows down startup, especially on mobile. For the sake of this article, let’s define overhead as work that can be avoided and still leads to the same end result.

## Digging Deeper into Hydration

The hard part of hydration is knowing what event handlers we need and where they need to be attached.

- **WHAT**: The event handler is a closure that contains the behavior of the event. It is what should happen if a user triggers this event.
- **WHERE**: The location of the DOM element where the WHAT needs to be attached (includes the event type)

The added complication is that WHAT is a closure that closes over _APP_STATE_ and _FW_STATE_:

- _APP_STATE_: the state of the application. _APP_STATE_ is what most people think of as the state. Without _APP_STATE_, your application has nothing dynamic to show the user.
- _FW_STATE_: the internal state of the framework. Without _FW_STATE_, the framework does not know which DOM nodes to update or when the framework should update them. Examples are component-tree and references to render functions.

So how do we recover WHAT and WHERE? By downloading and executing the rendered components in HTML. This is the expensive part.

In other words, hydration is a hack to recover the _APP_STATE_ and _FW_STATE_ by eagerly executing the app code in the browser and involves:

- Downloading component code.
- Executing component code.
- Recovering the WHAT (_APP_STATE_ and _FW_STATE_) and WHERE to get event handler closure.
- Attaching WHAT (the event handler closure) to WHERE (a DOM element).

Let’s call the first three steps the Recovery phase.

**Recovery** is when the framework is trying to rebuild the application. The rebuild is expensive because it requires downloading and executing the application code.

Recovery is directly proportional to the complexity of the page being hydrated and can easily take 10 seconds on a mobile device. Since Recovery is the expensive part, most applications have a suboptimal startup performance, especially on mobile.

Recovery is also overhead: It rebuilds information that the server already gathered as part of server-side rendering (SSR) or static site generation (SSG). Instead of sending the information to the client, the information was discarded. As a result, the client must perform expensive Recovery to rebuild what the server already had. If only the server had serialized the information and sent it to the client along with HTML, the Recovery could have been avoided. The serialized information would save the client from eagerly downloading and executing all of the components in the HTML.

In other words, the re-execution of code on the client that the server already executed as part of SSR/SSG is what makes hydration pure overhead.

## Resumability: A No-Overhead Alternative to Hydration

To remove overhead, the framework must not only avoid Recovery, but also step four from above: attaching the WHAT to WHERE.

To avoid this cost, you need three things:

- All of the required information serialized as part of the HTML, including WHAT, WHERE, _APP_STATE_, and _FW_STATE._
- A global event handler that relies on event bubbling to intercept all events so that we are not forced to eagerly register all events individually on specific DOM elements.
- A factory function that can lazily recover the event handler (the WHAT).

The above setup is resumable because it can resume the execution where the server left off without redoing any work that the server already did. By creating the WHAT lazily as a response to a user event, we can avoid doing all the unnecessary work that happens in hydration. All this means no overhead.

## Memory Usage

The DOM elements retain the event handlers for the lifetime of the element. Hydration eagerly creates all of the listeners, so it needs memory to be allocated on startup.

On the other hand, resumable frameworks do not create the event handlers until after the event is triggered. Therefore, they will consume less memory than hydration. Furthermore, the event handler is released after its execution, returning the memory.

In a way, releasing the memory is the opposite of hydration. It is as if the framework lazily hydrates a specific WHAT, executes it and then dehydrates it. There is not much of a difference between the first and nth execution of the handler.

## The Performance Difference

To put this idea into practice, we built [Qwik](https://qwik.builder.io/), a framework that is designed around “resumability” and achieves a speedy startup. To show you the impact of resumability, we built a [to-do app demo](https://todo-cloudflare-misko.sethealth.workers.dev/) that runs on Cloudflare edge. This page is ready for interaction in about 50 ms.

We also used the resumable strategy (and Qwik) to redo our website, [builder.io](http://www.builder.io/). Using Qwik (and our other solution, [Partytown](https://partytown.builder.io/)), we were able to [cut down 99% of the JavaScript in our site and get a PageSpeed score of 100/100](https://www.builder.io/blog/how-we-cut-99-percent-js-with-qwik-and-partytown). (You can still visit the [old page using hydration](https://www.builder.io/?render=next) to compare and experience the performance difference for yourself.)

## Conclusion

Put simply, hydration is overhead because it duplicates work. The server builds up the WHERE and WHAT (_APP_STATE_ and _FW_STATE_), but the information is discarded instead of being serialized for the client. The client then receives HTML that does not have sufficient information to rebuild the application. The lack of information forces the client to eagerly download the application and execute it to recover the WHERE and WHAT.

An alternative approach is resumability. Resumability focuses on transferring all of the information (the WHERE and WHAT) from the server to the client. Only a user interaction forces the client to download code to handle that specific interaction. The client is not duplicating any work from the server; therefore, there is no overhead.
