---
id: 5d1nk3a1ok64qnxteq2d6ce
title: OAuth 2.0 Grant Types 비교
desc: ''
updated: 1784167376889
created: 1784167360000
---

# OAuth 2.0 Grant Types 비교

**작성일:** 2026-07-16  
**목적:** Implicit Grant, Authorization Code Grant, PKCE의 차이와 보안 고려사항 이해

## 개요

OAuth 2.0은 앱 유형에 따라 다른 인증 플로우(Grant Type)를 제공합니다. 각 방식은 보안과 편의성 간의 트레이드오프가 있으며, 클라이언트 환경(백엔드 유무)에 따라 적합한 방식이 다릅니다.

## 1. Implicit Grant (Deprecated)

### 개념

가장 간단한 OAuth 플로우로, **authorization code 없이 바로 access_token을 반환**합니다.

### 플로우

```
1. 사용자 → OAuth 서버 로그인
   GET https://oauth.provider.com/authorize?
     response_type=token          ← 핵심: token 직접 요청
     &client_id=xxx
     &redirect_uri=https://myapp.com/callback
     &state=random123

2. 로그인 성공 → 즉시 access_token 반환
   https://myapp.com/callback#access_token=ya29.xxx&token_type=Bearer&expires_in=3600
                             ↑ URL Fragment (#) 사용

3. JavaScript로 token 추출 및 사용
   const token = new URLSearchParams(window.location.hash.slice(1)).get('access_token')
```

### 특징

- ✅ **간단함**: 한 번의 요청으로 완료
- ✅ **client_secret 불필요**: 프론트엔드에서 완결
- ✅ **백엔드 불필요**: SPA에 적합
- ❌ **보안 취약**: access_token이 URL에 노출
- ❌ **브라우저 히스토리에 저장**: 탈취 위험
- ❌ **Refresh token 미지원**: 장기 인증 불가

### 보안 문제

```javascript
// ❌ 위험 1: URL에 token 노출
https://myapp.com/callback#access_token=SENSITIVE_TOKEN
// → 브라우저 히스토리, 로그, Referer 헤더에 남을 수 있음

// ❌ 위험 2: XSS 공격에 취약
// 악성 스크립트가 window.location.hash에서 바로 추출 가능

// ❌ 위험 3: 브라우저 확장 프로그램
// 모든 URL에 접근 가능한 확장 프로그램이 token 탈취 가능
```

### 상태

- **2012년 (RFC 6749)**: SPA를 위한 권장 방식 ✅
- **2019년**: OAuth 2.0 Security Best Practices에서 deprecated ⚠️
- **2020년+**: 사용 금지 권고 🚫

## 2. Authorization Code Grant

### 개념

**2단계 인증 플로우**로, 먼저 authorization code를 받은 후 이를 access_token으로 교환합니다. `client_secret`이 필수이며, **백엔드 처리를 강제**합니다.

### 플로우

```
1. 사용자 → OAuth 서버 로그인 (프론트엔드)
   GET https://oauth.provider.com/authorize?
     response_type=code           ← 핵심: code 요청
     &client_id=xxx
     &redirect_uri=https://myapp.com/callback
     &state=random123

2. 로그인 성공 → authorization code 반환
   https://myapp.com/callback?code=SplxlOBeZQQ&state=random123
                             ↑ Query parameter (?) 사용
                             ↑ 짧은 수명 (10분), 일회용

3. Code를 access_token으로 교환 (백엔드)
   POST https://oauth.provider.com/token
   Headers:
     Content-Type: application/x-www-form-urlencoded
   Body:
     grant_type=authorization_code
     &client_id=xxx
     &client_secret=SECRET_KEY    ← 백엔드에만 존재!
     &code=SplxlOBeZQQ
     &redirect_uri=https://myapp.com/callback

   Response:
   {
     "access_token": "ya29.xxx",
     "refresh_token": "refresh_xxx",
     "token_type": "Bearer",
     "expires_in": 3600
   }

4. API 호출
   (access_token은 백엔드에서 관리하거나 안전하게 프론트엔드로 전달)
```

### 특징

