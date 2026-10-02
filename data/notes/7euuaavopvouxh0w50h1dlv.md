
> 작성일: 2026-03-27 | from Claude Opus 4.6

## 개요

Astro 6의 `ClientRouter`를 사용한 View Transition 활성화 방법과, View Transition API 자체와 SPA 라우팅의 성능 이점을 구분하여 정리한다.

## 내용

### 전환 애니메이션 옵션

| 옵션            | 설명                                                               |
| --------------- | ------------------------------------------------------------------ |
| `fade` (기본값) | 페이드 인/아웃                                                     |
| `slide`         | 이전 페이지 밀려나고 새 페이지 슬라이드 인 (뒤로가기 시 반대 방향) |
| `morph`         | 동일 `transition:name` 요소 간 위치/크기 보간                      |
| `none`          | 시각적 전환 효과 없음                                              |
| 커스텀          | `@keyframes` 직접 정의 가능                                        |

`transition:animate`는 `<html>` 등 HTML 요소에 디렉티브로 적용한다 (ClientRouter의 prop이 아님).

### `animate="none"`이어도 달라지는 점

시각적 애니메이션만 비활성화될 뿐, ClientRouter의 SPA 라우팅은 그대로 동작한다:

- 전체 페이지 새로고침 없이 DOM 교체
- `transition:name`이 같은 요소 간 morph 보간
- `transition:persist` 지정 요소는 전환 시에도 유지

### 성능 이점의 출처: View Transition vs SPA 라우팅

**View Transition API** (브라우저 네이티브)는 DOM 스냅샷 간 시각적 애니메이션만 담당하며 성능 이점이 없다.

**SPA 라우팅**이 실제 성능 이점의 원천이다:

- 공통 리소스(CSS, JS, 폰트) 재파싱/재실행 방지
- 공통 레이아웃(header, footer) 리렌더 최소화
- 브라우저 상태(스크롤, 미디어 재생, 포커스) 유지

Astro의 `ClientRouter`는 View Transition API + SPA 라우터를 묶어서 제공하므로 둘이 함께 활성화된다. React Router, Next.js, Nuxt 등 다른 SPA 프레임워크는 이미 SPA 라우팅을 사용하고 있어 해당 성능 이점을 기본적으로 갖고 있다.

### 브라우저 미지원 시 Fallback

`ClientRouter`의 `fallback` prop으로 View Transition API를 지원하지 않는 브라우저의 동작을 제어한다.

```astro
<ClientRouter fallback="swap" />
```

아래 옵션은 **View Transition API 미지원 브라우저에서의 동작**만 제어하며, 지원 브라우저에서는 항상 SPA 라우팅이 정상 동작한다.

| 값                 | 미지원 브라우저에서의 동작                             |
| ------------------ | ------------------------------------------------------ |
| `animate` (기본값) | CSS 애니메이션으로 전환 효과를 모방한 뒤 DOM 교체      |
| `swap`             | 애니메이션 없이 즉시 DOM 교체 (SPA 라우팅은 유지)      |
| `none`             | SPA 라우팅 비활성화, 일반 MPA처럼 전체 페이지 새로고침 |

View Transition API는 Chromium 기반 브라우저(Chrome, Edge, Opera)에서 지원되며, Firefox와 Safari는 미지원 또는 부분 지원 상태다. `animate="none"`을 사용하는 경우 `fallback="swap"`과 결과적으로 동일하므로 별도 설정이 필요 없다.

### 주의사항

- 정적 콘텐츠 위주 사이트에서는 체감 차이가 크지 않으며, 네트워크가 느리거나 공통 JS가 무거울 때 효과가 두드러진다

### ClientRouter의 단점

- **JS 필수** — JavaScript가 비활성화된 환경에서는 네비게이션이 깨질 수 있다
- **번들 크기 증가** — SPA 라우터 스크립트가 추가로 로드됨
- **서드파티 스크립트 호환성** — 전체 페이지 로드를 가정하는 외부 스크립트(analytics, 광고 등)가 페이지 전환 시 정상 동작하지 않을 수 있다
- **스크립트 생명주기 관리** — 모든 DOM 이벤트 바인딩을 `astro:page-load`로 감싸야 하고, cleanup이 필요한 경우 `astro:before-preparation` 등 추가 이벤트 처리 필요. 또한 `astro:page-load`는 **모든 페이지 전환마다** 발생하므로, 특정 페이지 전용 스크립트는 콜백 초입에 URL 체크(예: `if (!location.pathname.startsWith('/library')) return`)를 추가해야 한다. 없으면 다른 페이지로 전환 시 `Cannot read properties of null` 에러가 발생한다
- **디버깅 복잡도** — MPA에서는 페이지 로드마다 상태가 초기화되지만, SPA에서는 이전 페이지의 메모리 누수나 상태 잔존이 문제가 될 수 있다

## 참고

- [Astro View Transitions](https://docs.astro.build/en/guides/view-transitions/)
- [View Transition API (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API)
