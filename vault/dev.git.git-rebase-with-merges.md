---
id: nejz8v61m5gbyeyjhtl15gz
title: Git Rebase... with Merges?
desc: ""
updated: 1668731939222
created: 1668731898268
---

> https://jnielson.com/git-rebase-with-merges

**Did you know that `git rebase -i` will drop merge commits by default?**

> Note: Needs git --version to be greater than v2.22.0 in order to have this feature

```shell
git rebase -i --rebase-merges [some commit]
```