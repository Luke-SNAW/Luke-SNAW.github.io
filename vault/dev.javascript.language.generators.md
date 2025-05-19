---
id: l5asa62zny7n2wwaxbeqor8
title: I think the ergonomics of generators is growing on me.
desc: ""
updated: 1747638317466
created: 1747637774665
---

> Generators encapsulate state management, reducing tight coupling between components and allowing for cleaner, more modular code.
> The document illustrates how generators can replace complex patterns like recursion or callbacks, simplifying code and enhancing readability.
> — https://macarthur.me/posts/generators/

## [Where I've Begun to Appreciate Them](https://macarthur.me/posts/generators/#where-ive-begun-to-appreciate-them)

There's no groundbreaking capability here. I'm hard-pressed to find a problem that can't be solved with more common approaches. But as I've started working with them more, I'm coming to appreciate generators more often. A few reasons that come to mind:

### [They can help reduce tight coupling.](https://macarthur.me/posts/generators/#they-can-help-reduce-tight-coupling)

Generators (and all other iterators) shine at encapsulating themselves, including the management of its own state. More & more, I'm noticing how this helps ease the coupling between components I had always blindly made interdependent.

Scenario: when a button is clicked, you want to sequentially show the moving average of some price over the past five years, starting long ago. You only need the average of one window at a time, and you might not even need every possible item in the set (the user might not click through all the way). This would do the job:

```js
let windowStart = 0

function calculateMovingAverage(values, windowSize) {
  const section = values.slice(windowStart, windowStart + windowSize)

  if (section.length < windowSize) return null

  return section.reduce((sum, val) => sum + val, 0) / windowSize
}

loadButton.addEventListener("click", function () {
  const avg = calculateMovingAverage(prices, 5)
  average.innerHTML = `Average: $${avg}`
  windowStart++
})
```

Every time the button is clicked, the next average is rendered to the screen. But it's lame that we need to have a persistent `windowStart` variable at such a high scope, and I don't feel great about making the event listener responsible for updating that state. I want it exclusively focused on updating the UI.

On top of that, I might want to derive moving averages somewhere else on the page too. That'd be hard with so many things intersecting with everything else. Boundaries are weak and portability is a no-go.

A generator would help remedy this:

```js
function* calculateMovingAverage(values, windowSize) {
  let windowStart = 0

  while (windowStart <= values.length - 1) {
    const section = values.slice(windowStart, windowStart + windowSize)

    yield section.reduce((sum, val) => sum + val, 0) / windowSize

    windowStart++
  }
}

const generator = calculateMovingAverage(prices, 5)

loadButton.addEventListener("click", function () {
  const { value } = generator.next()
  average.innerHTML = `Average: $${value}`
})
```

There are some nice perks:

- The `windowStart` variable is only exposed where it's needed. No further.
- Since state and logic are self-contained, you could have multiple, distinct generators being used in parallel with no issue.
- Everything’s more focused in purpose. The math + state are left to the generator, and the click handler updates the DOM. Clear boundaries.

### [They can help avoid little "annoying" things.](https://macarthur.me/posts/generators/#they-can-help-avoid-little-annoying-things)

### [They can help make exhaustive pagination more efficient.](https://macarthur.me/posts/generators/#they-can-help-make-exhaustive-pagination-more-efficient)
