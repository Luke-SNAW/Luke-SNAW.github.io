---
id: mhxcmb8w2e7ubhe05s7wtib
title: TLA+ 인증 명세 (Auth.tla / MCAuth.cfg) 해설
desc: ""
updated: 1775627880014
created: 1775627863585
---

> 작성일: 2026-04-08 | from claude-sonnet-4-6

## 개요

`specs/auth/` 디렉토리의 TLA+ 인증 명세(`Auth.tla`, `MCAuth.tla`, `MCAuth.cfg`, `Common.tla`)의 구조와 핵심 개념을 설명한다. MC 래퍼 패턴, 불변식, 활성도, 시간 연산자를 다룬다.

## 모듈 구조

```
Common.tla          공유 타입: Users, Passwords, Pages, UserRecord, ...
    └── Auth.tla    인증 상태머신 명세
            └── MCAuth.tla   TLC 모델체킹 래퍼
                    └── MCAuth.cfg   TLC 설정 파일
```

### MCAuth.cfg 구성

| 섹션                     | 내용                                                            |
| ------------------------ | --------------------------------------------------------------- |
| `CONSTANTS`              | 모델값 선언 + 집합 정의                                         |
| `Accounts <- MCAccounts` | 함수 리터럴 우회 (cfg 문법 제약)                                |
| `SPECIFICATION Spec`     | `Init /\ [][Next]_authVars /\ WF(...)`                          |
| `INVARIANTS`             | TypeOK, SignedInImpliesAuthenticatedPage, SessionMatchesAccount |
| `PROPERTIES`             | PendingLoginEventuallyResolves (liveness)                       |

---

## MC 래퍼 패턴

### 왜 필요한가

TLC `.cfg` 파일의 `CONSTANTS` 섹션은 세 가지 문법만 허용한다:

```
Foo = bareword          # model value
Foo = {m1, m2, ...}     # model value 집합
Foo <- OperatorName     # 연산자 오버라이드
```

`[u1 |-> pw1, u2 |-> pw2]` 같은 함수 리터럴은 파서가 이해하지 못한다. `Auth.tla`의 `Accounts` 상수는 함수값이어야 하므로 직접 cfg에 쓸 수 없다.

### 해결 구조

`MCAuth.tla`에 함수를 연산자로 정의하고 cfg에서 `<-`로 바인딩한다.

```tla
---- MODULE MCAuth ----
EXTENDS Auth, TLC   \* TLC 필수: @@ 와 :> 가 TLC 모듈 소속

MCAccounts == (u1 :> pw1) @@ (u2 :> pw2)
====
```

```
\* MCAuth.cfg
Accounts <- MCAccounts
```

TLC는 `MCAuth.tla`를 평가할 때 `MCAccounts`를 호출해 함수값을 만들고, 그것을 `Accounts`에 바인딩한다.

### 주의사항

- `Auth.tla`에 `Accounts`라는 CONSTANT가 이미 선언되어 있으므로, MC 래퍼에서 같은 이름으로 operator를 정의하면 충돌 → 반드시 `MCAccounts`처럼 다른 이름 사용 후 `<-` 오버라이드
- `@@`, `:>`는 TLA+ 코어가 아닌 `TLC` 표준 모듈 소속 → `EXTENDS Auth, TLC` 필수
- NULL 센티넬은 문자열(`"__NULL__"`)이 아닌 `CONSTANT`로 선언해 model value로 사용해야 TypeOK 평가 시 타입 충돌이 없음

---

## Spec 정의

```tla
Spec == Init /\ [][Next]_authVars /\ WF_authVars(LoginSucceeds) /\ WF_authVars(LoginFails)
```

| 항                           | 역할                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| `Init`                       | 초기 상태 조건                                               |
| `[][Next]_authVars`          | 모든 스텝에서 Next 실행 또는 authVars 불변 (stuttering 허용) |
| `WF_authVars(LoginSucceeds)` | 로그인 성공 액션의 약한 공정성                               |
| `WF_authVars(LoginFails)`    | 로그인 실패 액션의 약한 공정성                               |

`Init /\ [][Next]_authVars`만으로는 Safety만 보장. WF 조건을 추가해야 Liveness까지 보장된다.

### `authVars` 튜플

```tla
authVars == <<currentPage, session, pendingLogin>>
```

세 변수를 튜플로 묶은 단축 이름. `UNCHANGED authVars`와 `WF_authVars(A)` subscript에 사용된다. 변수가 추가/삭제될 때 이 한 줄만 고치면 모든 액션에 자동 반영된다.

---

## 불변식 (Safety Invariants)

"어떤 상태에서도 항상 참이어야 한다" — TLC가 도달 가능한 모든 상태를 탐색하며 위반 즉시 반례를 출력한다.

