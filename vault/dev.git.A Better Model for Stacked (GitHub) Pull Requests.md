---
id: 989qwa1a1itktzuar413ocg
title: A Better Model for Stacked (GitHub) Pull Requests
desc: ""
updated: 1647307309927
created: 1647307309927
---

https://0xc0d1.com/blog/git-stack/

# Basic idea

The only real solution to this problem (that I know of, anyway) is the notion of **stacked PRs**. Here's the basic idea:

- Create a pull request from a feature branch (say feature-1) to master
- Create a second pull request from another feature branch (say feature-2) to feature-1
- Repeat until you have a stack of pull requests
- When it's time to merge, start from the topmost PR (the one that's furthest from master) and merge/rebase every PR in until you merge the entire stack in to master

# Benefits

After having used the stacked PR workflow for a while, the benefits are readily apparent:

1. Dependencies: Changes that your feature depends on (but are otherwise unrelated) can go in a separate PR.
2. Reviewers: Every PR in the stack can potentially be assigned to a different set of reviewers, which can be helpful in a few different contexts - ramping, areas of expertise, or workload.
3. Incremental approval: Large, thorny changes can be approved in pieces.

# Tradeoffs

The stacked PR workflow in general can be very useful, but it isn't a silver bullet. There are concerns & tradeoffs to consider:

1. You can't create a stack of pull requests if you're on a fork.
2. Force-pushes are pretty much a requirement, so this doesn't work well for collaborative feature branches.
3. There's more initial overhead for the author; it's a lot easier (at first, anyway) to stick the entire change in the single PR.
