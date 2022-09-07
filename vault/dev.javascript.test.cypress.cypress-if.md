---
id: itrcsgdehw4u6oop73pgqfs
title: Conditional Commands For Cypress
desc: ""
updated: 1662510633088
created: 1662510306831
---

> https://glebbahmutov.com/blog/cypress-if/

## [Conditional logic using cy.then](https://glebbahmutov.com/blog/cypress-if/#conditional-logic-using-cythen)

One solution is to grab the input element and check ourselves using the [cy.then](https://on.cypress.io/then) command.

```js
it("submits the terms forms", () => {
  cy.visit("cypress/terms.html");
  cy.get("#agreed").then(($input) => {
    if ($input.is(":checked")) {
      cy.log("The user already agreed");
    } else {
      cy.wrap($input).click();
    }
  });
  cy.get("button#submit").click();
});
```

## [Conditional logic using cypress-if](https://glebbahmutov.com/blog/cypress-if/#conditional-logic-using-cypress-if)

Instead of writing `.then` callbacks, you could use my [cypress-if](https://github.com/bahmutov/cypress-if) plugin. This plugin lets you write `if / else` commands right inside a chain of commands without using `cy.then` and `cy.wrap`.

Let's install the plugin as a dev dependency and simplify our test

```bash
$ npm i -D cypress-if
# or install the plugin using Yarn
$ yarn add -D cypress-if
```

```js
import "cypress-if";
it("submits the terms forms", () => {
  cy.visit("cypress/terms.html");
  cy.get("#agreed")
    .if("not.checked")
    .click() // IF path
    .else()
    .log("The user already agreed"); // ELSE path
  cy.get("button#submit").click();
});
```

The child commands `.if()` and `.else()` come from the `cypress-if` plugin. You can use any Cypress assertion as the `.if(assertion)` condition; by default it is element existence. If the input button is unchecked, the test takes the "IF" path and skips the "ELSE" portion of the command chain.

You can have multiple commands in the "IF" and "ELSE" portions, you can use `cy.then`, `cy.within` commands, etc. See the plugin's README for more examples of writing conditional command chains.

## [Warning: not every situation requires conditional commands](https://glebbahmutov.com/blog/cypress-if/#warning-not-every-situation-requires-conditional-commands)

In our situation the best solution is to use the [cy.check](https://on.cypress.io/check) command. This command does nothing if the checkbox is already checked!

```js
it("submits the terms forms", () => {
  cy.visit("cypress/terms.html");
  cy.get("#agreed")
    // check the input box
    // if it is not checked already
    // https://on.cypress.io/check
    .check();
  cy.get("button#submit").click();
});
```

For a similar lesson on using the built-in Cypress commands instead of conditional testing, see the free lesson "Lesson d4: How to avoid conditional test logic" in my course [Cypress Plugins](https://cypress.tips/courses/cypress-plugins). Deterministic tests are the best, use the conditional test commands only if you really cannot control the application in any other way.
