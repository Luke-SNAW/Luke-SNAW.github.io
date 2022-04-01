---
id: e8t0zochj5qg52oa7mf56a6
title: This Pattern Will Make Your React Hooks Cleaner
desc: ""
updated: 1649037081994
created: 1649037023956
---

https://betterprogramming.pub/this-pattern-will-make-your-react-hooks-cleaner-ca9deba5d58d

```javascript
const customHook = () => {
  const isLoading = true; //logic
  const reload = () => {
    /*logic*/
  };
  const result = [isLoading, reload];
  result.isLoading = isLoading;
  result.reload = reload;
  return result;
};
```

That implementation will give us the ability to use the hook’s return value as:

```javascript
const { isLoading, reload } = customHook(configs); // as object
const [isLoading, reload] = customHook(configs); // as array
```
