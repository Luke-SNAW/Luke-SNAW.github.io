---
id: cdgkaoy6064zew14hry05b3
title: A primer on functional architecture
desc: ""
updated: 1667865354007
created: 1647565553197
tags: architecture
---

https://increment.com/software-architecture/primer-on-functional-architecture/

_This article is based on chapter 3 of_ [Domain Modeling Made Functional](https://pragprog.com/book/swdddf/domain-modeling-made-functional) _by Scott Wlaschin._

Many articles on functional programming, or FP, focus on low-level coding practices (such as avoiding side effects) and FP-specific patterns (such as the dreaded monad). They don’t, however, touch on high-level design and architecture. Yet FP principles can be applied at larger scales. In fact, many popular frameworks and architectural styles, from serverless on the backend to Redux/Elm-style frameworks on the frontend, have their roots in functional programming.

When used appropriately, FP principles can reduce complexity while increasing the testability and maintainability of an application. This is functional architecture.

## The principles of FP applied to software architecture

In a functional architecture, the basic unit is also a function, but a much larger business-oriented one that I like to call a workflow. Each workflow represents a unit of functionality—a feature, use case, scenario, story, or whatever you want to call it.

Composition is the primary way to build systems. Two simple functions can be composed just by connecting the output of one to the input of another. The result is another function that can be used as a starting point for yet more composition.

Composition is such an important concept that functional programmers have a suite of standard tools, such as monads, that allow for composition even if the inputs and outputs don’t quite match.

This compositional approach means we only combine the specific components we need for a particular business workflow. There is no need for a traditional layered architecture. As we add new features to our system, the functionality required for each new workflow is defined independently, rather than grouped into a database or services layer.

Functional programmers try to use pure functions as much as possible. A pure function is deterministic (a given input always results in the same output) and has no side effects (such as mutation or I/O). They are very easy to test (deterministic!) and easy to understand without drilling into their implementation (no side effects!).

## Interacting with the outside world

Of course, at some point we will need to do I/O. Functional programmers try to keep this kind of nondeterminism at the edges of the pipeline as much as possible.

This functional model is very similar to well-known approaches such as [onion architecture](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/), [hexagonal architecture](http://www.dossier-andreas.net/software_architecture/ports_and_adapters.html) (a.k.a. ports-and-adapters architecture), and [functional core, imperative shell](https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell). In all cases, the core domain—the pure business logic—is isolated from the infrastructure. The infrastructure code knows about the core domain, but not the other way around. Dependencies are one-way only and I/O is kept at the edges.

Using only pure code for the business logic means there’s a clear distinction between unit testing and integration testing.

One of the advantages of functional programming is that this isolation of business domain from infrastructure occurs naturally.

## Boundaries and contexts

As software designers and architects, our next challenge is to decide how to group these workflows or pipelines into logical units.

In DDD terminology, a grouping of related functionality is called a bounded context, and each bounded context is treated as a mini-domain in its own right. It typically corresponds to the logical encapsulation of a particular business capability. We use the phrase “bounded context” instead of something like “subsystem” because it keeps us focused on what’s important when we’re designing a solution: being aware of the context and the boundaries. (Exactly how to define these bounded contexts is a topic for another article.)

Why context? Because each context represents some specialized knowledge or capability. Within the context, we share a common language, and the design is coherent and unified. But, just like in the real world, information taken out of context can be confusing or unusable.

Why bounded? In the real world, domains can have fuzzy boundaries. But in the world of software, we want to reduce coupling between subsystems so that they can evolve independently. Boundaries are key to ensuring that subsystems stay separate, and can be maintained using standard software practices such as using explicit APIs and avoiding dependencies such as shared code. In complex projects with changing requirements, we must be ruthless about preserving the “bounded” part of the bounded context. A boundary that’s too broad or too vague is no boundary at all.

Autonomy is a crucial aspect of a bounded context. Having autonomy means that the bounded context can make decisions without needing to wait on decisions or information from other bounded contexts. That is, if one bounded context is unavailable, the other bounded contexts can continue operating independently, which is an important decoupling. Autonomy can also apply to the development process. In general, a bounded context is best owned by a single team.

If we apply the concept of bounded contexts to a functional architecture, we end up with a number of small, focused domains, each of which supports a number of business workflows. These boundaries should be defined in such a way that the workflows within them are autonomous, able to do their job without depending on other systems.

In some cases, a long-running use case or scenario requires multiple workflows. In this case, workflows in different contexts will need to communicate with each other using events and other methods. However, it’s important to keep an individual workflow within a single bounded context and never attempt to implement a scenario “end to end” through multiple contexts. Allowing workflows to reach inside multiple services will eventually cause our nicely decoupled architecture to devolve into a tangle of unmaintainable dependencies—“[a big ball of mud](http://laputan.org/mud/).”

## The entity-service antipattern

There may not be one right way to define boundaries, but there are certainly many wrong ways. A common antipattern for grouping functionality is the [“entity-service” approach](https://www.michaelnygard.com/blog/2017/12/the-entity-service-antipattern/), in which the services are built around entities instead of workflows.

Just because a business workflow involves an entity, such as an “order,” doesn’t mean it has anything in common with other workflows that use that entity. For example, the “pay for an order” workflow and the “delete an order” workflow both involve orders but have completely different business logic.

## Events

Now our workflow functions are grouped into bounded contexts and ready to be used. But what triggers these business workflows? What causes an employee, user, or automated process to initiate a workflow?

An event. That is, something changes in the outside world—a customer clicks a button, an email arrives, an alert pops up. This is captured in the form of a business event—for example, “order placed” or “email received.” In an FP architecture, business events like these trigger workflows.

Furthermore, with this approach, the output of a workflow is also an event: a notification that tells any downstream workflows that something important has changed in the world. Changes that are specific to a particular workflow and aren’t shared, such as database updates, aren’t emitted from the workflow as events.

This is how we can assemble larger processes from these smaller workflows. Each workflow is triggered by an event, and that workflow in turn generates more events for downstream processes to consume.

Note that in all cases the workflows interact asynchronously. This allows them to stay independent and decoupled in both time and space.

If you’re familiar with [event-driven architectures](https://www.enterpriseintegrationpatterns.com/docs/EDA.pdf), this event-based approach will be familiar. And, indeed, the FP approach of having individual pipelines is very amenable to this architectural style.

## Logical versus physical architecture

It’s important to note that this description of separate workflows triggered by events is a logical view, not a physical one.

## Frontend functional architecture

...

The most common functional frontend architecture is the Model-View-Update architecture, also known as the Elm architecture.

## The power of functional programming principles

Many good practices of software architecture—cohesion, decoupling, isolation of I/O, etc.—arise naturally from applying functional-programming principles. For example, we’ve seen that in a typical functional design each workflow is constructed independently, comprising only the functionality it needs (which maximizes cohesion), and that autonomy is emphasized at all levels, from individual functions up to bounded contexts (decoupling). Furthermore, a surefire way to enhance testability and maintainability is to keep the business logic in pure, deterministic functions, and to use immutable data models to force data changes to become explicit and unambiguous.
