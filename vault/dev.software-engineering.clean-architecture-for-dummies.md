---
id: upls825jrixo3bbcp6xfuuu
title: Clean Architecture for Dummies
desc: ""
updated: 1667864711628
created: 1667806826347
published: false
tags: architecture
---

> https://medium.com/codex/clean-architecture-for-dummies-df6561d42c94

## I recall struggling to understand the idea of domain-centric architectures, so I decided to write my explanation by resorting to evolving models thus resembling the way we learn.

![](https://miro.medium.com/max/700/1*WtyW262ckzTEzxzV-MELbA.png)

The evolving [atomic models](https://www.wikilectures.eu/w/Atomic_Models). The clean architecture has more resemblance to atoms as we’ll see.

The [_hexagonal architecture_](https://hexagonalarchitecture.org/) (also known as _ports and adapters_) is a must-know architectural pattern. The [_clean architecture_](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) is similar but introduces more concepts (most important, entities and use cases). Both architectures are domain-centric — they’re derived from [domain-driven design](https://en.wikipedia.org/wiki/Domain-driven_design) (DDD). I’ll use a mix of terminology from both.

# Stage 0: the app

People and systems from the outside world interact with your app and vice-versa. This is our starting point. I’ll use the word app but that can mean many things; from a device driver to a server-side rendered UI. In [DDD](https://en.wikipedia.org/wiki/Domain-driven_design), it usually means a [bounded context](https://martinfowler.com/bliki/BoundedContext.html). A domain-centric architecture is not about physical architecture but instead about software design. It boils down to the decoupling of the business domain from the technology, as we’ll see later.

![](https://miro.medium.com/max/700/1*uFbaxSU8lDb-o2Mp-nwcIQ.png)

Your app and the outside world (i.e. the [I/O](https://en.wikipedia.org/wiki/Input/output) devices)

# Stage 1: domain and infrastructure

Let’s zoom into the app and split it into **domain** and **infrastructure**. You could view them as high-level software layers. That division embodies the [separation of business from technology](https://medium.com/codex/technology-is-a-detail-4b1edd341060).

![](https://miro.medium.com/max/700/1*LDrSj492K7s2ZvO2p8X-uw.png)

Splitting the app into the domain (more stable) and the infrastructure (more volatile)

➡️ The **_domain_** (short for ‘business domain’; also known as [core](<https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)>)) is the reason why your app exists. It’s the added value to the business/users/world, i.e. it contains your app’s identity (such as a [eukaryotic cell houses DNA in its nucleus](https://biologydictionary.net/eukaryotic-cell/)). It’s supposed to be independent of specific technologies like databases or web APIs and it shouldn't be tied to frameworks. All it contains is business logic and your domain modeling. Domain code uses the [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html), i.e., the agreed-upon language ([DDD](https://en.wikipedia.org/wiki/Domain-driven_design)).

> The core logic, or business logic, of an application consists of the algorithms that are essential to its purpose. They implement the use cases that are the heart of the application. When you change them, you change the essence of the application. [_Ports-And-Adapters_](http://www.dossier-andreas.net/software_architecture/ports_and_adapters.html)

➡️ The **_infrastructure_** represents the technology; it’s all that’s not business domain; it’s how it speaks with the outer world, whether humans or machines. On one hand, it’s how it gets delivered (e.g. [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)s, web APIs, [CLI](https://en.wikipedia.org/wiki/Command-line_interface)s); on the other hand, it’s how it loads and stores its data (e.g. databases, external APIs).

Even in a simple app like a console utility, soon you feel the need to separate the algorithm (the goal of the app) from the rest (the I/O — inputs parsing and printing). The domain is the algorithm; the I/O is the infrastructure. This separation is the first stage, but the most important one.

> Core code doesn’t directly depend on external systems, nor does it depend on code written for interacting with a specific type of external system. [_Advanced Web Application Architecture_](https://www.goodreads.com/book/show/54179859-advanced-web-application-architecture)

A domain-centric architecture aims to protect the domain, which contains all the [essential complexity](https://dev.to/alexbunardzic/software-complexity-essential-accidental-and-incidental-3i4d) (the domain complexity we are trying to model). The domain is at the center because it’s more stable (less likely to change) than the infrastructure around it. The domain couldn’t care less about the surrounding infrastructure. Ultimately, you could swap all the infrastructure without impacting the domain. In short: _domain_: stable high-level business domain code; _infrastructure_: volatile low-level I/O code.

# Stage 2: adapters, use cases, entities

OK, we’re ready for the second maturity level. This will be a refinement of the previous stage. Let’s consider the most relevant components of the infrastructure: the _adapters_.

➡️ **_Adapters_** are how your app interacts with the world. They wrap the communication with an I/O device. Common examples include API gateways, controllers (e.g. REST, GUI), loggers, monitors, email/SMS services, queue handlers, and database repositories. Adapters also mediate access to unpredictable things like id generators, env vars, and the system clock.

![](https://miro.medium.com/max/700/1*vPsfoD9O8zxyptYwSHl2Ag.png)

Adapters lie outside the domain; they’re the intermediates with the outside world.

Adapters bridge the gap between the app and the outside. Since the “[database is a detail](http://blog.cleancoder.com/uncle-bob/2012/05/15/NODB.html)” and “[the web is a detail](https://www.youtube.com/watch?v=WpkDN78P884)”, every interaction with them is always done through an adapter ([adapter pattern](https://en.wikipedia.org/wiki/Adapter_pattern)).

The adapters are part of your codebase. The remaining part is not your code; it’s what's left of the infrastructure: drivers, MVC frameworks, web frameworks, filesystem APIs, client libraries, and any other mechanism that bridges away to the outside. Handlers are usually coupled with frameworks and that’s fine because they are supposed to be thin. They are just translators and only contain data conversion (i.e. parsing, formatting, rendering), [error handling](https://medium.com/codex/pragmatic-exception-handling-3831f7ce0980), and validation of syntactic rules (e.g. fail if a string is parsed as an integer). **Never put business logic in adapters**.

Recall that the domain embodies the domain’s business rules. This is typically called the “business logic layer”. If we zoom into it, we’ll see the use cases and the entities.

![](https://miro.medium.com/max/700/1*hVrM4LymfJQVRC0vtG5Gvg.png)

Entities are not a software layer. The diagram shows only that they don’t depend on anything.

➡️️ **_Use cases_** (also known as ‘application services’) are pieces of functionality that map user stories into code; they're the reasons to build and use the app. They represent user-centered operations like _Checkout Cart_ or _View Debts_. Therefore, their name should start with a verb (e.g. _Create User_, _Delete Account_, _Withdraw Money_). A use case can be a ‘query’ if you’re interested in its output (e.g. _Get Loan_) or a ‘command’ if you care about its side effects (e.g. _Make Loan_) ([command-query separation](https://martinfowler.com/bliki/CommandQuerySeparation.html)). To make your app’s intents clear, **I recommend that** [**use cases are first-class citizens of your app**](https://medium.com/codex/avoiding-code-hotspots-a-use-case-driven-approach-2bcc12e4b878).

![](https://miro.medium.com/max/557/1*pLm7pmZyNjd5kZzGreUDlg.png)

A use case is like an algorithm to accomplish a client-driven task ([Clean Architecture for the rest of us](https://pusher.com/tutorials/clean-architecture-introduction#conclusion))

Use cases should bear no dependency on the way they’re delivered to the outside world (e.g. GUI, CLI). They solely depend on entities and abstractions of adapters. Use cases should be [pure](https://en.wikipedia.org/wiki/Pure_function), which is why you should isolate all side effects and nondeterministic things into adapters (e.g. updating status, network calls, reading the system clock, and id generators).

➡️ **_Entities_** are business objects as they reflect the concepts that your app manages (e.g. _Account_, _Deal_, _Movie_). There’s a common belief that [entities don’t contain logic but that’s wrong](https://www.martinfowler.com/bliki/AnemicDomainModel.html); entities have logic that relates directly to them.

![](https://miro.medium.com/max/282/0*P5bZfNpA_e777aAc.png)

Logic in entities is potentially reusable across use cases _(_[_Clean Architecture for the rest of us_](https://pusher.com/tutorials/clean-architecture-introduction#conclusion)_)_

![](https://miro.medium.com/max/700/1*jAH06pIzNh1scLVkU1Gjwg.png)

A use case usually deals with one or more entities. Use cases are also known as interactors since they can interact with one or more adapters to get the job done.

Use cases deal with entities, but entities don’t depend on anything else. Both use cases and entities contain business validation rules (i.e. semantic rules, also known as _domain invariants_). For example, “_a loan’s due date can’t surpass 30 years_”.

The domain contains other elements like events, [value objects](https://medium.com/codex/you-should-be-using-value-objects-568b19b1df8d) (e.g. `Email`, `Point`) and enums (e.g. `PaymentType`) and all that represents business domain concepts, but **never any reference to technology**, such as REST, JSON, networking, file system, ORM, SQL, MVC, frameworks, templating engines, and environment context (e.g. env vars).

> Core code doesn’t need a specific environment to run in, nor does it have dependencies that are designed to run in a specific context only. [_Advanced Web Application Architecture_](https://www.goodreads.com/book/show/54179859-advanced-web-application-architecture)

Database tables, ORM entities, DTOs, or GUI concepts are **not** domain entities. [DTO](https://en.wikipedia.org/wiki/Data_transfer_object)s only serve for transporting data; they contain no logic and don’t mean much to the business — they’re implementation details (e.g. read/write models, serializers, view models, etc.). Also, **don’t** use [ORM](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) entities in the domain as dirties it with technology.

# Stage 3: primary and secondary adapters

Recall that adapters are the mediators between the outside world and the domain (i.e. core app). We can categorize them into _primary_ and _secondary_:

➡️ **_Primary adapters_** are entry points of your app operated by _primary actors_ such as users, other systems, and automated tests. They are _‘driving adapters’_ since they trigger the domain code. Primary adapters include APIs, GUIs, CLIs (they’re all **_i_**_nterfaces_), workers, data migrations, and other kinds of jobs. They are also known as _delivery mechanisms_ because that’s the only way your app’s value can be delivered to its actors — every interaction with your app comes through them.

➡️ **_Secondary adapters_** connect your app to _secondary actors_ like databases and third-party services. They are ‘_driven adapters’_ since the domain triggers their usage. A secondary adapter represents a view of the world from your app’s perspective. This helps to insulate your code from changes outside of your control and therefore supports teams during contract changes since they represent single places of change. Typical examples include API clients, cloud storage clients, database adapters, reading env vars and the system clock, loggers, and monitors.

![](https://miro.medium.com/max/700/0*HtThP1bV7F_jIdKK.png)

(Source: [Hexagonal Architecture, there are always two sides to every story](https://medium.com/ssense-tech/hexagonal-architecture-there-are-always-two-sides-to-every-story-bc0780ed7d9c))

# Stage 4: ports and the dependency rule

Recall that the “inside can’t depend on the outside”. According to the [_dependency inversion principle_](https://en.wikipedia.org/wiki/Dependency_inversion_principle) (one of the [SOLID principles](https://en.wikipedia.org/wiki/SOLID)):

> \[…\] stable software architectures are those that avoid depending on volatile concretions, and that favor the use of stable abstract interfaces. [_Clean Architecture_](https://www.goodreads.com/book/show/18043011-clean-architecture)_, Chapter 11_

In other words, the domain/core shouldn’t directly depend on any adapter. But wait a minute: use cases need to rely on repositories, gateways, and other adapters. Any output/secondary adapter has this problem (for input/primary ones, the dependency points inwards). The solution is an output port.

➡️ A **_port_** defines a boundary to an external party. It defines a communication language that exposes what’s relevant to your domain, in your domain language: a port is comprised of an interface, the input and output types ([DTO](https://en.wikipedia.org/wiki/Data_transfer_object)s), and the possible [errors](https://medium.com/codex/pragmatic-exception-handling-3831f7ce0980). Since ports are only the language, your app needs concrete implementations — the adapters. Depending on the language, you may [inject](https://medium.com/codex/dependency-injection-back-to-the-basics-a52402890fdc) them by an interface implementation, compatible lambdas, or compatible objects ([duck typing](https://en.wikipedia.org/wiki/Duck_typing)).

![](https://miro.medium.com/max/700/1*YpcFmWZlu7MIkl86Y1y7aw.png)

Ports should belong to your domain; they abstract communication with the outside by preventing a hard dependency on a concrete adapter.

Here's an example of a repository port:

⚠️ **_Never expose your entities to the outside world._** _Entities should live inside the domain. They can still go to the adapters but if you need to externalize them (e.g. JSON), use proper serializers (known as presenters). Otherwise, you are coupling the domain with the outside world and you may be exposing sensitive information._

Beware not to confuse the flow of control with the dependency rule: the flow of control describes how the program flows: user → device (e.g. browser) → primary adapter (e.g. web handler) → use case → secondary adapter (e.g. repository) → device (e.g. database) → and back to the user. The dependency rule states that dependencies should point inwards.

![](https://miro.medium.com/max/700/1*wSGzNNYOJElQLPaxGoYAcA.png)

Primary/driver adapters (delivery mechanisms) and secondary/driving adapters

# Stage 5: requests and responses

We’ve been calling the use cases and ports with entities and primitive values. However, those options can quickly become problematic as parameters pile up. If your language doesn’t have [named parameters](https://en.wikipedia.org/wiki/Named_parameter), the solution is to create a [parameter object](https://wiki.c2.com/?ParameterObject) (a request model).

The problems with passing entities or primitive values to use cases (and adapters)

➡️ [**_Request/response models_**](https://en.wikipedia.org/wiki/Request%E2%80%93response) are [data transfer objects](https://en.wikipedia.org/wiki/Data_transfer_object) that carry the data to and from the use case. They play a role in [code self-documentation](https://medium.com/codex/towards-self-documenting-code-371364bdccbb). Some request models are ‘write models’ as they carry data downstream (e.g. to be written); some response models are ‘read models’ as they carry data upstream (e.g. to be shown).

![](https://miro.medium.com/max/700/1*bAXgQaZLgkMK4z01IjZX2w.png)

The small boxes inside the ports and the use cases represent request/response models.

Regarding outputs from use cases, you’d create a response model — a read model for the output. It can hold multiple pieces of data (e.g. in pagination, a response with the rows data optimized for reading, the page, total rows, and other metadata).

Adapters potentially need their response models as well — which you store in a port, in the domain. For example, you should have response types to represent third-party API calls. As a second example, you should never return a database-specific row type; sometimes an entity is enough but other times you need a custom response. This prevents leaking technology into the domain.

📝 _Keep request/response models in context. I usually put them as inner classes of their owner which can be a use case or a port. That way,_ [_the context helps to document them_](https://medium.com/codex/towards-self-documenting-code-371364bdccbb)_._

# Composition root

How do we put all this together? We separate the assembling of the app from the app itself. This means loading the configuration (e.g. env vars), creating the dependencies, wiring them, and booting the app. All this should happen outside of the circles, at the [composition root](https://blog.ploeh.dk/2011/07/28/CompositionRoot/) and the app shouldn’t know anything about it.

![](https://miro.medium.com/max/700/1*Ai6m0vLruwR8RteEWFG_9A.png)

The clean architecture has nothing to say about the codebase structure, but we can still reflect it on the way we organize it. The picture shows only a possible way of doing it.

[

## Dependency Injection — Back to the Basics

### DI ensures that components have their dependencies available without knowing anything about their creation. A…

medium.com

](https://medium.com/codex/dependency-injection-back-to-the-basics-a52402890fdc)

# Error handling

I wrote [an article about this topic](https://medium.com/codex/pragmatic-exception-handling-3831f7ce0980), so I won’t go into details.

[

## Pragmatic exception handling

### I’ll present a simple and practical approach to error management, based on my experience.

medium.com

](https://medium.com/codex/pragmatic-exception-handling-3831f7ce0980)

# Testing

We’ve now introduced the necessary concepts to talk about automated testing:

[

## A testing strategy for a domain-centric architecture (e.g. hexagonal)

### I’ll propose a testing strategy for the hexagonal architecture.

medium.com

](https://medium.com/codex/a-testing-strategy-for-a-domain-centric-architecture-e-g-hexagonal-9e8d7c6d4448)

# _Conclusion_

📝 _Proceed to Part II, where I talk further about use cases:_

[

## Implementing Clean Architecture — The use cases

### I’ll present my approach to avoid code hotspots and explain what user-centered design and the screaming architecture…

medium.com

](https://medium.com/codex/avoiding-code-hotspots-a-use-case-driven-approach-2bcc12e4b878)

My favorite aspect of a domain-centric architecture is the standardization that it brings into the codebase. Following patterns helps new developers change and create use cases. It’s harder to make mistakes like adapters directly calling other adapters — you’ll quickly remember the concentric circles and the dependency rule. When creating new components, there’s hardly anything else other than adapters, use cases, and entities — all the rest should be private. This creates a concise API with a small surface area to use in tests and implementation.

More stages could have been examined (some people consider an application sublayer within the domain), but this was an introductory article; what mattered to me was to show you the set of [mental models](https://en.wikipedia.org/wiki/Mental_model) you can use as a learning path. The stages are also a possible path to evolving a simple app into a more complex one. I hope that you take these as takeaways:

- your app is comprised of a **domain** (core) and an **infrastructure** (I/O). The domain maps the business (higher-level code); the infrastructure represents the technology (lower-level code).
- libraries and frameworks should live outside the domain. The domain should be as pure as possible and make use of the [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html).
- **the dependency rule**: source code dependencies can only point inwards (e.g. a use case cannot reference a concrete adapter).
- **adapters should ideally be replaceable**: it makes everything more testable and reduces the buy-in into specific technologies.

# Learn more

- Sample projects — [Kotlin](https://github.com/lsoares/clean-architecture-sample); [Python](https://github.com/lsoares/domain-driven-arch-python)
- [The Clean Coder](https://www.youtube.com/watch?v=NeXQEJNWO5w) (Bob Martin)
- [Hexagonal architecture](https://hexagonalarchitecture.org/) (Alistair Cockburn)
- [Advanced Web Application Architecture](https://www.goodreads.com/book/show/54179859-advanced-web-application-architecture) (Matthias Noback)
- [Modern Software Engineering](https://www.goodreads.com/book/show/59517038-modern-software-engineering) (David Farley)
