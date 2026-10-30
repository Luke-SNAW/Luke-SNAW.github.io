
https://css-tricks.com/send-an-http-request-on-page-exit/

# Browsers don’t guarantee to preserve open HTTP requests

When something occurs to terminate a page in the browser, there’s no guarantee that an in-process HTTP request will be successful ([see more](https://developers.google.com/web/updates/2018/07/page-lifecycle-api) about the “terminated” and other states of a page’s lifecycle).

...

When navigation occurs, the request is cancelled.

# But why are they cancelled?

The root of the issue is that, by default, **XHR** requests (via fetch or XMLHttpRequest) are asynchronous and non-blocking. As soon as the request is queued, the actual work of the request is handed off to a browser-level API behind the scenes.

As it relates to performance, this is good — you don’t want requests hogging the main thread. But it also means there’s a risk of them being deserted when a page enters into that “terminated” state, leaving no guarantee that any of that behind-the-scenes work reaches completion. [Here’s how Google summarizes](https://developers.google.com/web/updates/2018/07/page-lifecycle-api#states) that specific lifecycle state:

> A page is in the terminated state once it has started being unloaded and cleared from memory by the browser. No [new tasks](https://html.spec.whatwg.org/multipage/webappapis.html#queue-a-task) can start in this state, and in-progress tasks may be killed if they run too long.

In short, the browser is designed with the assumption that when a page is dismissed, there’s no need to continue to process any background processes queued by it.

# So, what are our options?

... to delay the user action until the request returns a response.  
That gets the job done, but there are some non-trivial drawbacks.

First, it compromises the user’s experience by delaying the desired behavior from occurring.

Second, this approach isn’t as reliable as it initially sounds, since some termination behaviors can’t be programmatically delayed.  
For example, e.preventDefault() is useless in delaying someone from closing a browser tab.

# Instructing the browser to preserve outstanding requests

## Using Fetch’s keepalive flag

If the [keepalive flag](https://fetch.spec.whatwg.org/#request-keepalive-flag) is set to true when using fetch(), the corresponding request will remain open, even if the page that initiated that request is terminated.

## Using [Navigator.sendBeacon()](https://w3c.github.io/beacon/#sec-processing-model)

## An honorable mention for [the ping attribute](https://css-tricks.com/the-ping-attribute-on-anchor-links/)

It’s technically similar to sending a beacon, but has a few notable limitations:

1. It’s strictly limited for use on links, which makes it a non-starter if you need to track data associated with other interactions, like button clicks or form submissions.
2. Browser support is good, [but not great](https://caniuse.com/ping).
3. You’re unable to send any custom data along with the request. As mentioned, the most you’ll get is a couple of ping-\* headers, along with whatever other headers are along for the ride.

# So, which one should I reach for?

There are definitely tradeoffs to using either fetch with keepalive or sendBeacon() to send your last-second requests. To help discern which is the most appropriate for different circumstances, here are some things to consider:

## You might go with `fetch()` + `keepalive` if:

- You need to easily pass custom headers with the request.
- You want to make a GET request to a service, rather than a POST.
- You’re supporting older browsers (like IE) and already have a fetch polyfill being loaded.

## But `sendBeacon()` might be a better choice if:

- You’re making simple service requests that don’t need much customization.
- You prefer the cleaner, more elegant API.
- You want to guarantee that your requests don’t compete with other high-priority requests being sent in the application.
