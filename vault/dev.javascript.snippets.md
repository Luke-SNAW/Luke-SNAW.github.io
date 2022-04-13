---
id: vjlre6d942v52sjkc0u3a95
title: Snippets
desc: ""
updated: 1649893451075
created: 1649396518867
---

Conditionally add properties💡 in the object from [11 Useful Modern JavaScript Tips](https://medium.com/dhiwise/11-useful-modern-javascript-tips-9736962ed2cd)

```javascript
const isValid = false;
const age = 18;

const person = {
  name: "Krina",
  ...(isValid && { isActive: true }),
  ...(age >= 18 || (isValid && { card: 0 })),
};
```

# [58 JavaScript Tips and Tricks for Web Developers](https://blog.bitsrc.io/common-js-development-skills-5053f0a74ced)
