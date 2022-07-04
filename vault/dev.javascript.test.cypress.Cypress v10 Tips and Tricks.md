---
id: g40joq8q80xsg6ii54nnoud
title: Cypress v10 Tips and Tricks
desc: ""
updated: 1656919229621
created: 1656919062565
---

> https://glebbahmutov.com/blog/cypress-v10-tips/

This blog post collects my tips for using Cypress v10+ which is a large step after the previous versions of Cypress. I plan to add more tips to this blog post as I use v10 more. See my post [Cypress Tips and Tricks](https://glebbahmutov.com/blog/cypress-tips-and-tricks/ "Cypress Tips and Tricks") for more content; most of it still applies to Cypress v10+ tests.

- [Register the plugins](https://glebbahmutov.com/blog/cypress-v10-tips/#register-the-plugins)
- [Launch the test runner in the desired mode](https://glebbahmutov.com/blog/cypress-v10-tips/#launch-the-test-runner-in-the-desired-mode)
- [Quickly change the testing type](https://glebbahmutov.com/blog/cypress-v10-tips/#quickly-change-the-testing-type)
- [Run all specs](https://glebbahmutov.com/blog/cypress-v10-tips/#run-all-specs)
- [Run E2E and component tests on CI](https://glebbahmutov.com/blog/cypress-v10-tips/#run-e2e-and-component-tests-on-ci)
- [Check the mode from the config file](https://glebbahmutov.com/blog/cypress-v10-tips/#check-the-mode-from-the-config-file)
- [Set the user values using the env block](https://glebbahmutov.com/blog/cypress-v10-tips/#set-the-user-values-using-the-env-block)

# Launch the test runner in the desired mode

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "eject": "react-scripts eject",
    "dev": "start-test 3000 cy:e2e",
    "e2e": "cypress open --e2e --browser electron",
    "comp": "cypress open --component --browser electron"
  }
}
```
