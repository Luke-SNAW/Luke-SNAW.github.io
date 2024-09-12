---
id: 4a5zty96wbgszd07faxjv78
title: Git
desc: ""
updated: 1726107571461
created: 1652404655162
---

## Collections

- [Introducing the Space Git Flow](https://blog.jetbrains.com/space/2023/04/18/space-git-flow/) - Branching Strategies about Git flow, GitHub flow, Trunk-based development, Space Git Flow
- [When to use "chore" as type of commit message?](https://stackoverflow.com/a/26944812/5163033)
  > "`grunt task`" means nothing that an external user would see:
  >
  > - implementation (of an _existing feature_, which doesn't involve a fix),
  > - configuration (like the `.gitignore` or `.gitattributes`),
  > - private internal methods...
- [Confusing git terminology](https://jvns.ca/blog/2023/11/01/confusing-git-terminology/)
- [Why some of us like "interdiff" code review](https://gist.github.com/thoughtpolice/9c45287550a56b2047c6311fbadebed2)

## [How to Write Useful Commit Messages](https://dev.to/jacobherrington/how-to-write-useful-commit-messages-my-commit-message-template-20n9)

- This commit will `What`
- `Why`

## [How do I commit case-sensitive only filename changes in Git?](https://stackoverflow.com/a/20907647/5163033)

```shell
git mv -f yOuRfIlEnAmE yourfilename
```

## [Commit with offered message editing](https://stackoverflow.com/questions/41181942/git-commit-with-template-message)

```shell
git commit -em "some string"
```

would open the text editor with "some string" that could be edited.

## [git commit --fixup=[(amend|reword):]<commit>](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt---fixupamendrewordltcommitgt)

## [Tracking SQLite Database Changes in Git](https://garrit.xyz/posts/2023-11-01-tracking-sqlite-database-changes-in-git)

First, add a diff type called "sqlite3" to your config. The simplest way is to just run these commands:

```shell
git config diff.sqlite3.binary true
git config diff.sqlite3.textconv "echo .dump | sqlite3"
```

Alternatively, you can add this snippet to your `~/.gitconfig` or `.git/config` in your repository:

```gitconfig
[diff "sqlite3"]
        binary = true
        textconv = "echo .dump | sqlite3"
```

Next, create a file called `.gitattributes` if it's not already present and add this line:

```gitattributes
*.sqlite diff=sqlite3
```

> [So it does look like git's delta encoding works with sqlite's blocks.](https://news.ycombinator.com/item?id=38117779)
