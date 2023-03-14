---
id: 2qiksgdv8iqkfg3wk64yqoy
title: The Role of Devops
desc: ""
updated: 1678748692175
created: 1648193871776
---

https://medium.com/pragmatic-programmers/the-role-of-devops-33a2171c004d

Three practices cover the role of DevOps in deploying your app:

- Continuous integration
- Continuous delivery
- Continuous deployment

They form a kind of ladder of DevOps maturity or advancement. Each rung of that ladder has a set of goals as well as a set of costs or challenges.
![ladder of devops](/assets/images/the-role-of-devops.webp)

## Continuous Integration

The first step on the ladder to more successful and reliable deployments is continuous integration. At this stage, everyone on the team adopts the practice of checking the code into the repository often. This means merging any changes into the master branch (or main trunk) of the repo. This is the practice I covered in Chapter 1, [Getting Started with API First](https://medium.com/@pragprog/chapter-1-getting-started-with-api-first-c48ac3a7186). Those check-ins should kick off automated tests too. We saw how to do that using Postman and Newman in Chapter 9, [Testing APIs](https://medium.com/@pragprog/chapter-9-testing-apis-d8684ba54e56).

By checking in your changes often and running automated tests for every check-in, you end up validating the project quite a few times and getting immediate success/fail feedback on each small set of changes. This means you catch problems early, when they’re easier to fix. Using scripted/automated tests means your tests are more consistent and the results are more reliable.

Continuous integration handles the coding, check-in, and testing steps.

## Continuous Delivery

At this point, the process of releasing into final staging is automated through scripting. That means deployment is reduced to making some selections (or configurations) and pressing a button. Now, along with scripted testing from continuous integration you also have scripted deployment to the staging level.

Continuous delivery handles the coding, check-in, testing, and staging steps.

## Continuous Deployment

At this stage, we’re not just scripting testing and staging deployment. We’re also making deployment into production automatic. That means making the entire process of testing and deploying your app completely driven by scripts and other tooling without the need for a human to “press a button.” Typically this is done by setting up your source code check-in process to handle the entire test-and-deploy process.

The test-and-deploy process usually looks like this:

- A developer checks code into the repository.
- That check-in kicks off a series of local tests.
- If the tests pass, the code is built into a release package.
- If the build succeeds, the build is deployed to a staging server.
- If the staging server deployment succeeds, another set of integration tests are run.
- If the integration tests succeed, the build is deployed on a production server.
- If the production deployment succeeds, the job is done.
