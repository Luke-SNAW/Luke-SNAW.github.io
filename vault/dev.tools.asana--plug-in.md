---
id: PSqXLI6YftRVtm4CWXKOD
title: Asana  Plug-in
desc: ""
updated: 1644973076154
created: 1644971914885
---

# Ticket Numbering

## 설치

Chrome extension [Ticket Number Generator](https://chrome.google.com/webstore/detail/ticket-number-generator-b/mkiflbeenlaomokhbibbgillnkppgane)

## 세팅

1. 확장 프로그램 우클릭
2. Manage extensions
3. Extension options
4. Identifier : team domain
   Prefix : `#IT-` (제일 앞에 빈 칸 하나 있음)

## 사용법

1. asana card title 편집 상태에 두고 확장 프로그램 클릭
2. Story point extension이 적용된 title이라면 충돌나기 때문에 (둘 다 prefix로 text 삽입)
   numbering text를 title 뒤쪽으로 옮겨야 함. (그래서 prefix 설정할 때 `빈 칸 + #`을 넣음)
3. 팀원들이 같은 identifier를 써야 ticket number 중복을 피할 수 있음 (서버로 요청하고 결과 받아옴)

## 주의점

- 제목 편집 상태가 아니면 티켓 넘버가 입력되지 않는다.
  하지만 클릭 수 만큼 counter가 올라감.

---

# Story Point

## 설치

Chrome extension: [Story Point for Asana](https://chrome.google.com/webstore/detail/storypoint-for-asana/ipkcinfcdhhcmibffhlklololceffgnc)

## 사용법

1. 설치하면 Ticket 속성 중 Story Point가 생기고, 이걸 클릭시 제목 맨 앞에 SP가 입력이 된다.
   ![Story Point](/assets/images/2022-02-16-09-51-19.webp)

2. 보드별로, 파이프라인별로 스코어 총 합을 알 수 있다. (노랑색은 완료 처리된 SP)

여기서 주의할 점은, 현재 렌더링된 티켓들만 계산이 된거라 티켓이 많으면 전부 스크롤 해서 로딩을 해야 정확한 SP를 알 수 있다.

![Story Point](/assets/images/2022-02-16-09-49-40.webp)
