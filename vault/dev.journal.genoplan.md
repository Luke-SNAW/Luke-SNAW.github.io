---
id: djdvoLLYDZe9TkgbPbnIt
title: Genoplan
desc: ''
updated: 1668494475804
created: 1644454051319
---

[[writing.dev.brag-documents]]

## 2022/04

### Cypress

![cypress dashboard](assets/images/genoplan/cypress.webp)

## 2022/07

### Webpack v3 → v5

vue3이 나온 시점에서 무조건 최신 plugin을 쓰면 호환이 안되므로 vue2에 맞는 버전 일일히 찾아 설치함.

## 2022/09

### Package manager yarn → pnpm

배포 시간 -40s (package 설치 시간 감소 - cache 설정이 작동 안했다가 적용되는 듯)

![github actions - yarn](assets/images/genoplan/yarn.webp)

![github actions - yarn](assets/images/genoplan/pnpm.webp)

local disk space 절약

---

한 달 188k transaction

## 2022/11

### TanStack Query 적용

Powerful asynchronous state management, server-state utilities and data fetching.

report detail modal → page로 변환함에 따라 summary 화면과 전환이 잦고 그 때마다 API request를 함.  
stale time을 설정하여 정해진 시간 내에는 request 없이 cache data 활용하도록 수정
