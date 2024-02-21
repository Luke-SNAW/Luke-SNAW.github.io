---
id: e3yxr6ae8tfu2hzmbi70rzc
title: In defense of simple architectures
desc: ""
updated: 1708477926323
created: 1708477826163
---

> https://danluu.com/simple-architectures/

Wave is a $1.7 billion company that runs a simple CRUD app architecture with a Python monolith on Postgres. This simple approach has allowed them to scale to their size while engineers focus on delivering value to users. Despite the effectiveness of simple architectures, most conferences focus on complex architectures. Wave keeps its architecture simple by using synchronous Python, farming out long tasks, and carefully managing database transactions. They also discuss some initial choices like RabbitMQ and Celery that they now question, but feel Python and GraphQL still make sense for their needs despite some downsides.

An interesting point made is that Wave's simple architecture allows them to spend their complexity budget where it matters most for their business, such as in telecom integrations which are unavoidably complex but critical given their operations in Africa. This strategic focus on complexity has helped them build a large business with relatively few engineers.

## from [from-nibly](https://news.ycombinator.com/item?id=39441508)

This is what I tell engineers. Microservices aren't a performance strategy. They are a POTENTIAL cost saving strategy against performance. And an engineering coordination strategy.  
Theoretically If you have a monolith that can be scaled horizontally there isn't any difference between having 10 replicas of your monolith and having 5 replicas of two microservices with the same codebase. UNLESS you are trying to underscale part of your functionality. You can't underscale part of your app with a monolith. Your pipe has to be big enough for all of it. Generally speaking though if you are talking about 10 replicas of something there's very little money to be saved anywhere.

Even then though the cost savings only start at large scales. You need to have a minimum of 3 replicas for resiliency. If those 3 replicas are too big for your scale then you are just wasting money.

The place where I see any real world benefit for most companies is just engineering coordination. With a single repo for a monolith I can make 1 team own that repo and tell them it's their responsibility to keep it clean. In a shared monolith however 0 people own it because everyone owns it and the repo becomes a disaster faster than you can say "we need enterprise caching".

## [Towards Modern Development of Cloud Applications](https://dl.acm.org/doi/pdf/10.1145/3593856.3595909)

- Writing distributed applications as microservices introduces challenges like increased latency due to network overhead, difficulty reasoning about interactions between versions, and complex application management.
- The proposed solution advocates writing applications as "logical monoliths" using components, and letting a runtime handle physical distribution and execution. This decouples logical and physical boundaries.
- Components represent long-lived computational agents that communicate via interfaces. The runtime determines how to place and replicate components across machines.
- Applications are deployed atomically, preventing different versions from interacting, which reduces failures and eases reasoning about correctness.
- The runtime optimizes for performance using techniques like custom serialization, transport protocols, and automated component placement.
- The programming model focuses developers on business logic while the runtime handles deployment complexities.
- Atomic rollouts are achieved through gradual blue/green deployments observed by the runtime.
- The approach enables new innovations like automated testing of distributed applications and stateful rollout techniques.
- An evaluation showed the proposed solution reduced latency by up to 15x and costs by up to 9x compared to a microservices baseline.
- The approach aims to address challenges of microservices architectures while enabling performance, manageability, and deployment optimizations.
