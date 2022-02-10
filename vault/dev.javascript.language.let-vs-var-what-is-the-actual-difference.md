---
id: L0mHMl0RZTJVa519JJKjP
title: "'let' vs 'var': What is the Actual Difference?"
desc: ""
updated: 1644478837185
created: 1644478658705
---

https://javascript.plainenglish.io/let-vs-var-what-is-the-actual-difference-5acdb1f1c83

# Scope

Both var and let are scoped differently. var is scoped for the immediate enclosing function while let is scoped for the immediate enclosing block.

## Example:

```javascript
function run() {
  var first = "First";
  let second = "Second";
  console.log(first, second); // First Second
  {
    var third = "Third";
    let fourth = "Fourth";
    console.log(third, fourth); // Third Fourth
  }
  console.log(third); // Third
  console.log(fourth); // ReferenceError
}

run();
```

# Creating global properties

The global var variables are added to the global object as properties. The global object is window on the web browser and global on Node.js:

```javscript
var counter = 0;
console.log(window.counter); //  0
```

However, the let variables are not added to the global object:

```javscript
let counter = 0;
console.log(window.counter); // undefined
```

# The Temporal dead zone

The let variables have temporal dead zones while the var variables don’t. To understand the temporal dead zone, let’s examine the life cycles of both var and let variables, which have two steps: creation and execution.

## The var variables

- In the creation phase, the JavaScript engine assigns storage spaces to var variables and immediately initializes them to undefined.
- In the execution phase, the JavaScript engine assigns the var variables the values specified by the assignments if there are ones. Otherwise, the var variables remain undefined.

## The let variables

- In the creation phase, the JavaScript engine assigns storage spaces to the let variables but does not initialize the variables. Referencing uninitialized variables will cause a ReferenceError.
- The let variables have the same execution phase as the var variables.
