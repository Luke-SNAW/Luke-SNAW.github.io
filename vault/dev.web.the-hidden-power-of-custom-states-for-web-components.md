---
id: b4i1t8kw72f26w7yyjky01i
title: The Hidden Power of Custom States for Web Components
desc: ""
updated: 1669533485989
created: 1669533061204
published: false
---

> https://itnext.io/the-hidden-power-of-custom-states-for-web-components-dcae5b048e20

## Adding and removing custom states

As mentioned, all custom states are stored in a `CustomStateSet` object that is stored in the `states` property of the `ElementInternals` interface.

It has the methods `add` and `delete` to add and remove states and the `has` method to check if the element has a certain state.

Other notable methods are `clear` to clear all states and `forEach` to iterate over all states of an element:

```js
// attach the internals
this.internals = this.attachInternals()

// add states
this.internals.states.add("--foo")
this.internals.states.add("--bar")

// iterate over states
this.internals.states.forEach((state) => {
  console.log(state) // foo bar
})

// remove states
this.internals.states.delete("--bar")

// check for existence of states
this.internals.states.has("--foo") // true
this.internals.states.has("--bar") // false
```

When you try to add a state that doesn’t start with `--` an error will be thrown:

```js
this.internals = this.attachInternals()
this.internals.states.add("foo") // error, does not start with '--'
```

To make the previous example work with custom states, the getter and setter for the \`playing\` property are changed to work with the states:

```js
get playing() {
  return this.internals.states.has('--playing');
}

set playing(isPlaying) {
  if(isPlaying) {
    this.internals.states.add('--playing');
  }
  else {
    this.internals.states.delete('--playing');
  }
}
```

and the `:host()` pseudo-class now takes the `--playing` selector instead of `[playing]`:

```css
:host(:--playing) #play {
  display: none;
}

:host(:--playing) #pause {
  display: block;
}
```

While this makes sure no internal properties are exposed as attributes, it’s still possible for consumers to access `states` through the `internals` property and add or remove states by calling the `add` and `delete` methods:

```js
const player = document.querySelector("video-player")
player.internals.states.add("--playing")
```

Even worse, consumers can just call the setter of `playing` to change the internal state.

You can fix this by making both the getter and setter and the `internals` property private by prefixing them with `#`:

```js
// internals is now private
this.#internals = this.attachInternals();

get #playing() {
  return this.#internals.states.has('--playing');
}

set #playing(isPlaying) {
  if(isPlaying) {
    this.#internals.states.add('--playing');
  }
  else {
    this.#internals.states.delete('--playing');
  }
}
```

Here’s the full code:

```html
<video-player></video-player>
```

```js
class VideoPlayer extends HTMLElement {
  #internals // class field needed for private property

  constructor() {
    super()

    const shadowRoot = this.attachShadow({ mode: "open" })

    this.#internals = this.attachInternals()

    shadowRoot.innerHTML = `
      <style>
        :host {
          width: 300px;
          height: 300px;
          border: 2px solid red;
          display: flex;
          justify-content: center;
          align-items: center;
          background-color: transparent;
        }

        #pause {
          display: none;
        }

        :host(:--playing) #play {
          display: none;
        }

        :host(:--playing) #pause {
          display: block;
        }
      </style>

      <button id="play" type="button">Play</button>
      <button id="pause" type="button">Pause</button
    `
  }

  connectedCallback() {
    const playButton = this.shadowRoot.querySelector("#play")
    const pauseButton = this.shadowRoot.querySelector("#pause")

    playButton.addEventListener("click", () => {
      this.#playing = true
    })

    pauseButton.addEventListener("click", () => {
      this.#playing = false
    })
  }

  get #playing() {
    return this.#internals.states.has("--playing")
  }

  set #playing(isPlaying) {
    if (isPlaying) {
      this.#internals.states.add("--playing")
    } else {
      this.#internals.states.delete("--playing")
    }
  }
}
customElements.define("video-player", VideoPlayer)
```

These examples show how a Custom Element can be styled based on its custom states from _inside_ the component using the `:host` pseudo-class.

A Custom Element can also be styled from the _outside_ based on custom states.

This styling has the same form as styling components based on built-in states like `:checked` and `:hover`:

```css
video-player:--playing {
  border: 1px solid red;
}
```
