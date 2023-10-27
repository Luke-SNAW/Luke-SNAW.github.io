---
id: hvcwysicrmsq7evtybwjpuv
title: Object-Oriented Programming is Bad

desc: ""
updated: 1698396444761
created: 1698396054146
---

> https://www.youtube.com/watch?v=QM1iUe6IofM

- Object-oriented programming is not inherently bad, but the pervasive use of classes as the primary unit of abstraction leads to problems. Not all code needs to be organized into classes.

- Encapsulating all code and data into rigid classes results in abstractions that do not fit problems well and introduce unnecessary complexity.

- Shared state and implicit coupling between objects caused by shared mutable objects undermine encapsulation and make code difficult to understand and maintain.

- Java popularized OOP but did not prove it is the best paradigm. Its success was also due to addressing other issues at the time rather than benefits of OOP itself.

- Code with many small, fractured units like tiny classes and methods scattered across files is difficult to comprehend.

- Procedural programming that minimizes shared state through parameterization is a viable alternative to favor in many cases.

- Pure functions are the ideal unit of code as they are fully self-contained. Code should opportunistically embrace purity.

- Longer methods with descriptive comments can be easier to understand than decomposing logic into many smaller units.

- Data types can help logically organize global state without requiring rigid classes.

- Language features like inline blocks that encapsulate code without extracting it could help address issues while keeping code linear.

---
