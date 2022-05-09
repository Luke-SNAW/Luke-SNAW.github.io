---
id: 9ougup81n2xo18fqoe98rs7
title: Send Data From The Application To The Cypress Test
desc: ""
updated: 1652055946412
created: 1652055764476
---

https://glebbahmutov.com/blog/send-data-to-the-test/

```javascript
// public/app.js

if (data.phone) data.phone = data.phone.replace(/[^\d]/g, ""); // clean up the phone number by removing all non-digit characters

window?.Cypress?.track?.("form", data);
```

Of course, we need to create the `Cypress.track` method ourselves. We also need to clean it up to avoid accidentally leaking it from one test to another. Using `beforeEach` and `afterEach` hooks works well for this purpose.

```javascript
// cypress/integration/spec.js
beforeEach(() => {
  Cypress.track = cy.stub().as("track");
});

afterEach(() => {
  // clean up Cypress.track property
  delete Cypress.track;
});
```

Now we can finish our test. We can confirm the [stub](https://on.cypress.io/stub) function `Cypress.track` was called with the first argument "form". From the first such call, we can grab the _second_ argument, which should be an object. We can confirm some properties of the object, and then also use it to confirm what the application sent to the server.

```javascript
// cypress/integration/spec.js
it("sends the expected form", () => {
  cy.visit("public/index.html");

  cy.intercept("POST", "/api/v1/message", {}).as("post");
  cy.get("form").within(() => {
    cy.get("input[name=name]").type("John Doe");
    cy.get("input[name=email]").type("joe@doe.com");
    cy.get("input[name=phone]").type("+1 (555) 555-5555");
    cy.get("input[name=message]").type("Hello World");
    cy.get("input[type=submit]").click();
  });

  // hmm, how do we verify the request as sent by the application?
  cy.get("@track")
    .should("be.calledWith", "form")
    .its("firstCall.args.1")
    // you can confirm some properties of the sent data
    // Tip: use https://github.com/bahmutov/cy-spok
    // for similar object and array assertions
    .should("deep.include", {
      name: "John Doe",
      message: "Hello World",
    })
    .then((data) => {
      cy.log(JSON.stringify(data));
      // confirm the network request was sent correctly
      cy.wait("@post")
        .its("request.body", { timeout: 0 })
        .should("deep.equal", data);
    });
});
```
