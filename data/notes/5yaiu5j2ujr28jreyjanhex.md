
## 불변식 (Safety Invariants)

"어떤 상태에서도 항상 참이어야 한다" — TLC가 도달 가능한 모든 상태를 탐색하며 위반 즉시 반례를 출력.

## 활성도 (Liveness Property)

"결국에는 반드시 일어나야 한다" — Safety와 달리 시간 축을 따라 검증. TLA+에서 ~> (leads-to) 연산자로 표현.

---

PendingLoginEventuallyResolves

PendingLoginEventuallyResolves ==
(pendingLogin /= NULL) ~> (pendingLogin = NULL)

"로그인 시도가 걸려있으면, 언젠가는 반드시 해소된다"

~> 의미: pendingLogin /= NULL인 상태에 도달하면, 그 이후 어떤 경로를 따르더라도 결국  
 pendingLogin = NULL이 되는 상태에 도달해야 함.

이 성질이 보장되려면 Next 액션 중 LoginSucceeds 또는 LoginFails가 반드시 실행 가능해야 한다.  
 그래서 Spec에 약한 공정성(Weak Fairness) 조건이 붙어 있음:

Spec == Init /\ [][Next]\_authVars  
 /\ WF_authVars(LoginSucceeds)
/\ WF_authVars(LoginFails)

WF_authVars(A): 액션 A가 무한히 오래 실행 가능한 상태로 있다면, 언젠가는 반드시 실행된다. 이 보장이 없으면 시스템이 영원히 pendingLogin /= NULL 상태에 머물러도 명세 위반이 아니게 됨 — **starvation** 허용.

## cfg 파일을 따로 만드는 이유?

명세(spec)와 모델(model)을 분리하기 위해서

tla는 수학적 명세, cfg는 "이번 실행에서 뭘 어떻게 검사할지" 설정

### .tla vs .cfg 역할

|            | .tla                            | .cfg                                   |
| ---------- | ------------------------------- | -------------------------------------- |
| **역할**   | 무엇이 참인가 (논리)            | 무엇을 검사할 것인가 (실행 설정)       |
| **내용**   | 상태, 전이, 불변식 정의         | 상수값, 검사할 invariant/property 지정 |
| **재사용** | 여러 cfg가 같은 tla를 공유 가능 | tla마다 또는 시나리오마다 별도         |

### 실용적 이점

같은 명세를 다른 조건으로 검사할 수 있다.

예시: Auth.tla 하나에 cfg를 여러 개 만드는 것이 가능:

- MCAuth_small.cfg # Users={u1}, Passwords={pw1, pw_bad} — 빠른 검사
- MCAuth_full.cfg # Users={u1,u2,u3}, Passwords={...} — 더 넓은 탐색
- MCAuth_noWF.cfg # WF 조건 없이 liveness만 빼고 safety만 검사

tla를 수정하지 않고 cfg만 바꿔서 탐색 범위나 검사 대상을 조절.

### TLC 실행 모델

TLC는 .tla 파일을 읽어 상태공간을 만들고, .cfg에 적힌 것만 검사한다. .tla 안에 불변식이 아무리
많아도 .cfg의 INVARIANTS 목록에 없으면 검사 안 함 — 이것도 분리의 이유 중 하나.
