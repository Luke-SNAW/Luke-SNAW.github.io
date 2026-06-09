---
id: t6vdrwfwa930p3uf76d8567
title: Vuejs 2의 router-link pointer-events-none + custom component g-button 조합 시 Cordova에서 file:/// 이동 문제
desc: ""
updated: 1780985796883
created: 1780985669302
---

## 현상

Cordova 앱에서 `pointer-events-none`인 `<router-link>` 안에 g-button을 중첩하면,
g-button 클릭 시 `$router.push`가 호출됨에도 불구하고 WKWebView(iOS)가 `file:///path`로 실제 파일 내비게이션을 시도해 빈 화면이나 에러가 발생한다.

```html
<!-- 문제 코드 -->
<router-link :to="guidePath" class="pointer-events-none lg:pointer-events-auto">
  <g-button
    class="pointer-events-auto lg:pointer-events-none"
    :click="() => $router.push(guidePath)"
  >
    詳しく
  </g-button>
</router-link>
```

웹(데스크탑)에서는 `lg:pointer-events-auto`로 인해 router-link가 정상 동작하므로 동일 증상이 없다.

## 원인

### 왜 file:/// 가 되는가

Cordova 앱은 `history` 모드 라우터를 `file://` 프로토콜 위에서 실행한다. `router.base`가 `''`(빈 문자열)이므로 `router-link :to="/dna-guide-old-kit"`가 렌더링하는 `<a>` 태그의 `href` 속성은 `/dna-guide-old-kit`이 되고, 브라우저 DOM에서는 이를 `file:///dna-guide-old-kit`으로 해석한다.

`$router.push`는 `history.pushState`를 통해 올바르게 컴포넌트를 전환하지만, 브라우저가 동시에 `<a>` href를 따라가면 덮어쓰인다.

### 왜 g-button 클릭이 `<a>` href를 따라가는가

`<a>` href를 따라가는 기본 동작은 `event.defaultPrevented === false`일 때 발생한다.

- **정상 동작하는 router-link(`pointer-events-auto`)**: 클릭 시 Vue Router의 내장 click handler가 `event.preventDefault()`를 호출 → `defaultPrevented = true` → 브라우저가 href를 따라가지 않음
- **문제 상황(`pointer-events-none`)**: Vue Router의 click handler가 실행되지 않음 → `preventDefault()` 미호출 → `defaultPrevented = false` 유지

g-button의 `@click.stop`은 `stopPropagation()`만 호출한다. 이벤트가 `<a>`까지 버블링되지 않더라도, 브라우저는 이벤트 dispatch 완료 후 `defaultPrevented`를 확인해 기본 동작을 결정한다. `stopPropagation()`은 이 판단에 영향을 주지 않는다.

### footer-gpj.vue의 동일 패턴이 정상인 이유

`footer-gpj.vue`의 `router-link :to="{ name: 'GpjDna' }"`는 `pointer-events-none`이 없다. 클릭 시 Vue Router click handler가 `preventDefault()`를 호출하므로 href 이동이 차단된다.

## 대처 방법

**g-button** 사용부에 `@click.native.prevent`를 추가한다. `<button>` 요소에서 `preventDefault()`를 먼저 호출해 `event.defaultPrevented = true`로 만들면, 이후 `@click.stop`의 `stopPropagation()`과 무관하게 브라우저가 `<a>` href를 따라가지 않는다.

```html
<!-- 수정 코드 -->
<router-link :to="guidePath" class="pointer-events-none lg:pointer-events-auto">
  <g-button
    class="pointer-events-auto lg:pointer-events-none"
    :click="() => $router.push(guidePath)"
    @click.native.prevent
  >
    詳しく
  </g-button>
</router-link>
```

### router-link에 붙이면 안 되는 이유

`router-link`에 `@click.native.prevent`를 붙이면 동작하지 않는다. g-button의 `@click.stop`이 이미 이벤트를 막아 `<a>`까지 이벤트가 전달되지 않기 때문에, `<a>`에 붙인 native listener는 실행되지 않는다.

### g-button 전역 수정이 위험한 이유

g-button 템플릿의 `@click.stop`을 `@click.stop.prevent`로 바꾸면 전역에서 `preventDefault()`가 호출되어, g-button이 `<form>` 안에서 쓰일 경우 form submit이 차단되는 부작용이 생긴다. 지역 한정 처리를 권장한다.
