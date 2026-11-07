
> https://www.cs.unc.edu/~stotts/COMP590-059-f24/robsrules.html

1. **Rule 1.** You can't tell where a program is going to spend its time. Bottlenecks occur in surprising places, so don't try to second guess and put in a speed hack until you've proven that's where the bottleneck is.

2. **Rule 2.** Measure. Don't tune for speed until you've measured, and even then don't unless one part of the code overwhelms the rest.

3. **Rule 3.** Fancy algorithms are slow when n is small, and n is usually small. Fancy algorithms have big constants. Until you know that n is frequently going to be big, don't get fancy. (Even if n does get big, use Rule 2 first.)

4. **Rule 4.** Fancy algorithms are buggier than simple ones, and they're much harder to implement. Use simple algorithms as well as simple data structures.

5. **Rule 5.** Data dominates. If you've chosen the right data structures and organized things well, the algorithms will almost always be self-evident. Data structures, not algorithms, are central to programming.

Pike's rules 1 and 2 restate Tony Hoare's famous maxim "Premature optimization is the root of all evil."

Ken Thompson rephrased Pike's rules 3 and 4 as "When in doubt, use brute force.".

Rules 3 and 4 are instances of the design philosophy KISS.

Rule 5 was previously stated by Fred Brooks in The Mythical Man-Month. Rule 5 is often shortened to "write stupid code that uses smart objects".

---

> https://news.ycombinator.com/item?id=47423647

Jonathan Blow의 [강연](https://www.youtube.com/watch?v=JjDsP5n2kSM)을 떠올리게 됨  
그는 **생산성** 관점에서 접근했음. Braid 개발 초기에는 거의 모든 걸 단순한 배열로 구현했고, 병목이 생길 때만 수정했음  
“속도나 메모리보다 더 중요한 건, 프로그램 하나를 구현하는 데 걸리는 **인생의 시간**”이라는 말이 인상적이었음

- 게임은 수많은 유사 객체를 초당 60프레임 이상으로 반복 처리하므로, 단순한 **배열 기반 구조**가 합리적인 기본값임
- 게임 개발에서는 16ms 안에 프레임을 렌더링해야 하므로, 고정 크기 테이블과 선형 탐색이 흔한 패턴임. **동적 할당**의 예측 불가능성을 피하기 위한 구조적 선택임
- 이 관점은 게임 외의 일반 개발에도 통함. 우리 모두는 마감과 비용 제약 속에서 일하므로, **엔지니어링 시간** 자체가 비용임
- 다만 게임의 교훈을 일반 프로그래밍에 그대로 확장하는 건 조심해야 함. 게임은 재사용보다 **특수 목적 코드** 중심이고, 일반 소프트웨어는 데이터 중심임

Rule 1을 진심으로 받아들이면, Rule 3~5는 자연스럽게 따라옴  
병목을 예측할 수 없다는 전제를 인정하면, **단순한 코드 작성과 측정**이 유일한 합리적 전략이 됨  
실제로 가장 자주 실패하는 건 조기 최적화가 아니라 **조기 추상화**임. 필요하지 않은 유연성을 위해 복잡한 계층을 만들고, 그게 오히려 유지보수 비용을 키움

- “추상화는 **자연스럽게 등장해야지**, 미리 설계하는 게 아니다”라는 말을 팀 내에서 자주 인용함
- 조기 추상화는 개발자 시간을 낭비시키고, **기술 부채**를 늘리며, 버그 가능성을 높임. 종종 ‘미래의 문제를 대비한다’는 명목으로 생김
- 관련 논문으로 [Philip Wadler의 글](https://people.mpi-sws.org/~dreyer/tor/papers/wadler.pdf)을 참고할 만함
- 나는 성능보다 **가독성과 유지보수성**을 더 중시함. 그래서 나에겐 Rule 4가 근본이고, Rule 1은 그 결과임

Rule 5에 전적으로 공감함  
어려운 문제일수록 **데이터 구조와 API의 반복적 개선**으로 해결됨. 구조가 잘 잡히면 제어 흐름은 자연스러워짐  
LLM은 이런 구조적 사고에는 약함. 복잡한 제어 흐름은 잘 제안하지만, **조합 가능한 데이터 구조 설계**는 잘 못함

- 내 경험상 Rule 5가 사실상 Rule 1임. “코드를 보여주면 혼란스럽지만, **데이터베이스 스키마**를 보여주면 모든 게 명확해진다”는 말이 있음
- 분산 서비스에서는 Rule 5가 자주 무시됨. 여러 HTTP·DB 호출을 나누는 대신, **한 번의 호출로 처리**할 수 있는 구조가 더 효율적임

“측정 없이 튜닝하지 말라”는 규칙과 Jeff Dean의 [Latency Numbers Every Programmer Should Know](https://gist.github.com/jboner/2841832)를 비교하면 흥미로움  
Dean은 사전 지식으로 **성능을 예측**할 수 있다고 말함  
결국 두 입장은 조화될 수 있음 — 설계 단계에서는 감각적으로 빠른 구조를 택하고, 구현 후에는 **측정 기반으로 미세 조정**해야 함

- 진짜 빠른 코드는 두 접근을 모두 사용함. 설계 단계에서 **캐시 효율성**을 고려하고, 이후 프로파일링으로 병목을 제거함
- 지연(latency) 수치는 알고리즘의 **이론적 한계선**을 알려줄 뿐, 실제 성능은 구현과 런타임 환경에 따라 달라짐
- ‘조기 최적화’가 금지하는 건 **국소적 해킹 수준의 튜닝**임. 전체 설계에서 속도를 고려하는 건 당연함
