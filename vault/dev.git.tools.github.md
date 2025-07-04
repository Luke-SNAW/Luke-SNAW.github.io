---
id: y96Q2Fyzh0EQb9j3xGKjX
title: GitHub tools
desc: ""
updated: 1751594575282
created: 1644887290931
---

## Collections

- [Repobeats](https://repobeats.axiom.co/) - Stunning insights for your GitHub Repo
- [Include diagrams in your Markdown files with Mermaid](https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/)
- [actions/github-script](https://github.com/actions/github-script) - This action makes it easy to quickly write a script in your workflow that uses the GitHub API and the workflow run context.
- [Awesome Actions](https://github.com/sdras/awesome-actions) - A curated list of awesome things related to GitHub Actions.
- [Events that trigger workflows](https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows)
  - [Running your workflow only when a push of specific tags occurs](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#running-your-workflow-only-when-a-push-of-specific-tags-occurs)
  - [Running your workflow only when a push affects specific files](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#running-your-workflow-only-when-a-push-affects-specific-files)
- [github1s](https://github.com/conwnet/github1s) - One second to read GitHub code with VS Code.
- [act](https://github.com/nektos/act) - Run your GitHub Actions locally 🚀
- https://github.com/search?o=desc&q=stars%3A%3E100000&s=stars&type=Repositories
- [[vue, vite, tailwind로 공통 component package 만들기 (github private package)|journal.what-i-struggled-brag-in#week-17-2023---github-private-package]]

## Criticism

- [issues](https://news.ycombinator.com/item?id=33772556) - The "issues" on Github could be "bugs", "feature request" or even "improvement" (it could be anything actually).

## Security

- [Anyone can Access Deleted and Private Repository Data on GitHub](https://trufflesecurity.com/blog/anyone-can-access-deleted-and-private-repo-data-github)
  - don't use private forks. Copy the repository instead. [#](https://news.ycombinator.com/item?id=41060617)
  - the only way to securely remediate a leaked key on a public GitHub repository is through [key rotation](https://howtorotate.com/docs/introduction/getting-started/).
- [I scanned all of GitHub's "oops commits" for leaked secrets](https://trufflesecurity.com/blog/guest-post-how-i-scanned-all-of-github-s-oops-commits-for-leaked-secrets)
  - Maybe I missed it but the article doesn't mention the even easier way to see this: the activity tab. Any force push to hide ugly prototype code is kept forever which annoys me. — [Pwhy1](https://news.ycombinator.com/item?id=44452623)
