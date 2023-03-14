---
id: c3h278rnmp6ak53huyvatbu
title: What is the difference between ref, toRef and toRefs
desc: ""
updated: 1678410393520
created: 1678410349706
---

> https://stackoverflow.com/a/66585822/5163033

## Vue 3 `ref`

A [ref](https://v3.vuejs.org/api/refs-api.html#ref) is a mechanism for reactivity in Vue 3. The idea is to wrap a non-object inside a `reactive` object:

> Takes an inner value and returns a reactive and mutable ref object. The ref object has a single property `.value` that points to the inner value.

<sub><strong>Hmm.. Why?</strong></sub>

Vue 3 relies on JavaScript [proxies](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) to detect changes to your reactive data and implement the reactivity. Proxies are essentially event listeners for objects: any reading or writing on a proxied object triggers the proxy, which can then do something with the values. This is convenient for reactivity since the variable changing will provide a trigger from which Vue can update any dependencies.

But proxies require objects to work. So Vue provides the `ref` method to convert your non-object variables into objects and then to grant reactive capabilities through a proxy. (Objects are [reference](https://developer.mozilla.org/en-US/docs/Glossary/Object_reference) variables, hence the name `ref`.)

<sup>(And Vue automatically unwraps your <code>refs</code> in the template, which is an added benefit of <code>ref</code> that you wouldn't get if you wrapped your value variables in an object manually.)</sup>

## `reactive`

If your original variable is already an object (or array), a `ref` wrapping is not needed because it is already a _reference_ type. It only needs Vue's [reactive](https://v3.vuejs.org/api/basic-reactivity.html#reactive) functionality (which a `ref` also has):

```javascript
const state = reactive({
  foo: 1,
  bar: 2,
})
```

But now consider copying a property from the object above to a new variable, for example `foo` which contains the number `1`. If you copied this to a new variable, the copy would of course be a regular, non-reactive variable having no connection to the reactive object it was copied from. If `foo` changed later, the copy would not, meaning the copy is not reactive. This is where `toRef` is useful.

## `toRef`

[`toRef`](https://v3.vuejs.org/api/refs-api.html#toref) converts a single `reactive` object property to a `ref` that **maintains its connection with the parent object**:

> ```javascript
> const state = reactive({
>   foo: 1,
>   bar: 2,
> })
>
> const fooRef = toRef(state, "foo")
> /*
> fooRef: Ref<number>,
> */
> ```

Now if `state.foo` changes, `fooRef.value` will change as well. So `toRef` has enabled copying a value property in such a way that the copy also has a reactive connection to the original parent object.

## `toRefs`

[`toRefs`](https://v3.vuejs.org/api/refs-api.html#torefs) converts _all_ of the properties, to a plain object with properties that are refs:

> ```javascript
> const state = reactive({
>   foo: 1,
>   bar: 2,
> })
>
> const stateAsRefs = toRefs(state)
> /*
> {
>   foo: Ref<number>,
>   bar: Ref<number>
> }
> */
> ```

**When would I ever use `toRef` or `toRefs`?**

The most likely time would be when importing a reactive object, say from a composable, and [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) it. The act of destructuring will pull the current property value from the object into a new local variable that will not be reactive without `toRef`. You may notice this when importing and destructuring a [Pinia](https://pinia.vuejs.org/) store into your component, for example.
