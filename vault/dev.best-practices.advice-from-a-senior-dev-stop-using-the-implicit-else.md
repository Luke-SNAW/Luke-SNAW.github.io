---
id: u30piqzarrbnded7pka0emt
title: Advice from a Senior Dev Stop Using the Implicit Else
desc: ""
updated: 1662446141771
created: 1662446033120
---

> https://javascript.plainenglish.io/advice-from-a-senior-dev-stop-using-the-implicit-else-2a2ecf0a3583

```js
function checkCountryCodeImplicit(country) {
  if (country === "United States") {
    return "+1";
  }
  if (country === "Uruguay") {
    return "+598";
  }
  if (country === "Uzbekistan") {
    return "+998";
  }
  // It's easy to forget what the condition for this return is!
  return "+44";
}
```

->

```js
function checkCountryCode(country) {
  if (country === "United States") {
    return "+1";
  } else if (country === "Uzbekistan") {
    return "+998";
  } else if (country === "Uruguay") {
    return "+598";
  } else if (country === "United Kingdom") {
    return "+44";
  } else {
    // This alerts us if a country is passed in that our function hasn't handled
    throw new Error("This input is not supported at the moment.");
  }
}
```
