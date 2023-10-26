---
id: 4gk9mt2w2x6r3i1fswjb7zj
title: Rust
desc: ""
updated: 1698306608620
created: 1646812868479
---

## Collections

- [From Javascript to Rust](assets/pdfs/from-javascript-to-rust.pdf) from https://github.com/vinodotdev/node-to-rust/
- [Rust basics, from the perspective of a high level programmer](https://danbulant.eu/posts/rust-basics)
  - [rust book](https://doc.rust-lang.org/book/) - an online book with short chapters about common things people want to do with Rust
  - [A gentle intro to Rust](https://stevedonovan.github.io/rust-gentle-intro/) - A short “book” that can be read in an hour or two, with a day or two worth of examples if you try them locally. Much more in-depth than this post, but still easy to grasp.
  - [r/rust](https://reddit.com/r/rust) - The well-moderated reddit community (quick to search. If you have a problem that will take longer than a single Discord message, post it here so that others are able to find it as well).
  - [The discord community](https://discord.gg/rust) - A simple way to quickly ask other developers
  - [rust by example](https://doc.rust-lang.org/rust-by-example/index.html) - The sort of thing I’d be going about in here as well, but this is just a quick short intro, that should be your go-to book if you want to learn even more.
- [Rust concepts I wish I learned earlier](https://rauljordan.com/rust-concepts-i-wish-i-learned-earlier/)
  - https://news.ycombinator.com/item?id=34427604

## Tools

- [Dioxus](https://github.com/DioxusLabs/dioxus) is a portable, performant, and ergonomic framework for building cross-platform user interfaces in Rust.

## [Was Rust Worth It?](https://jsoverson.medium.com/was-rust-worth-it-f43d171fb1b3)

> While Rust allows creating reliable software, its steep learning curve, rigid structure, and issues with async code can present roadblocks.

### [kuon's opinion](https://news.ycombinator.com/item?id=38021059)

I wrote a lot of rust, but after some years it still feels unproductive. I do a lot of zig now and I am like 10 times more productive with it. I can just concentrate on what I want to code and I never have to wonder what tool or what library to use.

I know rust gives memory safety and how important that is, but the ergonomic is really bad. Every time I write some rust I feel limited. I always have to search libraries and how to do things. I cannot just "type the code".

Also the type system can get out of control, it can be very hard to actually know what method you can call on a struct.

I still think rust is a great tool, and that it solves tons of problem. But I do not think it is a good general purpose language.

### [ostenning's opinion](https://news.ycombinator.com/item?id=38022460)

Opposite experience for me. Writing Rust on embedded systems greatly improved my confidence and speed. When using C a small mistake often leads to undefined behaviour and headaches. Rust theres none of that - its been a game changer for me.
