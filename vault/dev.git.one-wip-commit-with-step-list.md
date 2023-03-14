---
id: 5q5ack4phzcyigv8i4dlysh
title: One WIP commit with step list
desc: ""
updated: 1678750916208
created: 1677029017406
published: false
tags: draft
---

## 개념

1. feature를 개발 중에는 하나의 WIP에 다 때려박고 commit message에 장차 나눌 commit별 file list를 기록
2. 테섭에 올려 remote로 push commit의 경우 fixup으로 쌓는다.
3. 배포 때 rabase로 정리

## 계기

나중에 추가되는 code를 각 commit 의미에 맞게 rebase하는 수고가 많다. 회수 자체가 많기도 하고.

main에 나가야할 shared code(ex. component) 수정이 중간중간 섞여있는거 분리하기도 힘들다.

## 의문

한 파일에 다른 의미의 commit들로 정리해야 한다면?

## 주의

feature 개발 끝나고 의미를 기준으로 파일 별로 commit을 묶으면, 중간 commit 단계에선 필요한 파일이 없는 등 완전치 않다.  
commit별로 완전성을 추구하면 파일별 commit 내용을 쪼개야하는데 노력이 너무 든다.  
이 경우 feature-merge 단위로 완전성을 둬야 함.
