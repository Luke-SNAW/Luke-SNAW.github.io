---
id: p9blko4uudehmdutpacd2jh
title: 자바스크립트는 왜 프로토타입을 선택했을까
desc: ""
updated: 1725870336145
created: 1725869837002
published: false
---

> https://medium.com/@limsungmook/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%99%9C-%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85%EC%9D%84-%EC%84%A0%ED%83%9D%ED%96%88%EC%9D%84%EA%B9%8C-997f985adb42

프로토타입으로 검색하면 으레 나오는 서두처럼 저 또한 자바스크립트를 처음 접했을 때 가장 당황스러웠던 게 프로토타입이었습니다.

저는 여러 서적과 정리된 글을 본 뒤 정답이라곤 볼 수 없는 결론을 얻게 되었습니다.

“프로토타입은 자바스크립트에서 상속을 지원하기 위한 방법이다.”

여기엔 여러 가지 해소되지 않는 질문이 있습니다. ‘왜 다른 언어처럼 클래스가 아니라 프로토타입인가?’, ‘프로토타입은 어디서 나온 용어인가?’. 이 질문의 답은 쉽게 접할 수 있는 자료에선 찾을 수 없었습니다. (여기서 쉽게 접할 수 있는 자료란 서점에서 구매할 수 있는 책과 구글링 1~3페이지 내에 나오는 아티클을 뜻합니다)

프로토타입 외에도 당황스러웠던, 그리고 어려웠던 부분은 호이스팅과 this였습니다. 이것은 철저히 암기과목이었습니다. 대부분의 자료는 자바스크립트에서 구현해놓은 스펙과 현상만을 설명했습니다. 고통스러운 암기 시간이었습니다. 이 또한 ‘왜 자바스크립트만 이렇게 특이하게 처리하지?’ 에 대해 명쾌하게 답해주는 자료를 찾을 수 없었습니다. 외우는 수밖에 없었습니다.

“호이스팅은 자바스크립트에서 전체 코드를 훑을 때 선언 부를 상단으로 올린다.”

“this 는 기본적으로 global(브라우져에선 window)을 가리키고 실행 컨텍스트마다 달라질 수 있으니 bind 등을 통해 제어해야 한다.”

모두가 똑같이 얘기하고 있습니다. FE 개발자 면접 시 단골 질문이고, 우리 회사에서도 꼭 하는 질문인데 대부분의 지원자가 똑같은 대답을 하고 있습니다.

개인적으로 어떤 기술에 대해 ‘왜’를 알아야만 해당 기술에 애착이 생기는 편입니다. 오랜 시간 주 언어가 자바였던 제가 FE 개발로 직군 변경하게 되면서 필연으로 자바스크립트를 이해할 필요가 있었고, 이러한 이유로 ‘왜' 에 대해 집중적으로 연구하다가 아주 흥미로운 논문을 발견했습니다. [Classes vs. Prototypes Some Philosophical and Historical Observations](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.56.4713&rep=rep1&type=pdf) 라는 1996년에 작성된 논문인데요, 여기에 제가 궁금했던 ‘왜' 에 대한 내용이 담겨 있었습니다.

이 글은 위 논문을 토대로 제가 이해한 내용을 적은 글입니다. 내용 흐름과 핵심 내용은 유사합니다. 하지만 저 당시와 상황이 많이 달라지기도 했고(논문에 언급된 프로토타입 기반 언어는 모두 역사 속으로….), 함축적인 내용이 많아 나름대로 추가 연구하면서 알게 된 많은 내용을 덧붙여봤습니다.

앞으로 전개될 글 내용을 미리 요약하면, 프로토타입 기반 OOP는 class 기반의 OOP 와 완전히 상반되는 방식입니다. 객체를 바라보는 개념 자체가 완전히 다릅니다. 특히 문맥(context)을 매우 강조하는 철학적 근거에서 태어난 녀석이라 렉시컬 스코프에 의한 호이스팅과 실행 문맥에 의한 복잡한 this가 필연적으로 발생할 수밖에 없었습니다.

이 글을 통해 저처럼 혼란을 느끼는 분들도 프로토타입의 ‘why’를 깊이 이해할 수 있기를, 더 나아가 호이스팅과 this에 대해서도 보다 근원적인 이해를 할 수 있기를 기대합니다.

## 플라톤과 이데아, 그리고 클래스 기반 객체지향프로그래밍

> 서양 철학은 플라톤의 각주에 불과하다 — 화이트헤드

