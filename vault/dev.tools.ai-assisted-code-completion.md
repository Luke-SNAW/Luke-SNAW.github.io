---
id: wkkv4ptfhb0d0mxczybkqtp
title: Ai Assisted Code Completion
desc: ""
updated: 1656376640718
created: 1656030439228
---

[Github Copilot](https://github.com/features/copilot/)(이하 C) vs [Tabnine](https://www.tabnine.com/)(이하 T)

# 사용경험

Copilot만 몇 개월 경험.

- 하단과 JSON 비슷한 데이터 셋팅에 자주 도움 됨. 가끔가다 어캐했누 소리가 절로 나옴.
  ```js
  const REPORT = {
    "Basic 20+": {
      categories: ["cancer", "general-disease", "ancestry"].map(toLabel),
      txtCountItems: toLabel("items-total-basic"),
    },
    "Standard 80+": {
      categories: ["cancer", "general-disease", "ancestry", "traits"].map(
        toLabel
      ),
      txtCountItems: toLabel("items-total-standard"),
    },
    "GPFA 15": {
      categories: ["cancer", "general-disease"].map(toLabel),
      txtCountItems: toLabel("items-total-gpfa"),
    },
    "GPFA 25": {
      categories: ["cancer", "general-disease", "traits"].map(toLabel),
      txtCountItems: toLabel("items-total-gpfa-two"),
    },
  };
  ```
- 일반 코드 snippet도 기존 code 찾아서 copy&paste하는 시간보다 제시된 코드 수정하는게 빠를 때가 종종 있음.
- naming에 가끔 도움 됨
- 개인적인 의견으로 5% 미만으로 시간 단축시켜주나 영혼출타를 부르는 단순작업의 뼈대 세워주는 것만해도 사용추천

# 테스트 Plan

- C - 2달 무료
- T - 무료 plan (하루 횟수 제한이라 짜증날 수도)

# 지원 IDE

- C - VS, VS code, Neovim, JetBrains IDEs (https://github.com/features/copilot)
- T - 많음. vs code, IntelliJ 포함

# code 제안 특징

- C
  - 한 번에 한 code block만 제안. 응답 속도가 좀 있음. 약간 답답
    ![https://www.actuia.com/wp-content/uploads/2021/07/GitHub-Copilot.gif](https://www.actuia.com/wp-content/uploads/2021/07/GitHub-Copilot.gif)
- T
  - 제안 code는 몇 가지 옵션을 제시. typing 속도에 맞춰 code 제시. 응답 속도 빠름
    ![https://cdn.hashnode.com/res/hashnode/image/upload/v1635891875639/jbvlAGpKS.gif?auto=format,compress&gif-q=60&format=webm](https://cdn.hashnode.com/res/hashnode/image/upload/v1635891875639/jbvlAGpKS.gif?auto=format,compress&gif-q=60&format=webm)
  - local code 학습 능력이 있다고 함

# 개인정보 보호?

- C - 무슨 정보 보호 정책이 있긴한데 일단 github 측으로 코드 전송이 있다고 함
- T - 기본인지 옵션 설정인지 모르겠지만 code 전송 없음
