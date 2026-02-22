
https://ponyfoo.com/articles/testing-javascript-modules-with-tape

In this article well get an in-depth look at these three modules ([tape](https://github.com/substack/tape), [proxyquire](https://github.com/thlorenz/proxyquire), and [sinon](https://github.com/cjohansen/Sinon.JS)), learn why they are better than the competition, how to use them, what each of them is good for, and how they complement each other to provide the ultimate “testing harness”, figuratively speaking, no test harness is actually needed!

While everything else in the JavaScript universe seems to be moving at blisteringly fast speeds, and accelerating, testing is in this weird place where globals are mystically okay. Frameworks like mocha and jasmine dominate the field, while they require a test harness, litter the global object with variables, and generally go against established best practices. I’ve always found it kind of really weird that test frameworks, which are supposed to be used to improve the code quality around a codebase, may end up doing the exact same opposite by encouraging the usage of globals and awkward monkey patching.

# Leveraging proxyquire to mock modules

Besides using test databases, you could also mock services and libraries you don’t want to have an influence on the outcome of a particular test. There are plenty of ways of doing this, but I find that the best of them is to grab the dependency by its roots and remove it altogether. The proxyquire module makes the process quite easy for both the server and the browser.

# Complementing proxyquire with Sinon.JS

Sinon.JS provides you with many ways in which you can mock objects in JavaScript. While proxyquire is the best thing you could be using to replace an entire module with a stub, sinon makes it quite easy to create the stubs that you’ll be providing to proxyquire.
