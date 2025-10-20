---
id: pck31wdeftzv84so8l31a9t
title: "Building with Elixir for Three Years: A Production Retrospective"
desc: ""
updated: 1760916761012
created: 1760916400012
---

> https://ryanrasti.com/blog/elixir-three-years-production/ - Jul 10, 2025

- The BEAM (Erlang VM) delivered on its promises of scalability, concurrency, and resilience, reducing the need for complex tooling and orchestration.
- The Elixir ecosystem has exceptional depth in core areas but lacks breadth, with gaps in libraries for tasks outside the core ecosystem.
- Phoenix and LiveView aimed to eliminate frontend/backend split pain but did not meet the complex UI/UX needs of the warehouse management system.
- Developer experience in Elixir fell short compared to TypeScript, with issues in autocomplete, compile times, and static analysis.
- Elixir attracted high-quality talent, with developers demonstrating deep technical knowledge and pragmatic problem-solving skills.
- Oban proved to be a reliable tool for background jobs, and remote IEx was invaluable for debugging production issues during the MVP launch.
- Deployment of Elixir applications presented unexpected challenges, leading to the use of NixOS for VM management.
- Elixir is best suited for specific problems like distributed systems and real-time features, but may not be ideal for full-stack applications where developer velocity is crucial.
- The future of Elixir may be influenced by AI, with potential for accelerated evolution or consolidation around TypeScript.
- TypeScript's superior tooling, instant feedback loops, and static types give it an advantage in the AI-driven development landscape.

---