### TypeOK

각 변수가 정해진 타입 안에 있는지 확인하는 기반 불변식. 다른 불변식들은 이 위에서 동작한다.

### SignedInImpliesAuthenticatedPage

```tla
SignedInImpliesAuthenticatedPage ==
    session /= NULL => currentPage \notin {"/login", "/signup"}
```

"세션이 있으면 인증된 페이지에 있어야 한다." 대우: 로그인/회원가입 페이지에 있다면 세션이 없어야 한다.

`LoginSucceeds`에서 `currentPage' = "/my-tests"` 대입이 누락되면 즉시 위반된다. Cypress의 `cy.url().should('include', '/my-tests')`와 대응하는 형식적 서술.

### SessionMatchesAccount

```tla
SessionMatchesAccount ==
    session /= NULL => Accounts[session.id] = session.password
```

"활성 세션의 자격증명은 반드시 등록된 계정과 일치해야 한다." `LoginSucceeds`가 `Accounts[id] = password` 조건을 체크한 후에만 세션을 만들기 때문에 유지된다.

---

## 활성도 (Liveness Property)

"결국에는 반드시 일어나야 한다" — 시간 축을 따라 검증. 반례는 무한 루프(lasso) 형태.

### PendingLoginEventuallyResolves

```tla
PendingLoginEventuallyResolves ==
    (pendingLogin /= NULL) ~> (pendingLogin = NULL)
```

"로그인 시도가 걸려있으면, 언젠가는 반드시 해소된다."

`pendingLogin`을 NULL로 만드는 액션은 `LoginSucceeds`와 `LoginFails` 둘뿐이다. `Spec`의 `WF_authVars(LoginSucceeds) /\ WF_authVars(LoginFails)`가 없으면 시스템이 `NavigateTo`만 무한 반복해도 명세 위반이 아니게 된다.

### Safety vs Liveness

|           | Safety (불변식)            | Liveness (활성도)                      |
| --------- | -------------------------- | -------------------------------------- |
| 질문      | 나쁜 일이 일어나지 않는가? | 좋은 일이 결국 일어나는가?             |
| 위반      | 특정 상태 하나에서 발생    | 무한히 지속되는 경로에서 발생          |
| 서술 방식 | 상태 조건만으로 서술       | `~>`, `<>`, `[]<>` 등 시간 연산자 필요 |

---

## Weak Fairness vs Strong Fairness

```tla
WF_vars(A) == [](ENABLED <<A>>_vars) => []<><<A>>_vars
SF_vars(A) == []<>ENABLED <<A>>_vars => []<><<A>>_vars
```

|             | WF                            | SF                           |
| ----------- | ----------------------------- | ---------------------------- |
| 보장 조건   | enabled가 끊기지 않고 지속    | enabled가 무한히 자주 발생   |
| 강도        | 약함                          | 강함 (WF를 포함)             |
| 적합한 경우 | 한번 가능해지면 조건이 유지됨 | 가능/불가능을 반복할 수 있음 |

`LoginSucceeds`/`LoginFails`는 `pendingLogin`이 설정되면 해소될 때까지 enabled 상태가 끊기지 않으므로 WF로 충분하다.

SF가 필요한 경우: 채널에 메시지를 넣었다 뺐다 하는 시스템처럼 `Recv`의 enabled 상태가 켜졌다 꺼지기를 반복할 때.

---

## 시간 연산자

실행 경로(무한히 이어지는 상태 시퀀스) 전체를 대상으로 서술한다.

### `[]` — Always

```tla
[]P  \* 모든 상태에서 P가 참
```

불변식이 바로 `[]P` 형태. `INVARIANTS TypeOK`는 TLC에게 `[]TypeOK`를 검사하라는 뜻.

### `<>` — Eventually

```tla
<>P  \* 어떤 상태에서는 P가 참
```

### `[]<>` — Always Eventually

```tla
[]<>P  \* P가 무한히 자주 참이 된다
```

상태: s0 s1 s2 s3 s4 s5 s6 ...  
 P: ✗ ✓ ✗ ✗ ✓ ✗ ✓ ... → []<>P 성립  
 P: ✗ ✓ ✗ ✗ ✗ ✗ ✗ ... → []<>P 위반 (s1 이후 P 안 나타남)

SF 정의에 등장: `SF_v(A) == []<>ENABLED<<A>>_v => []<><<A>>_v`

### `<>[]` — Eventually Always

```tla
<>[]P  \* 언젠가부터 P가 영원히 참이 된다 (안착)
```

상태: s0 s1 s2 s3 s4 s5 ...  
 P: ✗ ✗ ✓ ✗ ✓ ✓ ... → <>[]P 아직 모름 (계속 봐야 함)  
 P: ✗ ✗ ✓ ✓ ✓ ✓ ... → <>[]P 성립 (s2부터 영원히 참)

