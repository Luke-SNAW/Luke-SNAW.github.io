---
id: w75ep21zwuxb5rv7323rinz
title: Git commands nobody has told you
desc: ""
updated: 1664154198292
created: 1652831885194
---

https://bootcamp.uxdesign.cc/git-commands-nobody-has-told-you-cd7025bea8db

# **Copy changes from another branch**

There are some scenarios where we have to add changes to more than one branches, for example if there are two versions and we support both of them, we should commit changes to both branches.

Let’s have two branches, **branchA** and bra**n**chB. Instead of committing in both branches manually, we can use **git rebase** command.

```bash
git checkout branchA
git rebase branchB
```

What will happen is that **branchA** will look like it was branched from **branchB**.

# Remove file from a commit

If we would like to remove a certain file that has been committed to a branch, we can use **git reset** command.

```bash
git reset --soft HEAD^
```

This will bring the committed files to the staging area and then we can specify exactly which file to remove.

```bash
git reset HEAD <filename>
```

# Find a commit with a bug

Have you been in a situation when a bug was introduced and you had to search when and what exactly was changed for this bug to appear? If you knew this command then, this process would be faster and easier. Using git bisect we can search for a commit which creates the bug, by first telling it a “bad” commit which has the bug and a “good” commit where it wasn’t there.

```bash
git bisect start
git bisect bad
git bisect good v.11.0.1-rc2
```

When we are done we should use **git bisect reset** to clean up the state and return to the original HEAD.

```bash
git bisect reset
```

# Show commits where a particular file was changed

There are cases when we want to see all of the changes to a particular file and this can be done using **git log** with **— follow** flag.

```bash
git log --follow -- <filename>
```

# Revert all local changes

There are different ways to remove local changes depending the scenario you have.

If you want to revert the changes to your working copy use:

```bash
git restore .
```

If you want to remove all unpushed commits to master use:

```bash
git reset
```

If you want to revert a change by a commit use:

```bash
git revert <commit>
```

If you want to remove untracked files or directories or use:

```bash
git clean -f or git clean -fd
```

> Stay tuned for Part 2, where will we look into the depths of git.
