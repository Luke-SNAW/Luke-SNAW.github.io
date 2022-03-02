---
id: gnh7pclc140wsbtf84b5yf8
title: Debug
desc: ""
updated: 1646265679834
created: 1646265630764
---

# [Developer Tools secrets that shouldn’t be secrets](https://christianheilmann.com/2021/11/01/developer-tools-secrets-that-shouldnt-be-secrets/)

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
