---
id: toxmbwct8elj033ffogg0ie
title: Level of parallelism
desc: ""
updated: 1653983538136
created: 1653983503602
---

https://coredumped.dev/2022/05/19/a-vision-of-a-multi-threaded-emacs/#what-level-of-parallelism-do-you-want

Level 1 - memory unsafe and data races allowed

Languages where incorrect code can lead to corruption of the program state and segfaults. This includes C++ and Swift.

Level 2 - memory safe and data races allowed

Languages where parallelism is memory safe, but can still lead to data races. This includes Java and Go.

Level 3 - memory safe and no data races

Languages that enable [fearless concurrency](https://doc.rust-lang.org/book/ch16-00-concurrency.html) by eliminating unguarded access to shared-memory. This includes Clojure, Rust, and TCL.

Generally the closer you are Level 1 the more footguns there are, but the more performance you can squeeze out. The higher you go the easier concurrent code is to write, but you have less performance and control. The exception to this is Rust, which is a safe Level 3 language with the performance of a Level 1.
