---
id: 7lfBuLShnSydgCh1ZVEd5
title: Tools
desc: ""
updated: 1668043443451
created: 1645487597560
---

## Collections

- [Speedy Web Compiler](https://swc.rs/) - Rust-based platform for the Web
- [bun](https://bun.sh/) is like postcss, babel, node & webpack in one 100x faster tool for building modern web frontends. Early access
- [Partytown](https://github.com/BuilderIO/partytown) is a lazy-loaded library to help relocate resource intensive scripts into a web worker, and off of the main thread. Its goal is to help speed up sites by dedicating the main thread to your code, and offloading third-party scripts to a web worker.
- [pnpm](https://github.com/pnpm/pnpm) - Fast, disk space efficient package manager
  - Fast. Up to 2x faster than the alternatives (see benchmark).
  - Efficient. Files inside node_modules are linked from a single content-addressable storage.
  - Great for monorepos.
  - Strict. A package can access only dependencies that are specified in its package.json.
  - Deterministic. Has a lockfile called pnpm-lock.yaml.
  - Works as a Node.js version manager. See pnpm env use.
  - Works everywhere. Supports Windows, Linux, and macOS.
  - Battle-tested. Used in production by teams of all sizes since 2016.
  - https://pnpm.io/cli/import
  - `pnpm outdated --json` https://github.com/pnpm/pnpm/releases/tag/v7.15.0
- [npm-check-updates](https://github.com/raineorshine/npm-check-updates) - Find newer versions of package dependencies than what your package.json allows
  - Selectively update the dependencies that you choose
    ```shell
      ncu -i
    ```
- [Volta](https://github.com/volta-cli/volta) - The Hassle-Free JavaScript Tool Manager
  - [Volta vs. nvm for JavaScript tooling](https://sirre.al/2021/02/12/volta-vs-nvm-for-managing-javascript-tooling/)
- [Upgraderoo](https://upgraderoo.janez.tech/) helps you upgrade NPM packages, discover outdated packages and saves you time to focus on building your product.
