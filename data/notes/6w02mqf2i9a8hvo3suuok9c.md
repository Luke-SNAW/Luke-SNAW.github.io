
> https://www.youtube.com/watch?v=tbDDYKRFjhk

## Kagi Summarize

- **AI's Impact on Developer Productivity**: AI increases developer productivity by roughly 15-20% on average, but this varies based on several factors.
- **Rework and Refactoring**: Implementing AI often leads to more rework, which can be misleading as it doesn't always contribute to useful output.
- **Task Complexity Matters**: AI is more effective for low-complexity tasks, with productivity gains of 30-40%, compared to 10-15% for high-complexity tasks.
- **Project Maturity**: AI is more beneficial for greenfield projects (new projects) than brownfield projects (existing projects with a codebase).
- **Language Popularity**: AI is less effective for low-popularity programming languages, and can even decrease productivity for complex tasks in these languages.
- **Codebase Size**: As codebase size increases, the productivity gains from AI decrease sharply due to context window limitations and increased dependencies.
- **Context Window Limitations**: Even with larger context windows, AI performance decreases as the amount of context increases.
- **Methodology**: The study used a model that automates the evaluation of code changes, making it scalable and affordable compared to manual expert evaluations.
- **Surveys are Ineffective**: Self-reported surveys are poor predictors of developer productivity, with developers often misjudging their own productivity by about 30 percentile points.
- **AI is Not a One-Size-Fits-All Solution**: AI's effectiveness varies based on task complexity, project maturity, language popularity, codebase size, and context length, so it should be used judiciously.

---

## [GeekNews 요약](https://news.hada.io/topic?id=22248)

연사는 "AI가 개발자를 전적으로 대체할 수 없다"는 점을 분명히 하며, AI 도입이 생산성에 분명히 도움을 주지만, 항상 그런 것은 아니고, 오히려 생산성이 감소하는 경우도 드물지 않다고 강조.

### 연구 설계 및 데이터

- **3년간, 600여 개 회사, 10만 명 이상의 소프트웨어 엔지니어, 십억 줄 이상의 코드, 수천만 건의 커밋 대상으로 측정.**
- 대부분은 _비공개 저장소(Private Repo)_ 기반 데이터 → 개발팀과 기업 단위의 실제 생산성 변화 측정 가능.

### 기존 연구의 한계

- *벤더 주도의 보고서*는 자사 AI툴 홍보 목적이 많아 객관성 부족.
- 단순 커밋/PR 개수, 평균 작업 시간 변화 등은 실제 생산성을 왜곡할 수 있음.
  - 예: AI 사용 직후엔 버그나 재작업(rework)성 커밋이 함께 증가하여 피상적으로만 생산성이 높아진 것처럼 보임.
- "그린필드(새로운 프로젝트) 실험"에서는 AI의 효과가 매우 커 보이나, 기존 코드(브라운필드)에서는 차이가 줄어듦.
- 개발자 설문(Self-report)은 실제 생산성과 큰 상관성이 없음(30%포인트 이상 체감과 실제 간극).

### Stanford의 생산성 측정 모델

- **전문가 패널 평가**와 유사한 _AI 기반 자동화 모델_ 활용:
  - 커밋별 _기능적 변화(added/removed/refactored/rework)_ 측정
  - 단순 "라인 수"가 아니라 "기능, 유지보수성, 품질"에 초점
- 기능 도입량, 리팩터링, 최근 커밋의 재수정(rework) 비중 등 정밀함.

### 주요 연구 결과

- 전체적으로 **AI 도입 시 평균 생산성 15~20% 증가**.
  - 하지만 상당량의 "재작업"(rework)이 동반되어 체감적 효익이 과장되는 경향도 있음.
- 팀/회사/과제 유형별로 **큰 편차** 존재.

### 생산성 격차의 원인: 과제 난이도·프로젝트 종류·언어·코드베이스 크기

| 프로젝트 유형         | 낮은 복잡도  | 높은 복잡도  |
| --------------------- | ------------ | ------------ |
| **그린필드** (신규)   | **30~40% ↑** | **10~15% ↑** |
| **브라운필드** (기존) | **15~20% ↑** | **0~10% ↑**  |

- **복잡성이 낮고, 신규(그린필드) 프로젝트**에서는 AI의 효과가 큼.
- **기존(브라운필드)·복잡한 시스템**은 효과가 뚜렷하게 줄고, 일부 케이스에서는 **생산성 감소 사례도 발견**.
- 실제 27개 기업 136개 팀 샘플 기준(강의 내 언급).

### 언어 인기와 AI 효과

- **파이썬/자바/자바스크립트(인기 언어)** 에서는 AI의 생산성 향상 크며,
- **COBOL/엘릭서/하스켈(비인기 언어)**: AI의 도움 거의 없고, 오히려 복잡한 작업에선 시간 낭비-생산성 저하까지 유발.
  - 예: 비인기 언어 & 높은 난이도의 경우 "오류 많고, 맞는 코드 못 내놓음" → 없는 게 나음.

### 코드베이스 크기와 AI 효과

- 코드베이스가 **클수록 AI의 생산성 향상효과가 급격히 줄어듦**.
  - 원인:
    - **컨텍스트 윈도 한계**: LLM이 여러 파일/수십만~수백만 라인 전체 맥락을 다 넣을 수 없음.
    - _"시그널/노이즈 비율" 감소_: 맥락 정보가 많아질수록 AI가 적합한 정보를 제대로 식별하지 못함.
    - 도메인별, 서비스별 복잡도가 많아질수록 실제 재구현 난도 상승
  - 실제로 최신 대형 LLM(Gemini 1.5 Pro 등)은 "토큰 수"가 늘어날수록 정확도가 90%→50%미만으로 급락.

### 총정리: 언제 AI가 효과적인가?

- **AI는 대부분의 경우(특히 간단한 신규 코드 작성)는 분명히 개발자 생산성을 향상**시킴.
- 하지만 **복잡한 유지보수, 오래된(대형) 코드, 비주류 언어, 많은 의존성**이 있는 환경에서는 한계 크고,
- *최상의 AI 생산성 전략*은 회사·팀·과제 특성에 맞추어 신중하게 설계해야 함("원 사이즈 핏 올" 아님).
- 설문, 마케팅 지표, 단순 커밋 수 증가는 신뢰 어렵고, 실제 코드 기능성과 반복작업 비율, 재작업량 등 "현실 기준 측정" 필요.

### 결론

- **AI는 "대다수 상황"에서 생산성 증가하지만, 과대평가 또는 과소평가 모두 주의**해야 함.
- 도입 성과가 잘 나는 "구체적 조건(간단/신규/인기 언어/작은 codebase)"을 파악해서 적용해야 하며, 무비판적·무차별적인 도입은 오히려 역효과가 날 수 있음.
