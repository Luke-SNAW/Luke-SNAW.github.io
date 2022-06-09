---
id: l29gxghljchn5f6o27ma72d
title: Setting
desc: ""
updated: 1655193445612
created: 1655167183618
---

# Global git config list

```shell
git config --list
git config --list --show-origin
```

# Alias

```shell
git config --global alias.cp cherry-pick
git config --global alias.cm commit
git config --global alias.co checkout
git config --global alias.rb rebase -i
git config --global alias.rs restore
git config --global alias.pl pull
git config --global alias.ps push
git config --global alias.df diff
git config --global alias.st status
git config --global alias.lg log --graph --abbrev-commit --decorate --format=format:'%C(cyan)%h%C(reset) - %C(green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(yellow)%d%C(reset)' --all
git config --global alias.ad add
git config --global alias.tg tag -n
git config --global alias.br branch
```

# Rebase

```shell
git config --global rebase.autosquash true
git config --global merge.conflictstyle diff3
git config --global rerere.enabled true
```

# Template

```shell
git config --global commit.template ~/.gitmessage
```
