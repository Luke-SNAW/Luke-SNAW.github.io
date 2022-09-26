---
id: 989qwa1a1itktzuar413ocg
title: A Better Model for Stacked (GitHub) Pull Requests
desc: ""
updated: 1664154184184
created: 1647307309927
---

> https://timothya.com/blog/git-stack/ has interactive examples

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

# Conclusion

Ultimately, stacking PRs is just another tool to help manage GitHub-based code review. I've found that it works well for large changes (4+ PRs), but small-to-medium changes are generally better off as commits on a single PR. There's undoubtedly some discretion that needs to be applied here, but don't be afraid to use a stack of PRs if the situation calls for it!

The tooling situation is not great, admittedly. I haven't found another tool that does what `gh-stack` does, and there's a lot of room for improvement there. I'm also hoping for [something GitHub-native](https://twitter.com/natfriedman/status/1170804894241972224) in the near future. 🤞

As for immediate next steps, I want to add functionality to `gh-stack` so it creates the initial set of PRs on Github for you. Right now you have to create them manually and make sure each PR has the right _merges into_ value set, which can be somewhat error prone.
