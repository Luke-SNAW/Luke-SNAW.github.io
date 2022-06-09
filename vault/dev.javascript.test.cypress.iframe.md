---
id: o6mu2pxtapvjdbf9i00rbct
title: Iframe
desc: ""
updated: 1655093793369
created: 1655091140018
---

```js
// https://bahr.dev/2019/09/02/testing-stripe-elements/
Cypress.Commands.add("iframeLoaded", { prevSubject: "element" }, ($iframe) => {
  if (Cypress.config("chromeWebSecurity"))
    throw new Error(
      "To get stripe element `chromeWebSecurity` must be disabled"
    ); // https://medium.com/swinginc/testing-stripe-integration-with-cypress-3f0d665cfef7

  const contentWindow = $iframe.prop("contentWindow");
  return new Promise((resolve) => {
    if (contentWindow && contentWindow.document.readyState === "complete") {
      resolve(contentWindow);
    } else {
      $iframe.on("load", () => {
        resolve(contentWindow);
      });
    }
  });
});
Cypress.Commands.add(
  "getInDocument",
  { prevSubject: "document" },
  (document, selector) => Cypress.$(selector, document)
);
Cypress.Commands.add("getWithinIframe", (targetElement) =>
  cy.get("iframe").iframeLoaded().its("document").getInDocument(targetElement)
);
```

```js
it("Stripe 테스트 결제", () => {
  const cyStripe = (selector) =>
    cy
      .get('iframe[name="stripe_checkout_app"]')
      .iframeLoaded()
      .its("document")
      .getInDocument(selector);

  cyStripe("#email").type("luke@genoplan.com");
  cyStripe("#card_number").type("4000056655665556"); // debit
});
```

```json
// cypress.config.js
chromeWebSecurity: false  //  for stripe test, accessing iframe on local
```
