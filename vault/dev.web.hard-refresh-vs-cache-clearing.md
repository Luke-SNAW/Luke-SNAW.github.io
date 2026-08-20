---
id: taqd33zknteokw2ld8kng1t
title: Hard Refresh Vs Cache Clearing
desc: ""
updated: 1787196927622
created: 1787196905564
---

하드 리프레시(Hard Refresh)는 **캐시를 삭제하는 것이 아니라 현재 페이지 로드 시에만 캐시를 우회(bypass)**합니다.

## 하드 리프레시 vs 캐시 삭제

Chrome DevTools에서 제공하는 3가지 reload 옵션:

1. **Normal Reload** - 일반 새로고침 (캐시 사용)
2. **Hard Reload** - 캐시 우회하고 새로고침 (캐시는 유지)
3. **Empty Cache and Hard Reload** - 캐시 삭제 후 새로고침

이 세 가지가 별개의 옵션으로 존재한다는 것 자체가 Hard Reload는 캐시를 삭제하지 않는다는 증거입니다.

### Chrome DevTools Reload 옵션 접근 방법

1. DevTools 열기 (F12 또는 Cmd+Option+I)
2. 주소창 왼쪽의 새로고침 버튼을 오른쪽 클릭 (또는 길게 클릭)
3. 드롭다운 메뉴에서 옵션 선택

**중요**: DevTools가 열려있을 때만 이 옵션들이 나타납니다.

## 하드 리프레시에 영향을 받지 않는 것

하드 리프레시는 다음을 **삭제하거나 변경하지 않습니다**:

- Cookies
- Local Storage
- Session Storage
- Saved passwords
- Form data
- Browser history

출처: [Chrome Hard Reload Explained - drizz.dev](https://www.drizz.dev/post/hard-reload-chrome-shortcuts-cache-clearing-and-common-fixes)

## QA 보고 사례: 새 탭에서 오래된 캐시 문제

### 문제 상황

1. 사용자가 `window.open(url, '_blank')`으로 새 탭 열기 → 오래된 HTML 표시
2. 하드 리프레시 수행 → 최신 HTML 표시
3. 다시 `window.open(url, '_blank')`으로 새 탭 열기 → 여전히 오래된 HTML 표시

### 원인

- 하드 리프레시는 **그 탭에서만** 캐시를 우회
- 브라우저의 HTTP 캐시는 **browser-wide**로 공유되며 삭제되지 않음
- 새 탭을 열 때는 일반적인 페이지 로드이므로 캐시를 사용

### 해결 방법

서버에서 `Cache-Control` 헤더를 명시적으로 설정:

```yaml
# HTML 파일: 캐시하지 않음
--cache-control 'no-store, no-cache, must-revalidate'
```

## 참고 자료

- [Chrome Hard Reload Explained - drizz.dev](https://www.drizz.dev/post/hard-reload-chrome-shortcuts-cache-clearing-and-common-fixes)
- [MDN - HTTP Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Caching)
- [MDN - Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)