시스템이 로그인 완료 상태에 안착하는 것을 서술할 때 사용.

### `~>` — Leads-to

```tla
P ~> Q  ==  [](P => <>Q)
\* P가 참인 상태에 도달할 때마다, 이후 언젠가는 반드시 Q가 참이 된다
```

P: ✗ ✓ ✗ ✗ ✓ ✗ ...  
Q: ✗ ✗ ✓ ✗ ✗ ✓ ...  
------↑-----↑  
-P 이후 Q----P 이후 Q → P ~> Q 성립

### 강도 관계

```
[]P  →  []<>P  →  <>P
[]P  →  <>[]P  →  <>P
```

---

## 연산자 vs 함수 (TLA+ 용어)

TLA+에서 공식 용어는 두 가지다.

| TLA+ 용어    | 문법                | 특징                                                                   |
| ------------ | ------------------- | ---------------------------------------------------------------------- |
| **Operator** | `Op(x) == ...`      | 수식의 약칭(abbreviation). 값으로 전달 불가. 매크로에 가까운 수식 치환 |
| **Function** | `f[x \in S] == ...` | 값(value). 도메인이 있고 `f[x]`로 적용. 수학의 집합론적 매핑           |

`NavigateTo(page)`와 `Next`는 모두 Operator. 차이는 매개변수 유무와 의미적 역할뿐이다.

---

## TLC 상태공간 탐색

TLC는 BFS(너비 우선 탐색)로 `Next`의 모든 분기를 현재 상태에서 시도하고, enabled인 것을 모두 후계 상태로 등록한다.

초기 상태 (Init)  
 currentPage = "/login"  
 session = NULL  
 pendingLogin = NULL

이 상태에서 Next의 각 분기를 시도:

### 분기 1: \E u \in Users, p \in Passwords : SubmitLogin(u, p)

SubmitLogin의 enabled 조건:
/\ session = NULL ✓  
 /\ pendingLogin = NULL ✓  
 /\ currentPage = "/login" ✓

{u1,u2} × {pw1,pw2,pw_bad} 6가지 모두 enabled → 6개 후계 상태 생성

1. 후계 상태 1-1: pendingLogin = [id:u1, password:pw1]
2. 후계 상태 1-2: pendingLogin = [id:u1, password:pw2]
3. 후계 상태 1-3: pendingLogin = [id:u1, password:pw_bad]
4. 후계 상태 1-4: pendingLogin = [id:u2, password:pw1]
5. 후계 상태 1-5: pendingLogin = [id:u2, password:pw2]
6. 후계 상태 1-6: pendingLogin = [id:u2, password:pw_bad]

### 분기 2: LoginSucceeds

enabled 조건:
/\ pendingLogin /= NULL ✗ (NULL임)  
 → disabled, 후계 상태 없음

분기 3: LoginFails → disabled (동일 이유)  
분기 4: Logout → disabled (session = NULL)  
분기 5: NavigateTo → disabled (session = NULL)

### 결과: 탐색 큐에 6개 추가

큐: [상태1-1, 상태1-2, 상태1-3, 상태1-4, 상태1-5, 상태1-6]

각 상태에서 다시 같은 과정 반복. 예를 들어 상태1-1에서:

상태1-1: pendingLogin = [id:u1, password:pw1]

LoginSucceeds enabled?  
 pendingLogin /= NULL ✓
Accounts[u1] = pw1 ✓ → enabled → 후계 상태 생성

LoginFails enabled?
pendingLogin /= NULL ✓  
 Accounts[u1] /= pw1 ✗ → disabled

SubmitLogin enabled?
pendingLogin = NULL ✗ → disabled

---

전체 그림

                      Init
                       │
          ┌────────────┼──────────────┐
        (u1,pw1)    (u1,pw2)  ...  (u2,pw_bad)
          │
     LoginSucceeds
          │
    session=[u1,pw1]
    currentPage="/my-tests"
          │
        Logout / NavigateTo / ...

TLC는 이 그래프를 완전히 탐색하고, 모든 노드에서 Invariant를 체크한다. 위반 발견 시 Init → 위반 상태까지의 경로를 반례로 출력.

---

## 참고

- `specs/auth/Auth.tla` — 인증 상태머신 명세
- `specs/auth/MCAuth.tla` — TLC 모델체킹 래퍼
- `specs/auth/MCAuth.cfg` — TLC 설정 파일
- `specs/auth/Common.tla` — 공유 타입 정의
- Leslie Lamport, "Specifying Systems" — 공식 TLA+ 교재
- https://learntla.com — 실무 관점 TLA+ 입문
