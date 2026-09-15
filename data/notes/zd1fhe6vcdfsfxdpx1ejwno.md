
> https://gomakethings.com/listening-for-events-on-multiple-elements-using-javascript-event-delegation/

# Why wouldn’t you just loop through each element and attach an event listener?

You can attach event listeners to individual elements by looping over each one.\
But if you have a lot of elements, it can actually be worse for performance than event delegation.\
Every event listener you create uses memory in the browser. It’s “cheaper” for the browser to track one event and fire it on every click that it is to manage multiple events.

# Capturing events that don’t bubble

Certain events, like `focus`, don’t bubble. In order to use event delegation with events that don’t bubble, you can set an optional third argument on the EventTarget.addEventListener() method, called useCapture, to true.

```javascript
// Listen for all focus events in the document
document.addEventListener(
  "focus",
  function (event) {
    // Run functions whenever an element in the document comes into focus
  },
  true
);
```
