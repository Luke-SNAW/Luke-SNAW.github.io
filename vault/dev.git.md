---
id: 4a5zty96wbgszd07faxjv78
title: Git
desc: ""
updated: 1692321452438
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