- ✅ **안전**: access_token이 URL에 노출 안 됨
- ✅ **Refresh token 지원**: 장기 인증 가능
- ✅ **앱 검증**: client_secret으로 등록된 앱인지 확인
- ✅ **보안 계층 분리**: 프론트엔드(공개)/백엔드(비공개)
- ❌ **복잡함**: 두 번의 요청 필요
- ❌ **백엔드 필수**: client_secret 안전 보관 필요

### 보안 설계 의도

```
┌─────────────────────────────────────────────┐
│ 프론트엔드 (공개 채널)                       │
├─────────────────────────────────────────────┤
│ ✓ 사용자 인증                                │
│ ✓ authorization code 수신                   │
│   └─ 짧은 수명 (10분)                        │
│   └─ 일회용 (재사용 불가)                     │
│   └─ 노출되어도 상대적으로 안전                │
└─────────────────────────────────────────────┘
              ↓ code 전달
┌─────────────────────────────────────────────┐
│ 백엔드 (비공개 채널)                         │
├─────────────────────────────────────────────┤
│ ✓ code + client_secret → token 교환         │
│   └─ client_secret: 절대 노출 안 됨          │
│   └─ access_token: URL 거치지 않음           │
│   └─ refresh_token: 서버에만 보관            │
│ ✓ 민감 정보는 백엔드에만 존재                 │
└─────────────────────────────────────────────┘
```

### client_secret의 역할

**1. 앱 인증 (App Authentication)**

```javascript
// OAuth 서버 입장에서의 검증
if (request.client_secret === registered_secret) {
  // ✅ 등록된 앱에서 온 요청이 맞음
  return { access_token: "..." }
} else {
  // ❌ code를 탈취해서 악용하려는 시도
  return { error: "invalid_client" }
}
```

**2. 백엔드 강제 (Force Backend)**

- client_secret을 안전하게 보관하려면 → **백엔드 서버 필수**
- 프론트엔드에서는 절대 사용 불가 (노출되면 보안 위협)

**3. 보안 계층 분리**

- 프론트엔드: code만 다룸 (노출되어도 덜 위험)
- 백엔드: secret + token 관리 (완전 비공개)

## 3. PKCE (Proof Key for Code Exchange)

### 개념

Authorization Code Grant의 **개선 버전**으로, **client_secret 없이도 안전한 인증**을 제공합니다. SPA와 모바일 앱을 위한 최신 권장 방식입니다.

### 핵심 아이디어

```
client_secret 대신 "동적으로 생성한 비밀키"를 사용
→ 매 로그인마다 새로운 키 생성
→ code를 탈취해도 비밀키 없으면 무용지물
```

### 플로우

```
1. code_verifier 생성 (랜덤 문자열)
   const codeVerifier = generateRandomString(128)
   // 예: "dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk"

2. code_challenge 생성 (SHA-256 해시)
   const codeChallenge = base64url(sha256(codeVerifier))
   // 예: "E9Melhoa2OwvFrEMTJguCHaoeK1t8URWbuGJSstw-cM"
   sessionStorage.setItem('pkce_verifier', codeVerifier)

3. 로그인 요청 (code_challenge 포함)
   GET https://oauth.provider.com/authorize?
     response_type=code
     &client_id=xxx
     &redirect_uri=https://myapp.com/callback
     &code_challenge=E9Melhoa2OwvFrEMTJguCHaoeK1t8URWbuGJSstw-cM
     &code_challenge_method=S256   ← SHA-256 사용
     &state=random123

4. Authorization code 수신
   https://myapp.com/callback?code=SplxlOBeZQQ&state=random123

5. Token 교환 (code_verifier로 검증)
   POST https://oauth.provider.com/token
   Body:
     grant_type=authorization_code
     &client_id=xxx
     &code=SplxlOBeZQQ
     &redirect_uri=https://myapp.com/callback
     &code_verifier=dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk

   서버 검증:
   if (sha256(code_verifier) === stored_code_challenge) {
     // ✅ 동일한 앱에서 온 요청 확인
     return { access_token: '...' }
   }
```

### 특징

- ✅ **client_secret 불필요**: 프론트엔드에서 완결
- ✅ **안전**: Authorization Code Grant 수준의 보안
- ✅ **Refresh token 지원**: 장기 인증 가능
- ✅ **XSS 방어**: code를 탈취해도 verifier 없으면 무용지물
- ✅ **백엔드 불필요**: SPA/모바일 앱에 적합
- ⚠️ **OAuth 서버 지원 필요**: 모든 제공자가 지원하는 것은 아님

