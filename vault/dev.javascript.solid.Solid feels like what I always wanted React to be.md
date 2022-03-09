---
id: 2fu187ymip33tphz3ik1m1u
title: Solid.js feels like what I always wanted React to be
desc: ""
updated: 1646824573438
created: 1646824443252
---

https://typeofnan.dev/solid-js-feels-like-what-i-always-wanted-react-to-be/

# Hooks are pretty neat, but error-prone.

# Faux reactivity

I’ve thought a lot about hooks and why they don’t feel quite right.

The problem with React hooks is that _React isn’t truly reactive_. If a linter knows when an effect (or callback, or memo) hook is missing a dependency, then why can’t the framework automatically detect dependencies and react to those changes?

# But what about hooks of Solid.js?

... And we didn’t even have to tell Solid that the effect was dependent on the `count` variable.

# More interesting Solid concepts

## Reactivity, not lifecycle hooks

If you’ve been in React-land for a while, the following code change might be really eyebrow-raising:

```jsx
const [count, setCount] = createSignal(0);

setInterval(() => {
  setCount(count() + 1);
}, 1000);

createEffect(() => {
  console.log(`The count is ${count()}`);
});

function Counter() {
  return <div>The count is: {count()}</div>;
}
```

And the code still works. Our `count` signal doesn’t need to live in a component function, nor do the effects that rely on it. Everything is just a part of the reactive system and “lifecycle hooks” really don’t play much of a role.

## Fine-grained DOM updates

So far I’ve been focusing a lot on developer experience (e.g., more easily writing non-buggy code), but Solid is also getting a lot of praise for its performance. One key to its strong performance is that it interacts directly with the DOM (no virtual DOM) and it performs “fine-grained” DOM updates.
