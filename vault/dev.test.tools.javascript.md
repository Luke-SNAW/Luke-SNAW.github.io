---
id: l0icikuzriyciqacnfsyfnx
title: JavaScript
desc: ""
updated: 1649482347978
created: 1646182938803
---

- [Faker](https://github.com/faker-js/faker): Generate massive amounts of fake data in the browser and node.js
- [Responsively App](https://github.com/responsively-org/responsively-app): A modified web browser that helps in responsive web development.
- [Real World Testing with Cypress](https://learn.cypress.io/)
- [Cypress Real Events](https://github.com/dmtrKovalenko/cypress-real-events)

---

# Playwright

## [Cypress vs Playwright: Which is best for E2E testing?](https://cathalmacdonnacha.com/cypress-vs-playwright-which-is-best-for-e2e-testing)

Dec 16, 2021

> In the end, we decided to go with Playwright, mainly because of its native support for multiple domains, tabs and iFrames.  
> I will say that I found Cypress' debugging to be more developer-friendly and in general "slicker", but that wasn't enough to make us stay put.

## [Cypress vs Other Test Runners](https://glebbahmutov.com/blog/cypress-vs-other-test-runners/)

Playwright can:

- opens page as page, not in iframe
- emulates mobile devices
- runs against android devices and emulators
- runs tests that cross domains
- works with iframes
- runs tests that span several pages
- uses idiomatic async/await api which is not chained
- uses real browser network stack for routing and mocking
- detects occlusion problems
- selector expressiveness is unprecedented: https://playwright.dev/docs...
- tests pages with out-of-process iframes
- tests Web Workers
- tests Web Sockets
- tests Service Workers