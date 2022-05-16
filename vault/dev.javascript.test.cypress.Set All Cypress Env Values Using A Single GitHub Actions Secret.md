---
id: m07q638xtiaicpa56y172us
title: Set All Cypress Env Values Using A Single GitHub Actions Secret
desc: ""
updated: 1652688074309
created: 1652687907738
---

https://glebbahmutov.com/blog/secrets-to-env/

You can pass an entire JSON object of values using a single GitHub Actions secret by saving it as cypress.env.json file.

```shell
npx cypress run --env userName=${{ secrets.USERNAME }},password=${{ secrets.PASSWORD }}
```

It all works if you only have a few simple values to pass. If you have multiple values, or if they are complex JSON objects, passing them via command line is bound to break due to parsing and quotes. Luckily, there are other ways, and this blog post shows one good way for GitHub Actions.

```json
// cypress.json
{
  "env": {
    "person": {
      "name": "Jane",
      "age": 25
    },
    "location": {
      "city": "San Francisco"
    }
  }
}
```

```javascript
// cypress/integration/spec.js
it("has valid env values", () => {
  expect(Cypress.env())
    .to.be.an("object")
    .and.to.include.keys("person", "location");
  cy.wrap(Cypress.env("person"))
    .should("have.keys", "name", "age")
    .its("age")
    .should("be.within", 10, 99);
  cy.log("**name:** " + Cypress.env("person").name);
  cy.log("**city:** " + Cypress.env("location").city);

  // save a screenshot of the test runner
  // to show what the env values were
  cy.screenshot("env", { capture: "runner" });
});
```

To better separate Cypress own configuration values from the user's own values, you could move the env object from cypress.json to cypress.env.json file.

````json
// cypress.env.json
{
  "person": {
    "name": "Jane",
    "age": 25
  },
  "location": {
    "city": "San Francisco"
  }
}
```
````