I recently responded to a [Hacker News thread](https://news.ycombinator.com/item?id=44495879) about Elixir’s benefits. As CTO of a startup that built with Elixir for two years before deploying to production in our third, I wanted to share our actual experience versus the marketing promises.

We built a warehouse management system from scratch — complete with multi-warehouse inventory tracking, order routing, pick/pack workflows, and dozens of e-commerce integrations. We successfully went live with our MVP and first customers, and have since fulfilled over 100,000 orders. Here’s what worked, what didn’t, and what I’d do differently.

## The BEAM: Living Up to the Hype

The Erlang VM delivered on its core promise. Scalability, concurrency, and resilience “just worked.” No orchestration needed, no complex tooling, no surprises. You avoid the typical distributed systems mess — no gluing together Redis for queues, Kubernetes for orchestration, and a dozen other tools. Everything you need comes built-in. When you are running a lean team, this reduced surface area means you can iterate faster with fewer things that can break.

## The Ecosystem: Depth Over Breadth

The ecosystem is hit or miss. I would characterize it as having exceptional depth where it matters but frustrating gaps elsewhere.

[Phoenix](https://phoenixframework.org/) and [Oban](https://hexdocs.pm/oban/Oban.html) were fantastic — world-class libraries that did exactly what we needed.

[Ecto](https://hexdocs.pm/ecto/Ecto.html) deserves special mention. This query builder opened my eyes to what is possible beyond raw SQL. It saved us countless times with its ability to dynamically compose queries — in that sense, it is even more powerful than raw SQL. The biggest drawback? Most extensions require writing macros, which are hard to grasp when you are picking up Elixir for the first time.

Step outside that golden path and you will hit walls fast. No good libraries for parsing shell commands. Shopify integration libraries were either missing or unmaintained. When you venture beyond the core ecosystem, be ready to build it yourself.

## Phoenix: The Double-Edged Sword

Phoenix and [LiveView](https://hexdocs.pm/phoenix_live_view/Phoenix.LiveView.html) promise to eliminate the split frontend/backend pain that plagues so many teams. No more maintaining separate frontends. No more coordinating across teams. No more API versioning headaches. For rapid iteration, this sounds transformative.

We started with React from day one. LiveView could handle simple interactions beautifully, but we knew it could not deliver the complex UI/UX flows our warehouse management system demanded. We ended up with the exact split-stack complexity Phoenix aims to solve. Looking back, a full-stack Node.js framework would have simplified our client/server interaction considerably.

## Developer Experience: The Achilles’ Heel

I love functional programming, and Elixir’s standard library is thoughtfully designed. The developer experience fell short compared to TypeScript in ways that compound over time.

**Autocomplete was a coin flip.** Half the time [ElixirLS](https://github.com/elixir-lsp/elixir-ls) simply did not work — either too slow or completely broken. When it did work, the static analysis was not sophisticated enough to provide genuinely useful suggestions. In a 300K line codebase, you need autocomplete just to remember function names and schema attributes. Without it, you are constantly grepping through files.

**Compile times broke my flow.** Our 300K line codebase took 10 seconds to recompile after a one-line change, plus a few more seconds for tests. We used GraphQL to get typing between backend and frontend — crucial for type safety and developer experience, but it came at a steep cost. After several hundred thousand lines of code, the full cycle became painful: recompile Elixir, then regenerate types — easily 20 seconds on beefy hardware for a single-line change. VS Code often choked on the huge type definition changes, requiring a full restart to make IntelliSense happy again. Compare that to the instant feedback loop of [Vite](https://vitejs.dev/). Those 20-second turnarounds might sound trivial, but they shatter concentration and compound into hours of lost productivity.

## The Unexpected Wins

Despite the challenges, Elixir delivered some surprising victories.

**Talent quality was exceptional.** Every Elixir developer we interviewed demonstrated deep technical knowledge and pragmatic problem-solving skills. The community self-selects for engineers who choose tools for sound technical reasons, not resume padding or trend chasing. Elixir also made our roles more appealing — talented engineers were excited to work with the language, giving us an edge in recruiting.

**Oban saved us repeatedly.** We leaned on it heavily for background jobs, and I honestly cannot imagine building our system without it. Rock solid.

**Remote IEx got us through MVP.** Being able to debug production issues in real-time via remote console access was absolutely clutch for our launch. Not something you would want to rely on forever, but invaluable when you need it.

## Deployment: More Complex Than Expected

Elixir’s distributed nature, while powerful, created unexpected deployment challenges. We started on Fly.io but their repeated instability and lack of managed Postgres forced us to look elsewhere. Cloud Run seemed perfect until we discovered it did not support the peer-to-peer ports Elixir needed for clustering.

We ended up running virtual machines with [NixOS](https://nixos.org/) to manage the overhead. The alternative was Kubernetes, but even managed Kubernetes felt like overkill for our needs. NixOS made VM management tolerable, but it was still more operational complexity than we had budgeted for.

## The Verdict

Elixir shines as the right tool for specific problems. For us building a full-stack application, the experience was decidedly mixed.

Part of this challenge is structural — JavaScript owns the frontend, giving JavaScript frameworks an inherent full-stack advantage that is hard to overcome. There is also significant room for Elixir to improve its developer experience, particularly around tooling and compile times. I am not alone in this assessment — [James Russo from Brex](https://boredhacking.com/areas-of-improvement-for-elixir/) documented similar pain points after running Elixir at scale there.

Would I choose Elixir again? It depends entirely on what you’re building. Need true concurrency and fault tolerance for a distributed system? Absolutely. Building a full-stack application where developer velocity is paramount? I would carefully evaluate other options first.

The key lesson after three years is actually an old lesson: use the right tool for the job. Elixir excels at certain challenges — distributed systems, real-time features, fault tolerance. Force it into the wrong context, and you will fight it the entire way.

Most of the pain points I encountered are technical problems with technical solutions. Better tooling, faster compilation, improved static analysis — these are solvable challenges. The Elixir community is talented and pragmatic. I hope they tackle these issues, because the core technology is genuinely impressive.

## The Future: The AI Wild Card

The biggest unknown is how AI will reshape the landscape. I see two competing possibilities — both entirely plausible yet leading to radically different outcomes:

1. **AI accelerates Elixir’s evolution.** LLMs could help the smaller Elixir community punch above its weight — addressing tooling gaps faster, improving documentation, and letting the language’s strengths shine through.
2. **AI drives consolidation around TypeScript.** Every new project becomes full-stack Next.js. Old projects get rewritten. The AI hive mind converges on “best practices” and every LLM regurgitates the same stack recommendation. Alternative approaches get buried under the weight of generated sameness.

My bet? The language with the best feedback loop to LLMs wins. TypeScript has a huge advantage here. Static types give LLMs clear signals about correctness. At our startup, we reached a point where TypeScript eliminated virtually all runtime type errors — no null pointer exceptions, no frontend crashes from type mismatches. I have only heard similar stories from niche functional languages like Elm.

Ironically, functional programming should be perfect for LLMs. When there is no global mutable state, you need much less context to understand what code does. Elixir has this advantage. TypeScript does not.

One last thought: the alternatives are not standing still. TypeScript already has the superior tooling and instant feedback loops. New tools like [tsgo](https://devblogs.microsoft.com/typescript/typescript-native-port/) promise 10x faster performance (we’ve seen 5x improvements in our codebase). Meanwhile, TypeScript keeps adding features that chip away at functional programming’s advantages — better immutability support, stricter null checking, even pattern matching proposals.

Elixir’s window to catch up might be closing. The race is on.

---

Elixir와 BEAM의 핵심 강점(동시성, 장애 내성)은 실제로 훌륭하게 작동했으나, 코드베이스(약 30만 줄)가 성장함에 따라 개발자 경험(DX)과 생태계의 단점이 두드러졌다. MVP 1년 + 전체 3년 운영 경험을 바탕으로 한 장단점 정리.

## 장점 (The Good Parts)

- **BEAM의 기본 기능**: 동시성, 장애 내성, "just works" 수준의 안정성. 생산 환경에서 신뢰할 수 있음.
- **라이브러리와 도구**: Ecto(데이터베이스), Oban(작업 큐) 같은 도구가 세계적 수준. 원격 `iex`는 프로덕션 디버깅의 생명줄.
- **인재 풀**: Elixir 엔지니어의 질이 뛰어나 채용에서 큰 이점.

## 단점 (Where We Struggled)

- **개발자 경험 (DX)**: 가장 큰 병목. 대규모 코드베이스에서 한 줄 변경 시 컴파일 시간이 10~15초 이상 소요되어 흐름이 끊김. Vite/TypeScript 같은 즉각 피드백과 비교해 느림.
- **도구링**: ElixirLS의 자동 완성(autocomplete)이 불안정해 대형 코드베이스에서 함수명이나 스키마 필드를 grep으로 검색해야 함. 테스트/재컴파일 사이클이 모멘텀을 죽임.
- **생태계 (Ecosystem)**: 깊이는 있지만 폭이 좁음. Phoenix, Ecto, Oban은 훌륭하나, Shopify 라이브러리 같은 사소한 기능도 직접 구현해야 함. 다른 생태계에서 쉬운 일이 벽에 부딪힘.
- **풀스택 문제 (Full-Stack)**: 복잡한 UI(클라이언트 측 상호작용 많음)에서 LiveView가 적합하지 않아 React 프론트엔드를 도입. 결과적으로 GraphQL 오버헤드와 컨텍스트 스위칭으로 풀스택 JS 프레임워크보다 복잡해짐.
- **배포 및 DevOps**: 클러스터링으로 인해 단순 컨테이너(Cloud Run) 대신 복잡한 VM 관리(NixOS) 필요. fly.io에서 Postgres 불안정성으로 마이그레이션. (참고: 현대 Elixir 도구에서 핫 코드 업그레이드 지원이 실질적으로 약함.)
- **개선 영역**: [이 포스트](https://boredhacking.com/areas-of-improvement-for-elixir/)에서 지적된 DX, 도구링, 생태계 문제와 유사한 고통 경험.

## 결론

Elixir는 특정 문제(예: 고동시성 백엔드)에 최적화된 킬러 도구지만, 풀스택 앱처럼 복잡한 경우 장점이 일방적이지 않음. 이 trade-off는 생태계 성숙도 문제로 보이는데, 다른 팀들은 어떻게 극복하나? 근본적 문제 vs. 우선순위 개선으로 보는가?

> - https://news.ycombinator.com/item?id=44495879
> - https://news.ycombinator.com/item?id=45613852
