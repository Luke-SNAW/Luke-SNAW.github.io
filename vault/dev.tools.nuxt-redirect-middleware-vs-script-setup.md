---
id: hq804fsuzxa4wlqgohfhrzl
title: "Nuxt 3 SPA 리다이렉트: 미들웨어 vs script setup vs onMounted"
desc: ""
updated: 1776756342154
created: 1776756305568
---

> 작성일: 2026-04-21 | from claude-sonnet-4-6

## 개요

Nuxt 3 SPA 모드(`ssr: false`)에서 페이지 진입 시 리다이렉트를 처리하는 세 가지 방법의 동작 원리와 차이점을 정리한다.

## 내용

### 방법별 실행 시점 비교

| 방법                                  | 실행 시점                            | 컴포넌트 렌더 여부 | 깜빡임                   |
| ------------------------------------- | ------------------------------------ | ------------------ | ------------------------ |
| `definePageMeta` 미들웨어             | 라우터 beforeEach (컴포넌트 로드 전) | 없음               | 없음                     |
| `<script setup>` + `await navigateTo` | 컴포넌트 마운트 직후                 | 있음 (렌더 불안정) | 있음                     |
| `onMounted` + `navigateTo`            | DOM 완전 렌더 후                     | 있음               | 있음 (빈 화면 한 프레임) |

---

### `<script setup>` 방식의 문제

`await navigateTo('/login')`을 `<script setup>` 안에서 호출하면, Vue Router의 `router.replace()`가 비동기 가드 체인을 거쳐 실행된다. 이 시점에 Vue는 이미 현재 컴포넌트를 렌더 대상으로 확정한 상태이므로, 라우터 전환과 렌더 사이클의 타이밍 불일치로 대상 페이지가 렌더되지 않거나 빈 화면이 될 수 있다.

```
라우터 "/" 매칭
→ index.vue 컴포넌트 로드
→ <script setup> 실행
→ await navigateTo('/login') 호출  ← 이미 렌더 큐에 올라간 후
→ 라우터 전환 시도
→ login.vue 렌더 불안정
```

---

### `onMounted` 방식의 문제

`onMounted`는 DOM이 완전히 렌더된 후 실행되므로 대상 페이지는 정상 렌더된다. 그러나 리다이렉트 전 현재 페이지(index.vue)의 빈 화면 또는 default 레이아웃이 한 프레임 노출되는 깜빡임이 발생한다.

---

### 미들웨어 방식 (권장)

`definePageMeta`의 미들웨어는 Vue Router의 `beforeEach` navigation guard 안에서 실행된다. 컴포넌트가 로드되기 전에 리다이렉트가 결정되므로 index.vue는 렌더 큐에 올라가지 않는다.

```vue
<!-- app/pages/index.vue -->
<script setup>
definePageMeta({
  middleware: () => {
    const token = useCookie("token")
    return navigateTo(token.value ? "/customer-list" : "/login", {
      replace: true,
    })
  },
})
</script>

<template></template>
```

```
라우터 "/" 매칭
→ beforeEach에서 미들웨어 실행
→ navigateTo('/login') 반환 → 라우터가 /login으로 재매칭
→ index.vue 로드 자체가 발생하지 않음
→ login.vue 렌더
```

---

### 핵심 원칙

`<script setup>`은 **컴포넌트 안**이고, 미들웨어는 **라우터 안**이다. 리다이렉트는 라우터 수준에서 처리해야 렌더 사이클과 충돌하지 않는다.

## 참고

- [Nuxt 3 Route Middleware](https://nuxt.com/docs/guide/directory-structure/middleware)
- [Nuxt 3 navigateTo](https://nuxt.com/docs/api/utils/navigate-to)
- [Vue Router Navigation Guards](https://router.vuejs.org/guide/advanced/navigation-guards.html)