### 보안 원리

```
공격자가 authorization code를 탈취했다고 가정:

❌ Implicit Grant:
   code 없음 → token이 URL에 바로 노출 → 탈취 성공

❌ Auth Code (without PKCE):
   code만으로 token 교환 가능 → 탈취 성공

✅ PKCE:
   code를 탈취해도 code_verifier가 없으면 교환 실패
   → code_verifier는 sessionStorage에만 존재
   → 공격자는 token 획득 불가
```

### Kakao/Naver 지원 여부

| Provider   | PKCE 지원 | Implicit Grant   | 비고                      |
| ---------- | --------- | ---------------- | ------------------------- |
| **Kakao**  | ❌ 미지원 | ❌ 기본 비활성화 | Authorization Code만 강제 |
| **Naver**  | ❌ 미지원 | ✅ 지원          | Implicit Grant 허용됨     |
| **Google** | ✅ 지원   | Deprecated       | PKCE 권장                 |
| **GitHub** | ✅ 지원   | Deprecated       | PKCE 권장                 |

## 비교 표

### 기본 비교

| 항목              | Implicit Grant | Auth Code Grant     | PKCE        |
| ----------------- | -------------- | ------------------- | ----------- |
| **response_type** | `token`        | `code`              | `code`      |
| **client_secret** | 불필요         | **필수**            | 불필요      |
| **백엔드 필요**   | ❌             | ✅                  | ❌          |
| **보안 수준**     | ❌ 낮음        | ✅ 높음 (백엔드 시) | ✅ 높음     |
| **브라우저 노출** | Token 노출     | Code만 노출         | Code만 노출 |
| **Refresh Token** | ❌             | ✅                  | ✅          |
| **상태**          | Deprecated     | 표준                | 최신 권장   |

### 보안 비교

| 공격 벡터             | Implicit        | Auth Code             | PKCE             |
| --------------------- | --------------- | --------------------- | ---------------- |
| **URL 노출**          | ❌ Token 노출   | ✅ Code만 (안전)      | ✅ Code만 (안전) |
| **XSS 공격**          | ❌ 취약         | ⚠️ 백엔드 시 안전     | ✅ 안전          |
| **Code 탈취**         | N/A             | ⚠️ Secret 없으면 취약 | ✅ Verifier 필요 |
| **브라우저 히스토리** | ❌ Token 저장됨 | ✅ Code만             | ✅ Code만        |
| **중간자 공격**       | ❌ 취약         | ✅ HTTPS 필수         | ✅ HTTPS 필수    |

### 사용 사례

| 앱 유형                       | 권장 방식          | 이유                             |
| ----------------------------- | ------------------ | -------------------------------- |
| **전통적인 웹앱** (백엔드 有) | Auth Code Grant    | client_secret 안전 보관 가능     |
| **SPA** (백엔드 無)           | **PKCE**           | client_secret 없이 안전          |
| **모바일 앱**                 | **PKCE**           | 코드 디컴파일 위험               |
| **데스크톱 앱**               | PKCE               | 설치 파일에서 secret 추출 가능   |
| **레거시 SPA**                | ~~Implicit Grant~~ | Deprecated - PKCE로 마이그레이션 |

## 권장 사항

**SPA / 모바일 앱:**

```
✅ PKCE (Authorization Code Grant with PKCE)
   - client_secret 불필요
   - 안전함
   - 최신 권장 방식
```

**전통적인 웹앱 (백엔드 有):**

```
✅ Authorization Code Grant (백엔드에서 처리)
   - client_secret은 서버 환경변수로 관리
   - Token 교환은 백엔드에서만
```

## 참고 자료

### OAuth 2.0 스펙

- [RFC 6749 - OAuth 2.0 Framework](https://tools.ietf.org/html/rfc6749)
- [RFC 7636 - PKCE](https://tools.ietf.org/html/rfc7636)
- [OAuth 2.0 Security Best Current Practice](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-security-topics)

### Kakao 관련

- [Kakao OAuth 공식 문서](https://developers.kakao.com/docs/ko/kakaologin/rest-api)
- [Kakao SDK v2 마이그레이션](https://developers.kakao.com/docs/ko/javascript/migration)
