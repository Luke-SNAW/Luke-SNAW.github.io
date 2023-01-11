---
id: npg73o89u51mfv0matorgku
title: Temp branch 운영
desc: ""
updated: 1673418559200
created: 1673417547325
---

## 문제

배포 환경에서만 테스트 할 수 있는 내용이라면 지속적으로 수정·배포·테스트를 진행  
이 과정 중에 다른 개발자가 테스트 서버에 배포하면 내용이 서로 상실되거나 브랜치 conflict가 빈번하게 발생할 수 있으므로, 개발자끼리 테스트 브랜치, 서버를 쓰겠다고 알린 뒤에 독점적으로 사용 중

## 해결

temp branch 운영. husky를 이용하여 temp branch를 push하기 전에 origin/test branch를 merge

> https://git-scm.com/docs/githooks#_pre_push

```shell
# .husky/pre-push
if [ `git rev-parse --abbrev-ref HEAD` == "temp" ]; then
   git fetch --prune;git merge origin/test
fi
# https://stackoverflow.com/questions/6372334/git-commit-hooks-per-branch/6376054#6376054
```

## Trouble shooting

push할 때 다음 error가 발생하면 `chmod`로 해당 파일에 실행 권한을 줄 것

> hint: The '.husky/pre-push' hook was ignored because it's not set as executable.
