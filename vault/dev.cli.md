---
id: 4ybwuj5k3hrpflb3snik3wh
title: CLI
desc: ""
updated: 1769128529317
created: 1681888715077
---

## Collections

- [What is Source Command in Linux and How Does it Work?](https://linuxhandbook.com/source-command/)
- [Command Line Interface Guidelines](https://clig.dev/)
  - [명령줄 인터페이스 가이드라인](https://clig.kr/)
- Setting PATH environment variable in OSX permanently
  > You have to add it to `/etc/paths`. - https://stackoverflow.com/a/22465399/26960115

## 라인 수 200 넘는 js, ts 파일 리스트 출력

```bash
wc -l $(find . -type f \( -name "*.ts" -o -name "*.js" \) ! -path "./node_modules/*" ! -path "./dist/*") 2>/dev/null | awk '$1 > 200 && !/total$/ {print}' | sort -rn
```
