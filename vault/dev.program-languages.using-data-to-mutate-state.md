---
id: pwsz57kf3xjhcyahb2ztqnt
title: Data as a mediator between computation and state
desc: ""
updated: 1780034752626
created: 1780034524057
---

[원 글](https://www.tedinski.com/2018/08/28/using-data-to-mutate-state.html)을 읽고 sonnet과 문답 정리

# 액션을 데이터 타입으로 표현하는 설계 기법

## 1. 핵심 문제: OO와 멀티 오브젝트 시스템

OO(객체지향)는 단일 객체의 상태를 캡슐화하는 데는 강하지만, **여러 객체를 동시에 변경해야 하는 상황**에서 설계가 어색해진다. OO 이데올로기가 "데이터 타입으로 생각하기"를 억제하기 때문에, 멀티 오브젝트 시스템에서 설계 선택지가 좁아진다.

---

## 2. 제안하는 해결책: 액션을 데이터로 표현

함수가 직접 상태를 바꾸는 대신, **"무엇을 해야 하는지"를 기술하는 데이터**를 반환하게 하고, 실제 실행은 별도의 **인터프리터**가 담당하게 한다.

```
기존 방식:  함수 → 직접 상태 변경
제안 방식:  함수 → 액션 기술(data) → 인터프리터 → 상태 변경
```

### 코드 예시

```javascript
// 기존: 함수가 직접 상태를 변경
function transfer(from, to, amount) {
  from.balance -= amount // 직접 변경
  to.balance += amount // 직접 변경
}

// 제안: 함수가 "설명 데이터"를 반환
function transfer(from, to, amount) {
  return [
    { type: "DEBIT", accountId: from.id, amount },
    { type: "CREDIT", accountId: to.id, amount },
  ]
}

// 인터프리터가 실제 변경을 담당
function interpret(actions) {
  for (const action of actions) {
    if (action.type === "DEBIT") db.update(action.accountId, -action.amount)
    if (action.type === "CREDIT") db.update(action.accountId, +action.amount)
  }
}
```

이 패턴은 함수형 프로그래밍의 **Command 패턴**, Haskell의 **IO 모나드**, Redux의 **Action/Reducer** 구조와 맥락이 같다.

---

## 3. 4가지 장점

1. **테스트가 쉬워진다** — 함수가 상태를 직접 바꾸지 않고 데이터를 반환하므로, 복잡한 상태 셋업 없이 출력값만 검사하면 된다. 사실상 순수 함수처럼 테스트할 수 있다.

2. **불변식(invariant) 보장이 쉬워진다** — 실제 상태 변경은 인터프리터 한 곳에서만 일어나므로, 시스템 전체 규칙을 한 곳에서만 강제하면 된다.

3. **인터프리터 자체도 테스트하기 쉬워진다** — 가장 위험한 코드(실제 멀티 오브젝트 변경)가 한 곳에 모여 있으므로 집중적으로 테스트할 수 있다.

4. **디커플링(decoupling)이 강화된다** — 액션을 생성하는 코드와 실제 시스템이 분리되어 있으므로, 나중에 시스템 구조를 바꿔도 액션 생성 로직은 건드리지 않아도 된다.

There are of course, several disadvantages:

1. Many of our programming languages lack good support for representing data (in particular, algebraic data types), making it overly verbose to create such a data type, and so more more costly and difficult than it should be.
2. Designing the intermediate data type describing actions can be hard. Non-trivial data types can become akin to miniature programming languages (hence my choice of the term “interpreter”), and keeping the abstractions sensible is tricky.

---

## 4. Q&A: 인터프리터 vs 각 객체의 public method

### Q. 각 객체의 public method를 사용하는 것이 더 견고하지 않나?

**두 가지를 구분해야 한다.**

- **각 객체의 public method**: 그 객체 자신의 불변식(예: 잔고 음수 방지)을 보장한다.
- **인터프리터**: 여러 객체에 걸친 시스템 수준의 불변식(예: debit과 credit의 원자성)을 보장한다.

| 불변식                                          | 담당자                       |
| ----------------------------------------------- | ---------------------------- |
| 잔고가 음수가 되면 안 된다                      | Account 객체의 public method |
| debit과 credit은 반드시 함께 성공/실패해야 한다 | 인터프리터                   |

**둘은 경쟁 관계가 아니라 상호 보완 관계다.** 인터프리터 내부에서 각 객체의 public method를 호출하는 방식으로 조합할 수 있다.

```javascript
function interpret(actions) {
  beginTransaction()
  try {
    for (const action of actions) {
      // 객체 자신의 불변식은 객체가 보장
      accounts.get(action.id).debit(action.amount)
    }
    commit()
  } catch {
    rollback() // 멀티 객체 원자성은 인터프리터가 보장
  }
}
```

OO의 캡슐화는 객체 내부를 보호하는 데 탁월하지만, **객체 간 조율이 필요한 불변식**은 애초에 어느 객체의 책임도 아니다. 인터프리터는 그 공백을 메운다.

---

## 5. 인터프리터와 프로퍼티 테스팅의 시너지

액션이 데이터로 표현되기 때문에, **랜덤한 액션 시퀀스를 자동 생성하기 쉽다.**

### 전략 1: 모델 기반 검증 (Model-based Testing)

실제 시스템과 동작이 동일해야 하는 단순화된 모델을 만들어 둘의 결과를 비교한다.

```
랜덤 액션 시퀀스
    ↓              ↓
실제 인터프리터   단순 모델(예: Map으로 구현한 가짜 DB)
    ↓              ↓
결과 A    ==?    결과 B
```

### 전략 2: 불변식 검사와의 시너지

랜덤 액션을 실행한 후 시스템 불변식이 깨지지 않았는지 확인하는 것만으로도 강력한 테스트가 된다.

```
랜덤 액션 시퀀스 실행
    ↓
불변식 체크:
  - 모든 잔고의 합이 일정한가?
  - 음수 잔고가 존재하지 않는가?
  - 트랜잭션이 원자적으로 처리되었는가?
```

개발자가 미처 생각하지 못한 엣지 케이스 조합을 자동으로 발견해준다.

### 시너지의 이유

- 액션이 데이터라서 → 랜덤 생성이 쉽고
- 변경이 인터프리터에 집중되어 있어서 → 불변식 검사 지점이 명확하고
- 인터프리터가 격리되어 있어서 → 테스트 설정이 단순하다

세 가지가 맞물려 단순히 "테스트하기 편하다" 수준을 넘어, **버그를 자동으로 찾아내는 테스트 체계**를 구축하기 훨씬 수월해진다.

---

## 한 줄 요약

> **"상태를 바꾸는 코드"와 "무엇을 바꿀지 결정하는 코드"를 분리하면, 복잡한 멀티 오브젝트 시스템도 테스트 가능하고 안전하게 관리할 수 있다.**
