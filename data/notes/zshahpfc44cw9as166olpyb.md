
https://glebbahmutov.com/blog/solve-the-first-click/

# [Recording](https://glebbahmutov.com/blog/solve-the-first-click/#recording)

To record the test results and error screenshots on the Cypress Dashboard, I could have set the shown Cypress record key as an environment variable `CYPRESS_RECORD_KEY`. Since I am using GitHub Actions, I need to set the key as a secret.

```yml
name: ci
on: [push]
jobs:
  test:
    # use the reusable workflow to check out the code, install dependencies
    # and run the Cypress tests
    # https://github.com/bahmutov/cypress-workflows
    uses: bahmutov/cypress-workflows/.github/workflows/standard.yml@v1
    with:
      start: "npm run dev"
      wait-on: "http://localhost:3000"
      wait-on-timeout: 60
      record: true # to record
    secrets: # to record
      recordKey: ${{ secrets.CYPRESS_RECORD_KEY }}
```

# [The solution](https://glebbahmutov.com/blog/solve-the-first-click/#the-solution)

There are no observable attributes on the page I could find that would let me know when the application has finished attaching its event listeners. Thus I need to ask the button itself "do you have click event listener?" as described in [When Can The Test Click](https://glebbahmutov.com/blog/when-can-the-test-click/ "When Can The Test Click") blog post. I installed the [cypress-cdp](https://github.com/bahmutov/cypress-cdp) plugin and added a command to the test file [cypress/integration/spec.js](https://github.com/bahmutov/my-svelte-app/blob/main/cypress/integration/spec.js).

```javascript
import "cypress-cdp";

it("counts", () => {
  cy.visit("/");
  cy.contains("[data-cy=count]", "0");
  const incrementSelector = '[aria-label="Increase the counter by one"]';
  const decrementSelector = '[aria-label="Decrease the counter by one"]';
  cy.hasEventListeners(incrementSelector, { type: "click" });
  cy.get(incrementSelector).click();
  cy.contains("[data-cy=count]", "1");
  cy.get(incrementSelector).click();
  cy.contains("[data-cy=count]", "2");
  cy.get(decrementSelector).click();
  cy.contains("[data-cy=count]", "1");
});
```
