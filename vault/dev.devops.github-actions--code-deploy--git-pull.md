---
id: 26h3tfb1gqg656z1me77tgs
title: GitHub Actions  Code Deploy  Git Pull
desc: ""
updated: 1674618871696
created: 1674612380914
---

## 사용처

build 과정 없이 script만 배포하면 되는 project

## Setup - github actions, code deploy

[[dev.devops.github-actions--s3--code-deploy]] 참고

## Code deplay - git pull

```shell
# after-install__test.sh

#!/bin/bash
cd /var/www/html/biz
ssh -vT git@github.com # https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey#always-use-the-git-user
git fetch --prune
git checkout origin/test
git pull origin test
```

### git auth 참고 링크

- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints
