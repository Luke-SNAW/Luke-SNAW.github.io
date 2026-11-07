
# Kakao Postcode SDK COEP 차단 이슈 해결

## 문제 상황

로컬 개발 환경(HTTP)에서 Kakao 우편번호 검색 SDK 사용 시 `Cross-Origin-Embedder-Policy (COEP)` 오류로 iframe이 차단되는 문제 발생

### 에러 메시지

```
Because your site has the Cross-Origin Embedder Policy (COEP) enabled,
each embedded iframe must also specify this policy.
```

### 증상

- 주소 검색 버튼 클릭 → Drawer는 정상 열림
- iframe은 렌더링되지만 내부 컨텐츠 로드 차단
- `http://postcode.map.kakao.com/search` 요청이 블락됨
- Response headers에 `NOT-SET Cross-Origin-Embedder-Policy` 표시

## 원인 분석 과정

### 1단계: Mixed Content 의심

- **가설**: HTTP 페이지에서 HTTPS 리소스 로드 시 블락
- **시도**: SDK src를 `http://`로 명시
  ```javascript
  src: "http://t1.kakaocdn.net/mapjsapi/bundle/postcode/prod/postcode.v2.js"
  ```
- **결과**: 실패 (SDK 내부에서 HTTPS 요청 하드코딩)

### 2단계: HTTPS 개발 서버 전환

- **시도**: `nuxt.config.ts`에 `devServer.https: true` 추가
- **결과**: 실패 (여전히 COEP 에러)

### 3단계: CSP 설정 확인

- **시도**: CSP meta 태그 비활성화
  ```typescript
  // meta: [cspMetaTag],
  ```
- **결과**: 실패 (CSP는 원인 아님)

### 4단계: Nuxt 헤더 설정 시도

- **시도**: `nitro.routeRules`에서 COEP 헤더 조정
  ```typescript
  headers: {
    'Cross-Origin-Embedder-Policy': 'unsafe-none',
    'Cross-Origin-Resource-Policy': 'cross-origin',
  }
  ```
- **결과**: 실패 (헤더는 설정되지 않음)

### 5단계: @nuxt/scripts 모듈 의심

- **발견**: `@nuxt/scripts` 모듈이 기본적으로 `crossOriginIsolated` 활성화
- **확인**: `console.log(window.crossOriginIsolated)` → `true`
- **시도**: 모듈 제거 및 `.nuxt` 폴더 삭제
- **결과**: 실패 (여전히 `true`)

### 6단계: 시크릿 모드 테스트

- **발견**: 시크릿 모드에서는 `window.crossOriginIsolated === false`
- **결론**: 브라우저 확장 프로그램이 원인!

### 7단계: 브라우저 확장 프로그램 확인

- **범인 확인**: "CORS Unblock" 확장 프로그램
- **원인 옵션**: "Append Headers to allow Shared Array Buffer"
  - 이 옵션이 COEP 헤더를 강제 주입
  - SharedArrayBuffer 사용을 위해 `crossOriginIsolated` 활성화

#### "Append Headers to allow Shared Array Buffer" 옵션의 목적

**SharedArrayBuffer란?**

- 멀티스레드 프로그래밍을 위한 JavaScript API
- 여러 Web Worker 간 메모리 공유 가능
- WebAssembly + 멀티스레드, 고성능 계산에 필수

**왜 COEP가 필요한가?**

- 2018년 Spectre/Meltdown 보안 취약점 발견 후 제한
- SharedArrayBuffer 사용 조건:
  ```
  Cross-Origin-Embedder-Policy: require-corp (또는 credentialless)
  Cross-Origin-Opener-Policy: same-origin
  ```
- 두 헤더 설정 → `window.crossOriginIsolated === true`

**CORS Unblock 확장의 동작**

- 모든 HTTP 응답에 COEP/COOP 헤더 강제 주입
- `SharedArrayBuffer`, `performance.measureUserAgentSpecificMemory()` 등 활성화

**부작용**

- 외부 iframe (Kakao, YouTube, Google Maps 등)이 CORP 헤더 없으면 차단
- 대부분의 서드파티 서비스는 CORP 헤더 미제공
- 일반적인 웹 개발에서는 불필요하며 오히려 방해

## 해결 방법

### ✅ 최종 해결책: CORS Unblock 확장 프로그램 설정 변경

**"Append Headers to allow Shared Array Buffer" 옵션 비활성화**

```
☐ Append Headers to allow Shared Array Buffer
```

**효과**:

- CORS 우회는 계속 동작
- COEP는 주입되지 않음
- `window.crossOriginIsolated === false`
- Kakao 우편번호 검색 정상 동작

### 검증 방법

브라우저 콘솔에서:

```javascript
console.log(window.crossOriginIsolated) // false 확인
```

## 교훈

1. **`crossOriginIsolated` 상태 확인이 핵심**
   - `window.crossOriginIsolated` 값으로 COEP 활성화 여부 즉시 확인 가능

2. **시크릿 모드 비교 테스트**
   - 일반 모드 vs 시크릿 모드 차이 → 브라우저 확장 프로그램 원인 파악

3. **브라우저 확장 프로그램 영향**
   - CORS 우회, 개발자 도구, 보안 관련 확장이 COEP를 주입할 수 있음
   - 특히 SharedArrayBuffer 관련 옵션 주의

## 참고 자료

- [COOP and COEP - web.dev](https://web.dev/articles/coop-coep)
- [Cross-Origin-Embedder-Policy - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Embedder-Policy)
