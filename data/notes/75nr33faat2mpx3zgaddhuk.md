
github 문서를 계속 찾아봐도 action이 실행되는 동안 제공되는 context에 대한 정보가 불명확해서 직접 출력하는 script를 찾아서 결과를 확인해봄

```yml
# https://github.com/orgs/community/discussions/27058#discussioncomment-3254475
name: "Print github context"
on:
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 1
    steps:
      - name: Check object
        run: |
          cat << OBJECT
          ${{ toJson(github) }}
          OBJECT
```
