---
id: 6369gjkobqwh0now11ib7tl
title: Pass The Reference
desc: ''
updated: 1654414150515
created: 1654414106612
---

https://glebbahmutov.com/blog/pass-reference/

```javascript
// cypress/integration/spec.js
import Alert from '../../src/Alert'
// if get the instance of alert from the application
cy.get(...).then(... => {
 // NOPE, will fail!
 expect(isAlert(appAlert)).to.be.true
})
```

So how do we ensure the spec has _the same Alert_ reference as the application? By avoiding importing it and instead getting it from the application. Following the approach outlined in the blog post [Send Data From The Application To The Cypress Test](https://glebbahmutov.com/blog/send-data-to-the-test/ "Send Data From The Application To The Cypress Test") we do the following in the application:

```javascript
// application code in "src"
import Alert from "./Alert";
if (window.Cypress) {
  window.Alert = Alert;
}
function isAlert(a) {
  return a instanceof Alert;
}
```

So when the application loads, it "saves" its `Alert` reference on the `window` object. From the spec we can get to that reference using the [cy.window](https://on.cypress.io/window) and [cy.its](https://on.cypress.io/its) commands. Even if it takes a little for the application to load and set the `window.Alert` no problem, the `cy.its` command [retries automatically](https://on.cypress.io/retry-ability) until that property is found.

```javascript
// cypress/integration/spec.js
// do not import Alert, instead
cy.window().its('Alert').then(Alert => {
 // ✅ The Alert instance now comes from the application code
 cy.get(...).then(... => {
 expect(isAlert(appAlert)).to.be.true
 })
})
```
