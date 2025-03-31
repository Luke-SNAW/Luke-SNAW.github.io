---
id: gnh7pclc140wsbtf84b5yf8
title: Javascript debug
desc: ""
updated: 1743386893206
created: 1646265630764
---

## Collections

- [How to Inspect Interactions in the Browser](https://www.builder.io/blog/inspect-interactions-in-the-browser)
- [Et Tu, Grammarly?](https://dbushell.com/2025/03/29/et-tu-grammarly/)

## [Developer Tools secrets that shouldn’t be secrets](https://christianheilmann.com/2021/11/01/developer-tools-secrets-that-shouldnt-be-secrets/)

```javascript
console.log({width})

function third(name) {
  if(!name)
    console.error(`Name isn't defined :(`)
  else
    console.assert(
      name.length <= 8,
      `"${name} is not less than eight letters"`
    )
```

- console.group()
- console.table()
- Blinging it up: $() and $$()
- [Console Utilities](https://docs.microsoft.com/microsoft-edge/devtools-guide-chromium/console/utilities)

## [Monitor Events and Function Calls via Console](https://davidwalsh.name/monitorevents)

### Monitor Events

Pass an element and a series of events to `monitorEvents` to get a console log when the event happens:

```js
// Monitor any clicks within the window
monitorEvents(window, "click")

// Monitor for keyup and keydown events on the body
monitorEvents(document.body, ["keyup", "keydown"])
```

You can pass an array of events to listen for multiple events. The logged `event` represents the same event you'd see if you manually called `addEventListener`.

### Monitor Function Calls

The `monitor` method allows you to listen for calls on a specific function:

```js
// Define a sample function
function myFn() {}
// Monitor it
monitor(myFn)

// Usage 1: Basic call
myFn()
// function myFn called

// Usage 2: Arguments
myFn(1)
// function myFn called with arguments: 1
```

I really like that you can view the arguments provided, which is great for inspecting.

I usually opt for [logpoints](https://davidwalsh.name/logpoints) instead of embedding `console` statements in code, but `monitor` and `monitorEvents` provide an alternative to both.
