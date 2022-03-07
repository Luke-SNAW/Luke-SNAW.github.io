---
id: uf4zpuxkf6di8v8i3uzdhs5
title: JavaScript Execution Context – How JS Works Behind The Scenes
desc: ""
updated: 1646699258171
created: 1646699018476
---

https://www.freecodecamp.org/news/execution-context-how-javascript-works-behind-the-scenes/

Before we dive in, here are some prerequisites to familiarize yourself with, because we'll use them often in this article.

- **JavaScript Engine**: A JavaScript engine is simply a computer program that receives JavaScript source code and compiles it to the binary instructions (machine code) that a CPU can understand.

# How JavaScript Code Gets Executed

...

The browser's JavaScript engine then creates a special environment to handle the transformation and execution of this JavaScript code. This environment is known as the `Execution Context`.

The Execution Context contains the code that's currently running, and everything that aids in its execution.

During the Execution Context run-time, the specific code gets parsed by a parser, the variables and functions are stored in memory, executable byte-code gets generated, and the code gets executed.

There are two kinds of Execution Context in JavaScript:

- Global Execution Context (GEC)
- Function Execution Context (FEC)

## Global Execution Context (GEC)

... WIP
