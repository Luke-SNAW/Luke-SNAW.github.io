---
id: mraMGoestTO9V6pkpE8XE
title: Language
desc: ""
updated: 1646699051816
created: 1644885695251
---

- [10 Powerful JavaScript Destructuring Techniques Every Developer Should Know](https://javascript.plainenglish.io/10-powerful-javascript-destructuring-techniques-every-developer-should-know-15ae06818bb6)

# [Avoid the “delete” Keyword in JavaScript](https://javascript.plainenglish.io/avoid-the-delete-keyword-in-javascript-87ff2a47f26c)

```javascript
const snowbit = {
  age: 15,
  test: "abc",
};
const { test, ...newSnowbit } = snowbit;
console.log(newSnowbit); //  {age: 15}
```

Let me explain, You should not use `delete` to remove the property from the object because this mutates the original and that can lead to unpredictable behaviours and becomes difficult to debug.
