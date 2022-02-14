---
id: gYXXxzE1hbYsUtusQq8zA
title: "A pipe operator for JavaScript: introduction and use cases"
desc: ""
updated: 1644800150975
created: 1644799968834
---

https://2ality.com/2022/01/pipe-operator.html

The proposal [“Pipe operator (|>) for JavaScript”](https://github.com/tc39/proposal-pipeline-operator#tacit-unary-function-application-syntax) (by J. S. Choi, James DiGioia, Ron Buckton and Tab Atkins) introduces a new operator.

---

There originally were two competing proposals for a pipe operator, inspired by other programming languages:

- F# by Microsoft is a functional programming language whose core is based on OCaml. This pipe operator works together well with curried functions (I’ll explain what that is soon).

- Hack by Facebook is – roughly – a statically typed version of PHP. This pipe operator focuses on language features other than curried functions. It includes syntactic support for partial application.

The latter proposal won. However, if you prefer the F# pipe, there is good news: Its benefits may be added to the Hack pipe at a later time (details are explained later).