프로토타입을 이해하려면 그 대척점에 있는 클래스의 기원을 알아야 합니다. 클래스 기반 객체지향 언어(Java, C# 등)를 오랫동안 해왔다면 이미 알고 있는 내용일 수 있습니다. 그렇다면 바로 프로토타입으로 넘어가셔도 좋습니다. (그래도 한번 읽어보시는 걸 추천합니다)

서양철학은 이분법적 세계관을 갖고 있습니다.

- 영혼 / 육체
- 추상적 / 구체적
- 이데아 / 프랙티스

눈앞에 실제로, 구체적으로 존재하는 사물이 있다면 반드시 그것의 본질이 존재한다는 것이 플라톤의 주장입니다.

의자를 예로 들어보면 우리가 앉아있는 의자는 여러 가지 형태가 존재합니다. 원목 의자, 바퀴 달린 의자, 하이 체어 등등. 이러한 수많은 의자가 실제로 존재한다면 반드시 그 본질적이고 추상적인 ‘의자’라는 것이 존재한다는 것이지요. 이러한 본질 세계를 이데아(Idea) 라고 합니다. 현실의 의자는 모두 이데아의 ‘의자'를 모방한 의자라는 것이지요.

영어권의 사고방식에는 이러한 이분법적 세계관이 기본입니다. 학창 시절부터 성인이 될 때까지 쭉 어려웠던 “관사"를 보면 확실하게 알 수 있습니다. 영어에서는 이데아의 세계에 있는 것을 지칭할 때 “추상적인 존재”를 표현하는 방법이 있습니다. 추상적인 의자를 얘기할 때 그냥 ‘chair’라고 얘기하는 것이 그 방법입니다. 그럼 현실에 존재하는 의자를 가리킬 땐 어떻게 할까요? 현실의 존재를 얘기할 땐 단어 그대로 얘기하지 못합니다. 반드시 “때”가 묻어있어야 합니다. 그래서 ‘a chair’라고 얘기해야 합니다. (“[한마디로 영어](https://hanmadiro.com/)” 강의를 통해 배운 내용입니다)

- chair : 이데아에 존재하는 본질적인, 추상적인 의자. 현실세계에 존재하지 않는다
- a chair, the chair, chairs : 현실 세계에 존재하는 의자

이러한 사고방식이 프로그래밍 언어에도 자연스럽게 녹아들어 생긴 언어가 “클래스 기반 객체지향 프로그래밍 언어”입니다. 대표적으로 Java, C# 이 있습니다.

Java에서의 예를 볼까요?

```java
class Chair {
...
}
Chair myChair = new Chair();
```

위 코드에서 레퍼런스 타입이라 불리는 Chair 클래스는 이데아에 존재하는 추상적인 개념입니다. 즉, 코드상으로만 존재하지 실제 메모리상에는 존재하지 않습니다. (디테일하게 들어가면 PermGen 영역에 있겠지만 여기서는 Heap 메모리만 실존하는 공간으로 보겠습니다)

그럼 현실세계에 존재하게 하려면 어떻게 해야 할까요? 바로 new 키워드를 사용하면 됩니다. new Chair() 를 하는 순간 추상적으로만 존재하던 의자가 메모리라는 현실세계에 구체적으로 존재(인스턴스화)하게 됩니다.

이러한 클래스 방식의 OOP 언어는 플라톤류(Platonic) 서양철학의 자연스러운 흐름입니다.

## 분류(Classification)

이러한 플라톤의 이데아 이론은 그의 제자 아리스토텔레스에 의해서 ‘분류(classification)'란 개념으로 정립됩니다. class 라는 키워드가 어디서 나온 지 알 수 있겠죠? 아리스토텔레스는 아래와 같이 분류를 정리했습니다.

- `개체의 속성이 동일한 경우` 개체 그룹이 같은 범주에 속한다. 범주는 정의와 구별의 합이다

이는 전통적인 클래스 기반 객체 지향 프로그래밍의 아이디어-일반화(generalization)와 정확히 일치합니다. 여기서 속성은 클래스의 프로퍼티가 되겠죠. 프로퍼티가 유사한 객체가 있다면 일반화 과정을 통해 클래스로 추상화됩니다.

실제로 아리스토텔레스는 이러한 기준으로 현실 세계의 많은 것들을 분류했고, 최초로 동물을 분류한 사람이 되었습니다. 속성에 따른 분류로 인해 돌고래는 어류가 아닌 포유류가 되었죠. (학창 시절 저는 이게 너무 헷갈렸습니다. ㅠㅠ)

## 프로토타입(Prototype)

> _서양 철학은 플라톤의 각주에 불과하다 — 화이트헤드_
>
> _하지만 이 말에는 ‘비트겐슈타인 이전까지’라는 단서를 덧붙여야 한다 — 와스피 히잡_

드디어 프로토타입 얘기를 시작합니다. 프로토타입을 이해하기 위해선 분류(Classification)에 대해 반드시 알아야 할 필요가 있기 때문에 긴 지면을 할애해 설명했습니다. 왜냐하면 프로토타입이란 개념이 이 분류(Classification)이론을 정면으로 반박하여 나온 이론이기 때문입니다.

19세기 매우 유명한 철학자 비트겐슈타인은 아리스토텔레스의 분류 개념을 정면으로 반박합니다

> 공유 속성의 관점에서 정의하기 어려운 개념이 있다(사실상 올바른 분류란 없다) — 비트겐슈타인

이 얘기를 하면서 근거로 들고 온 것은 바로 게임입니다. 게임은 일반적으로 승리와 패배가 명확합니다. 즉 ‘승리'와 ‘패배'라는 속성이 있다고 볼 수 있죠. 하지만 비트겐슈타인은 이에 대한 반론으로 ‘승리', ‘패배'가 없는 \`ring around a rosy\`를 들고옵니다. (한국에서 자란 저는 이 게임이 뭔지 잘 모르겠습니다; 승자가 없는 게임이라고 합니다)

이 게임은 빙글빙글 돌다가 다같이 주저앉는 게임입니다. 누구도 승리, 패배하지 않는 게임이죠.

이처럼 게임에는 공유 속성이 없습니다.

- 승리 / 패배? ring around a rosy 게임엔 없잖아
- 숙련도 여부? 행운(주사위) 위주 게임은 없잖아
- 플레이어 존재여부? 플레이어가 전혀 필요하지 않는 게임도 있잖아

특히 게임 외에도 예술작품의 경우 공통 속성을 정의할 수 없습니다. 즉, 좀 더 철학적으로 본다면 ‘게임', ‘예술' 등의 단어는 결코 속성으로 규정할 수 없지요.

> 세계에 미리 내재되어서 대상과 언어를 완전히 규정하는 어떤 언어란 존재하지 않는다 — 비트겐슈타인

저는 Java로 개발하는 동안 이러한 본질적인 한계를 자주 느꼈습니다. 최적의 클래스 설계를 찾는 것이 너무 어려웠습니다. 속성(property)으로 분류하는 것은 확장성을 고려하면 좋은 방식이 아니었습니다. 정답이라 생각했던 설계도 개발이 진행되면서 뒤엎는 경우가 많았습니다. 멋들어진 상속 관계는 결국 거대한 기술부채가 되는 경우가 왕왕 있었습니다. 경력이 쌓이고 나서야 도메인 기반 설계, SOLID, 디자인 패턴 등을 통해 그럴싸한 클래스를 설계할 수 있게 되었지만 이러한 것을 숙달하기까진 오랜 시간과 시행착오가 필요했습니다. 그리고 이 또한 한 번에 완벽한 디자인이 나오는 것은 불가능하다고 생각합니다. 클래스는 너무 어렵습니다.

이러한 분류(Classification)에 대해 강하게 비판한 비트겐슈타인, 그렇다면 그의 대안은 무엇이었을까요? 비트겐슈타인은 다음의 유명한 말을 남깁니다.

> 표현은 삶의 흐름 속에서만 의미를 갖는다 — 비트겐슈타인

마음에 울림이 있는 문구입니다. 이 내용을 좀 더 살펴보겠습니다.

## 의미사용이론(the use theory of meaning)

비트겐슈타인 일생의 후기에 내놓은 이론입니다. 사용(use)에 의해 의미(meaning)가 결정된다는 이론입니다. 단어의 쓰임새가 곧 의미가 됩니다. 즉, 단어의 ‘진정한 본래의 의미'란 존재하지 않고 ‘상황과 맥락에 의해서 결정된다'라고 주장하고 있습니다. 그러니 단어의 의미를 백날 분석해봤자 소용이 없다는 것입니다.

비트겐슈타인은 ‘벽돌'을 예로 들었습니다. 누군가 벽돌! 이라 외쳤을 때 상황마다 그 의미는 달라집니다

- (벽돌이 필요할 때) : 벽돌을 달라
- (벽돌로 보수해야 할 때) : 벽돌을 채우라
- (벽돌이 떨어질 때) : 벽돌을 피해라

위 내용이 어렵다면 맥락(Context)이 중요하다는 것만 기억하시면 됩니다. 이 컨텍스트로 프로토타입 기반 언어의 실행 컨텍스트를 설명할 수 있습니다. (자세한 건 뒤에)

## 가족 유사성(Family Resemblance)

비트겐슈타인은 위에서 설명한 의미사용이론과 또 하나의 이론을 주장합니다. 바로 가족 유사성입니다.

[image - 가족 유사성](https://miro.medium.com/v2/resize:fit:637/1*M8Z3pB6HloC2pM8UJIOjtA.png)

출처 : [https://www.slideshare.net/vcmlab/cog5-lecppt-chapter08](https://www.slideshare.net/vcmlab/cog5-lecppt-chapter08)

비트겐슈타인은 인간이 현실에서 실제로 대상을 분류할 때 속성(전통적인 분류에서의 기준)이 아닌 가족 유사성을 통해 분류하게 된다고 얘기합니다.

위 그림처럼 가족이 있을 때 이 가족이 모두 공유하는 공통 속성은 없습니다. 갈색 머리, 안경, 수염, 큰 코가 가족의 전형적인 특징이라고 하더라도 모든 가족 구성원에게 적용되는 공통된 특성(속성)은 없을 수 있습니다. 그런데도 우리는 이 그림을 보고 전형적인 특징을 통해 ‘가족'으로 분류합니다. 이런 분류 방식을 ‘가족 유사성' 에 의한 분류라고 합니다.

이 이론은 프로토타입 이론의 근거가 됩니다.

## Rosch 의 프로토타입 이론

드디어 이론의 마지막 장에 도달했습니다. 아주 익숙한 단어가 나옵니다 ‘프로토타입'. 네 맞습니다. 이 프로토타입이 바로 Javascript에서 사용하는 프로토타입입니다.

비트겐슈타인의 의미사용이론, 가족 유사성은 1970년경 철학자 Eleanor Rosch 에 의해 `프로토타입 이론(Prototype theory)`으로 정리됩니다.

1975년에 Rosch 는 한 가지 실험을 합니다.

- 실험 참가자들에게 여러 범주 구성원(사과, 코코넛, 오렌지)의 속성을 적어보라고 함
- 각 범주 구성원에 대해 범주의 다른 구성원과 공유하는 속성의 개수를 도출함
- 사과, 오렌지 : 2점(둥글다. 즙이 있다.)
- 코코넛 : 1점(둥글다)

점수가 높을수록 ‘가족 유사성'이 높다고 볼 수 있습니다. 전통적인 분류에선 모두 과일로 볼 수 있지만, 프로토타입 이론에서는 사과와 오렌지가 가장 전형적인 무언가라고 볼 수 있습니다. 반면에 코코넛은 저 중에서 가장 비전형적인 것으로 볼 수 있습니다.

이 실험을 통해 로쉬는 “인간은 ‘등급이 매겨진 (개념) 구조(graded structure)’를 가진다”라고 주장합니다. 인간은 사물을 분류할 때 자연스럽게 가장 유사성 높은 것 순서대로 등급을 매긴다는 의미로 볼 수 있습니다. 이렇게 분류했을 때 가장 높은 등급을 가진 녀석이 나올 텐데요, 이것이 바로 원형(Prototype)이다. 란 주장이 프로토타입 이론입니다.

‘새'를 예로 들어볼까요?

‘참새'는 새의 범주를 대표할 만한 가장 전형적인 녀석입니다. 이 녀석을 ‘원형(prototype)'으로 간주하겠습니다.

[image - birdness rankings](https://miro.medium.com/v2/resize:fit:700/1*ThdtLo8MUCQ2bcfII6AJcQ.png)

출처 : [https://laurabecker.gitlab.io/classes/as/08-semantics.pdf](https://laurabecker.gitlab.io/classes/as/08-semantics.pdf)

‘타조'는 전통적인 분류에선 같은 새가 되지만 프로토타입 이론에서는 ‘원형'에서 가장 멀리 떨어진, 즉 ‘비전형적인' 녀석이 됩니다. 범주의 가장 끄트머리에 있는 녀석이 되는 거죠.

즉, 객체는 ‘정의’로부터 분류되는 것이 아니라 가장 좋은 보기(prototype, exemplar)로부터 범주화된다고 합니다.

이러한 분류 체계는 매우 경제적입니다. 만약 우리가 새로운 대상을 접해서 분류해야 할 때, 우리는 새로운 대상의 몇 가지 특징만 원형(prototype)과 비교확인만 하면 됩니다. 특징이 다를수록 원형에서 멀~리 떨어진 범주가 되는 거죠.

이 이론에 또 한 가지 중요한 것이 있습니다.

같은 단어라 할지라도 누가 어떤 상황(context)에서 접했나에 따라 의미가 달라진다는 것입니다. (의미사용이론)

예를 들면 아이가 생각하는 새의 범주에서 ‘참새’는 명확하게 새에 속하지만 ‘펭귄' 은 해당 범주에 속하지 못할 수도 있습니다. 아이가 생각할 땐 펭귄이 매우 비전형적이기 때문이죠. 하지만 조류학자가 생각할 때 ‘참새'와 ‘펭귄'은 명확하게 유사한 새의 범주에 속할 수 있습니다. 같은 단어여도 어떤 상황(누가, 어디서…)에서 접했나에 따라 범주는 크게 달라집니다.

와! 정말 어렵네요. 그래도 여기까지 모두 이해하셨다면 앞으로는 꽃길만 걸을 수 있습니다. 이해가 안 되셨다면 다음 두 가지만 기억하셔도 될 것 같습니다.

- 현실에 존재하는 것 중 가장 좋은 본보기를 원형(prototype)으로 선택한다.
- 문맥(컨텍스트)에 따라 ‘범주’, 즉 ‘의미’가 달라진다.

## 프로토타입 기반 객체지향 프로그래밍

이러한 프로토타입 이론은 그대로 프로토타입 기반 객체지향 프로그래밍 언어를 통해 구현되었습니다. 1980~90년대에 이 이론을 토대로 많은 프로토타입 기반 언어가 생겨났습니다. 대표적으로 Javascript의 모태인 Self 언어(Self 에서 로쉬의 프로토타입을 참고한 부분은 [Prototype Based Programming 문서](https://expertiza.csc.ncsu.edu/index.php/CSC/ECE_517_Fall_2010/ch4_4e_ms) 참고)와, 가족유사성(Family Resemblance)을 언어 차원에서 완벽하게 구현한 Kevo 가 있습니다.

프로토타입 기반 OOP 언어의 특징은 다음과 같습니다.

- 개별 객체(instance) 수준에서 메소드와 변수를 추가
- 객체 생성은 일반적으로 복사를 통해 이루어짐
- 확장(extends)은 클래스가 아니라 위임(delegation)  
   \> 현재 객체가 메시지에 반응하지 못할 때 다른 객체로 메시지를 전달할 수 있게 하여 상속의 본질을 지원
- 개별 객체 수준에서 객체를 수정하고 발전시키는 능력은 **선험적 분류의 필요성을 줄이고 반복적인 프로그래밍 및 디자인 스타일**을 장려
- 프로토타입 프로그래밍은 일반적으로 `분류하지 않고 유사성을 활용하도록 선택`
- 결과적으로 설계는 맥락에 의해 평가

Javascript 에 익숙하다면 별다른 설명 없이도 이해되는 부분이 있을 것으로 보입니다.

다시 한번 가장 중요하다 생각되는 부분을 정리해보면

- 프로토타입 언어에서는 ‘분류’를 우선하지 않는다. 생성된 객체 위주로 유사성을 정의한다.
- 어휘, 쓰임새는 맥락(context)에 의해 평가된다.  
   \> 실행 컨텍스트, 스코프 체인이 여기서 파생되었습니다  
   \> 클로져, this, 호이스팅 등등. 이 모든 헬(?) 이 프로토타입의 ‘맥락’을 표현하기 위한 것입니다.

이 내용을 대표적인 프로토타입 기반 언어인 Javascript 를 통해 예제와 함께 살펴보겠습니다.

## 자바스크립트 — 프로토타입

드디어 코드가 나왔습니다!

```js
function 참새() {
  this.날개갯수 = 2
  this.날수있나 = true
}
const 참새1 = new 참새()

console.log("참새의 날개 갯수 : ", 참새1.날개갯수) // 2

function 닭() {
  this.벼슬 = true
}
닭.prototype = 참새1 // reference(오른쪽이 인스턴스인 점 주목)
const 닭1 = new 닭()
console.log("닭1 날개 : ", 닭1.날개갯수, ", 날수있나? ", 닭1.날수있나) // 2, true
닭1.날수있나 = false
console.log("다시 물어본다. 닭1은 날 수 있나? :", 닭1.날수있나) // false
// 아래는 고전적인 방식의 프로토타입 연결
function 펭귄() {
  참새.call(this) // copy properties
}
펭귄.prototype = Object.create(참새.prototype) // 프로토타입 연결
const 펭귄1 = new 펭귄()
console.log("펭귄1 날개 : ", 펭귄1.날개갯수, ", 날수있나? ", 펭귄1.날수있나) // 2, true
펭귄1.날수있나 = false
console.log("다시 물어본다. 펭귄1은 날 수 있나? :", 펭귄1.날수있나) // false
```

- 5L : 날개가 2개, 날 수 있는 참새1 이 있습니다.
- 13L : 참새1 을 프로토타입으로 갖는 닭1 이 생겼습니다. 여기서 주목할 점은 오른쪽이 참새(함수)가 아니라 참새1(인스턴스) 인 점입니다. 프로토타입 이론은 이미 존재하는 사물을 통해 범주화한다는 점에서 일치합니다
- 14L : 닭의 정의(10L)에는 날개갯수가 없지만 2가 출력됩니다. 프로토타입 체인에 의해 참새1 의 속성에 접근했기 때문입니다.
- 15L : 닭1 은 날 수 없다고 합니다. 닭1은 날 수 없어도 프로토타입에 해당하는 참새1 은 날 수 있습니다. (닭1은 참새1프로토타입에서 좀더 멀어졌습니다) 같은 속성을 변경해도 프로토타입 객체의 속성은 변경되지 않은 점에 주의
- 17L~25L : 고전적인 방식으로 프로토타입을 사용해봤습니다. 프로토타입에선 객체 생성을 통해 확장한다는 부분이 좀더 직관적으로 다가옵니다.

위 코드는 아래처럼 도식화할 수 있습니다.

![](https://miro.medium.com/v2/resize:fit:700/1*EPvcWtTdkrM_vZHDwNNMJg.png)

- 닭1 의 원형(프로토타입)은 참새1이다
- 닭1에 없는 속성(날개갯수)은 프로토타입 체인을 통해 참조된다
- 닭1에 동일한 속성명(날수있나)을 추가해도 원형은 변하지 않는다(위임)  
   \> 원리적으로는 닭1을 통해 원형(prototype)을 변경하는건 불가능해야 한다. 하지만 JS 에선 문법적으로 가능. (권장하지 않음)

## 자바스크립트 — 어휘적 범위(lexical scope)

의미사용이론에 따르면 단어의 의미는 그 어휘적인, 근처 환경에서의 의미가 됩니다. 이는 Javascript에 다음처럼 적용됩니다

> 변수의 의미는 그 **어휘적인(Lexical)**, **실행 문맥(Execution Context)**에서의 의미가 된다

그렇기 때문에 동일 범위(실행 문맥)의 모든 `선언`을 참고(호이스팅)해 의미를 정의합니다.

호이스팅은 자바스크립트에서 악명 높기로 유명한 특징들 중 하나입니다. 면접 단골 질문이기도 하죠. 저도 면접자들에게 종종 물어보는데 대부분 ‘코드가 로드될 때 선언 부가 끌어올려지는' 정도로 대답을 합니다. 틀린 대답은 아니지만 조금 아쉽습니다. (참고로 지금까지 가장 훌륭한 대답은 ‘실행 컨텍스트 생성 시 렉시컬 스코프 내의 선언이 끌어올려 지는 게 호이스팅이다'란 대답이었습니다)

프로토타입 기반 언어인 자바스크립트에서는 ‘단어의 의미가 사용되는 근처 환경’ 에서의 ‘근처'를 어휘적인 범위(Lexical Scope)로 정의했습니다. 자바스크립트 엔진은 코드가 로드될 때 실행 컨텍스트를 생성하고 그 안에 선언된 변수, 함수를 실행 컨텍스트 최상단으로 호이스팅 합니다. 이러한 범위를 렉시컬 스코프라 합니다.

예제 코드를 준비해봤습니다. 주석을 참고하면서 천천히 흐름을 따라가면 좋을 것 같습니다.

```js
// 전역 실행문맥 생성. 전체 정의(name, init) 호이스팅
var name = "Kai"
init() // init 실행문맥 생성. 내부 정의(name, displayName) 호이스팅
function init() {
  var name = "Steve"
  function displayName() {
    console.log(name) // 현재 실행문맥 내에 정의된게 없으니 outer 로 chain
    // var name = 'troll?'; // 주석 해제되면 호이스팅
  }
  displayName() // displayName 실행문맥 생성. 내부 정의 호이스팅.
}
```

- 2L : 코드가 로드될 때 전역 실행문맥(Execution Scope) 이 생성됩니다. 전역의 선언부를 모두 호이스팅 하게 되는데 여기선 2L 의 name 과 4L의 init 이 렉시컬 스코프에 들어갑니다.
- 3L : 렉시컬 스코프 상에 4L 의 init 함수가 존재하니 에러 없이 실행할 수 있습니다. 코드 로딩 시점에 init 함수를 타고 들어가 실행 문맥을 생성합니다
- 4L : init 함수에 대한 렉시컬 스코프를 생성합니다. name 과 displayName 이 들어옵니다
- 6L-9L : displayName 실행 문맥 내에 name 이라 선언된 것이 없습니다. 이럴땐 Scope Chain 을 통해 상위 실행컨텍스트로 위임합니다.

코드를 로드하게 되면 아래와 같은 구조가 생성됩니다.

\- Global Execution // 1

- Lexical : name, init  
  \- Execution : init // 2
- Lexical : name, displayName
- Outer : global  
  \- Execution : displayName // 3
- Lexical : null
- Outer : init

대략 아래와 같은 그림으로 이해하시면 될 것 같습니다. 가장 바깥 원에서부터 안쪽 원으로 Scope Chain 을 하게 됩니다. 위에서 봤던 로쉬의 프로토타입 모델과 비슷하죠? 자바스크립트에서의 스코프 체인, 프로토타입 체인 모두 이 그림으로 표현됩니다.

![](https://miro.medium.com/v2/resize:fit:700/1*0qa5p_SprK0BE20fhHWpAQ.png)

여기서 중요한 것은 자바스크립트의 동작 방식보다는, 프로토타입 언어인 자바스크립트에 **도대체 왜 ‘실행 문맥', ‘렉시컬 스코프', ‘호이스팅'이 존재하는가** 입니다. ‘왜'를 이해했다면 이 부분은 더는 암기과목이 아닙니다. 프로토타입 철학의 근원인 비트겐슈타인류에서 가장 중요하게 생각하는 것이 바로 ‘어휘'이고 이것은 ‘문맥(context)’ 내에서만 의미를 가진다는 것이 핵심입니다. 이 핵심을 자바스크립트에서 구현하기 위해 자연스럽게 발생한 특징임을 이해한다면 더 이상 외울 필요가 없어집니다.

## 자바스크립트 — **this**

자바스크립트에 또 다른 악명으로 유명한 특징은 바로 this 입니다. 클래스 기반 객체지향 언어에서의 this 와 완전히 다른 동작을 하므로 대부분의 자바스크립트 초심자가 머리 싸매고 넘어가는게 바로 요 this 입니다. 면접에서도 단골 주제죠. 자바를 오래 했던 저는 자바스크립트를 접하며 이 this 가 가장 이상하고 이해가 안 됐습니다.

재미있는 건 서적이나 인터넷을 아무리 뒤져봐도 자바스크립트에서 this 가 이 모양이 된 이유를 설명해주는 글을 찾지 못했다는 점입니다. 꽤 영향력 있는 인물도 잘못 알고 있는 경우가 있었습니다. 잘 작성된 기술 문서도 대부분 Case by case 로 this 가 가리키는 객체를 설명하는 방식이었습니다. 개인적으로 이런 식의 학습은 정말 좋아하지 않기 때문에 이해하기를 포기하고 Arrow Function(=>) 만 의지하게 되었습니다. 하지만 ‘프로토타입'에 대해 이해한 뒤로는 요 this 를 명확하게 이해하게 되었고 매력적인 요소로 받아들이게 되었습니다.

아래는 this 에 대한 대표적인 오해들입니다.

- this 는 기본적으로 window 다 ( X )
- 이벤트 리스너에서 등록한 콜백의 this 는 내부에서 bind 등을 통해 바뀌기때문에 무엇인지 알 수 없다. ( X )
- this 는 외워야한다 ( X )

이러한 오해를 바로잡기 위해선 먼저 프로토타입 철학에서 이런 상황을 어떻게 해석하는지 알 필요가 있습니다.

비트겐슈타인은 그의 대표적인 저서 ‘철학적 탐구'에서 단어의 쓰임새가 곧 의미라는 점을 강조했습니다(의미사용이론). 그는 이를 ‘발화’ 라고 얘기했는데요, 위에서 예시 들었던 것 처럼 ‘벽돌!’이라고 크게 외칠 때, 그것이 어디서 ‘발화’되느냐에 따라서 단어의 의미가 달라집니다. 좀더 쉽게 얘기하면 받아들이는 ‘대상' 에 따라서 같은 단어도 의미가 달라진다는 얘기입니다.

이것이 바로 프로토타입과 클래스의 대표적인 차이라고 볼 수 있습니다. 전혀 다르게 단어를 보는 방식이고 중요한 세계관의 차이입니다. 미리 분류하고 정의한 클래스를 가장 중요하게 여기는 전통적인 방식과는 달리, 프로토타입에서는 받아들이는 주체와 문맥이 가장 중요한 것이죠. 프로그래밍으로 보자면 실행(invoke)하는 ‘객체' 가 중요하다는 의미입니다.

이것이 바로 프로토타입 기반 언어인 자바스크립트에서 this 가 클래스 기반 언어들과 다르게 동작하는 이유입니다.

프로토타입 기반 언어에서는 this 가 정의된 함수가 어떻게 발화(invoke) 되었는지에 따라 가리키는 값이 달라집니다. 정확히는 받아들이는 대상의 컨텍스트를 가리킵니다.

이를 이해하려면 먼저 메소드와 메시지를 명확하게 알아야 합니다.

- 메소드 : 객체의 함수
- 메시지 : 메소드를 실행하라는 메시지 전달

자바에서는 클래스의 메소드를 호출하는 행위를 메시지라 합니다. 자바스크립트 개발자에게는 위 용어가 익숙하지 않을 수도 있을 것 같은데, 메시지로 이해하는 것이 앞으로의 내용을 이해하는데 도움이 될 것 같습니다. 자바스크립트를 예로 들면 foo 라는 객체가 있고 그 내부에 bar() 라는 함수가 있을 때 다음처럼 발화(invoke) 할 객체를 지정할 수 있습니다

- foo.bar()
- bar.call(foo)
- var boundBar = bar.bind(foo)

위처럼 foo 객체를 통해 발화한 함수는 내부 this 가 무조건 foo 를 가리킵니다. 만약 아무것도 지정되어있지 않으면 글로벌(브라우져라면 window)을 가리킵니다.

좀더 자세히 알기 위해 예시를 준비했습니다.

```js
var someValue = "hello"
function outerFunc() {
  console.log(this.someValue) // 첫번째 : ?, 두번째 : ?
  this.innerFunc()
}
const obj = {
  someValue: "world",
  outerFunc,
  innerFunc: function () {
    console.log("innerFunc's this : ", this) // 첫번째 : ?, 두번째 : ?
  },
}
obj.outerFunc() // 첫번째
outerFunc() // 두번째
```

- 3L : 13L 에서 호출한 첫번째는 world가, 14L 에서 호출한 두번째는 hello 가 찍힙니다. outerFunc 가 누구를 통해 발화되었는지를 알면 this 가 무엇이 될지 알 수 있습니다
- 4L : obj 를 통해 발화되면 innerFunc 가 존재하기 때문에 호출되지만, 글로벌에서 발화되면 innerFunc 가 없기 때문에 에러가 납니다
- 10L : this 가 이중으로 들어가있어 헷갈릴 수 있는데 복잡하지 않습니다. this(obj) 를 통해 발화했기 때문에 첫번째는 obj 가 됩니다.

먼저, 13L 의 obj.outerFunc 호출 상황을 그림으로 그려보면 아래와 같습니다.

![](https://miro.medium.com/v2/resize:fit:700/1*sU6vTevHUcZAsXF1zz31Ag.png)

- 시작 : 자바스크립트 엔진이 코드를 실행합니다. (브라우져에서 use strict 모드가 아닌 경우 this 는 window 를 가리킵니다)
- 1번 : 코드의 13L 을 만나면 엔진은 obj 에 outerFunc 를 실행하라는 메시지를 보냅니다.
- 2번 : obj 에서 outerFunc 를 발화합니다. 코드 로드 시 만들어져있는 실행문맥을 참고해 실행합니다. 이때 실행 문맥상의 this 는 발화한 obj 를 가리킵니다.
- 3번 : 실행중에 this.innerFunc 를 만납니다. 엔진은 this 가 가리키는 obj 에 innerFunc 를 실행하라는 메시지를 보냅니다.
- 4번 : obj 에 innerFunc 이 선언되어있으니 잘 실행합니다

14L 의 outerFunc 호출 상황을 그림으로 그려보면 아래와 같습니다.

![](https://miro.medium.com/v2/resize:fit:700/1*RcrKnh6VwTclbsLiYypQeA.png)

- 1번 : 코드의 14L 을 만나면 엔진은 자신(global)의 실행문맥상에 존재하는 outerFunc 을 호출합니다.
- 2번 : 발화한 지점이 엔진(global)이니 this 는 엔진을 가리킵니다. 엔진에 innerFunc 을 실행하라는 메시지를 보냅니다
- 3번 : 글로벌 실행문맥에는 innerFunc 이 없기 때문에 에러가 납니다

여기까지 잘 이해가 되었는지 모르겠습니다. 문제를 하나 더 내볼께요!

```js
function handle() {
  console.log(this) // 첫번째 ?, 두번째 ?
}
document.getElementsByTagName("body")[0].addEventListener("click", handle) // 첫번째. 호출되었다고 가정.handle(); // 두번째. 첫번째 이후에 호출되었다고 가정.
```

this 를 얘기할 때 많이들 헷갈려하는 문제입니다. 발화지점으로 생각하면 전혀 헷갈리지 않습니다.

![](https://miro.medium.com/v2/resize:fit:700/1*NCnqM2YQgJ7oSxdSYawyrg.png)

addEventListener 함수는 해당 엘리먼트에 콜백을 등록하는 함수입니다. 간단하게 얘기하면 ‘div’ 객체에 ‘handle’ 메소드를 등록했다고 볼 수 있죠.

- 1번 : 브라우져에서 div 를 클릭하면 엔진이 반응합니다
- 2번 : 해당 엘리먼트(div)에 등록된 event listener 들을 실행하라는 메시지를 보냅니다
- 3번 : div 엘리먼트에서 handle 을 발화 합니다.
- 4번 : 이때 handle 의 실행문맥의 this 는 발화한 div 를 가리킵니다.

마지막 문제는 약간 재미로 넣은 보너스입니다.

```js
var value = 1

var obj = {
  value: 100,
  foo: function () {
    setTimeout(function () {
      console.log("callback's this: ", this) // ?
      console.log("callback's this.value: ", this.value) // ?
      function bar() {
        console.log("bar's this: ", this) // ?
      }
      bar()
    }, 1000)
  },
}

obj.foo()
```

this 는 무엇이 될까요?

7L : 브라우져 라면 window 를 가리킵니다. 하지만 node.js 라면? 재밌게도 Timer 란 객체를 가리킵니다. setTimeout 에 대한 구현이 다른거죠. node.js 에서는 setTimeout 시 Timer 객체에 등록하고 해당 tick 이 되면 Timer 에 실행하라는 메시지를 보내나 봅니다. 중요한 점은, 같은 코드여도 돌아가는 엔진마다 다를 수 있다는 의미인 것 같습니다.

8L : 브라우져라면 1, node.js 라면 undefined 가 나옵니다. 기본 this 는 global 라고 외우면 안되는 이유입니다

9L : 당연하게도 브라우져라면 window, node.js 면 global 을 가리킵니다. 엔진이 어떤 방식으로 실행했는지를 기억하시면 됩니다.

## 마무리

드디어 프로토타입에 대한 긴 여정이 마무리 되었습니다.

프로토타입은 ‘클래스’의 다른 구현이 아닌, 완전히 새로운 인식 하에 만들어진 이론입니다. 이러한 차이점을 이해하게 된다면 더 이상 JS 의 프로토타입, 호이스팅, this 는 암기 과목이 아니게 됩니다. 저는 이것을 이해한 뒤로 더 이상 헷갈리는 부분이 없어졌습니다.

최근 자바스크립트 스펙에서 `class`, `arrow function`, `let`, `const` 등 여타 일반적인 언어와 보편성을 맞추려는 시도도 많고, 이것들을 정말 편하게 사용 중이지만 근본(프로토타입)은 변하지 않는다는 걸 알아야 합니다. 또한 이것들이 언어적 지원이 아닌 syntactic sugar 인 부분도 언어의 근본 구조(프로토타입)가 다르기 때문임을 이해할 수 있게 되면 좋겠습니다. 지금도 많은 구루들이 JS 의 디자인 철학(프로토타입)을 해치지 말자고 주장하고 있지요. ([더글라스 크록포드 왈 : 클래스는 ES6의 최대 실수다](https://www.youtube.com/watch?v=PSGEjv3Tqo0&t=300s)). 이런 흐름을 이해하려면 언어의 디자인 철학을 이해할 필요가 있을 것 같습니다.

글을 쓸 땐 항상 마무리가 가장 어렵네요. 재밌게 읽으셨으면 좋겠습니다. 다들 즐겁게 JS 코딩하세요 🙂

(2021–12–13 업데이트 : JS 의 모태가 된 Self 링크를 추가하고 Kevo의 가족유사성 설명을 추가했습니다)

레퍼런스

- [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.56.4713&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.56.4713&rep=rep1&type=pdf)
- [https://m.blog.naver.com/ms2948/220999019306](https://m.blog.naver.com/ms2948/220999019306)
- [https://imnt.tistory.com/207](https://imnt.tistory.com/207)
- [http://m.blog.daum.net/wise1004-1/6985545](http://m.blog.daum.net/wise1004-1/6985545)
- [http://zolaist.org/category/과학철학/page/2](http://zolaist.org/category/%EA%B3%BC%ED%95%99%EC%B2%A0%ED%95%99/page/2)
- [http://www.aistudy.co.kr/paper/pdf/scientific_lee.pdf](http://www.aistudy.co.kr/paper/pdf/scientific_lee.pdf)
- [https://m.blog.naver.com/PostView.nhn?blogId=linigy&logNo=80002151688&proxyReferer=https:%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=linigy&logNo=80002151688&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)
- [https://www.koreascience.or.kr/article/JAKO200916263468706.pdf](https://www.koreascience.or.kr/article/JAKO200916263468706.pdf)
- [https://www.netinbag.com/ko/science/what-is-prototype-theory.html](https://www.netinbag.com/ko/science/what-is-prototype-theory.html)
- [https://skytreesea.tistory.com/11](https://skytreesea.tistory.com/11)
- [https://m.blog.naver.com/PostView.nhn?blogId=ilikepeace8&logNo=221004215876&proxyReferer=&proxyReferer=https:%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=ilikepeace8&logNo=221004215876&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F)
- [https://kaspyx.tistory.com/93](https://kaspyx.tistory.com/93)
- [https://namu.wiki/w/루트비히 요제프 요한 비트겐슈타인#s-1](https://namu.wiki/w/%EB%A3%A8%ED%8A%B8%EB%B9%84%ED%9E%88%20%EC%9A%94%EC%A0%9C%ED%94%84%20%EC%9A%94%ED%95%9C%20%EB%B9%84%ED%8A%B8%EA%B2%90%EC%8A%88%ED%83%80%EC%9D%B8#s-1)
- [https://www.slideshare.net/vcmlab/cog5-lecppt-chapter08](https://www.slideshare.net/vcmlab/cog5-lecppt-chapter08)
- [https://laurabecker.gitlab.io/classes/as/08-semantics.pdf](https://laurabecker.gitlab.io/classes/as/08-semantics.pdf)
- [https://m.blog.naver.com/PostView.nhn?blogId=starsailoris&logNo=220530218923&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=starsailoris&logNo=220530218923&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [https://expertiza.csc.ncsu.edu/index.php/CSC/ECE_517_Fall_2010/ch4_4e_ms](https://expertiza.csc.ncsu.edu/index.php/CSC/ECE_517_Fall_2010/ch4_4e_ms)