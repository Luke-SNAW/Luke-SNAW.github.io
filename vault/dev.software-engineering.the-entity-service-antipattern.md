---
id: tgud80cj6687x0o11ht4sn6
title: The Entity Service Antipattern
desc: ""
updated: 1684906080738
created: 1684902641408
---

> https://www.michaelnygard.com/blog/2017/12/the-entity-service-antipattern/

In my [last post](http://www.michaelnygard.com/blog/2017/11/keep-em-separated/) I talked about the need to keep things separated once they've been decoupled. Let's look at one of the ways this breaks down: entity services.

If a pattern is a solution to a problem in a context, what is an antipattern? An antipattern is a commonly-rediscovered solution to a problem in a context, that inadvertently creates a resulting context we like less than the original context. In other words, it's a pattern that makes things worse (according to some value system.)

I contend that "entity services" are an antipattern.

To make that case, I need to establish that "entity services" are a commonly-rediscovered solution to a problem and that the resulting context is worse than the starting context (a monolith.)

Let's start with the "commonly-rediscovered" part. Entity services are in Microsoft's [.NET microservices architecture ebook](https://docs.microsoft.com/en-us/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/data-driven-crud-microservice). Spring has a [tutorial with them](https://spring.io/blog/2015/07/14/microservices-with-spring). (Spring may give us the absolute easiest way to create an entity service. The same class can be annotated with JSON mapping and persistence mapping.) RedHat has a [Microservice Reference Architecture](https://www.redhat.com/cms/managed-files/mi-microservices-eap-7-reference-architecture-201606-en.pdf) with product-service and sales-service. Some of the microservice-focused frameworks such as [JHipster](http://www.jhipster.tech/) start with CRUD on data entities.

In order to make the case that the resulting context is worse than the starting context, I need to assume what that starting context actually is. For the sake of generality, I'll assume a largish, legacy application that is more-or-less a monolith. It may call out to some integration points to get work done, but features are pretty much local and in-process. There are multiple instance of the process running on different hosts. Basically, like the following diagram.

![](/assets/images/software-engineering/the-entity-service-antipattern__monolith.svg)

All features reside in the code for the application instances.

Many other authors have enumerated the sins of the monolith, so I won't belabor them here. (Though I feel compelled to make a brief aside to say that we did somehow deliver quite a lot of working, valuable features that ran in monoliths.)

How might we describe this initial context?

- It is clear where the code to build a feature goes and how to test the code.
- The release cadence is dictated by the slowest-delivering subteam.
- There is little inherent enforcement of boundaries, thus coupling tends to increase over time.
- Performance problems can be found by profiling a single application.
- The cause of availability problems is typically found in one place.
- Building features that rely on multiple entities is straightforward, though it may come at the cost of inappropriate coupling.
- As the code grows large, the organization is at risk of entering [the fear cycle](http://www.michaelnygard.com/blog/2015/07/the-fear-cycle/).
- Feature availability may be compromised by inappropriate coupling via common modes in the application. (E.g., thread pools, connection pools.)
- Feature availability should be improved by redundancy of the whole application itself. This is reduced, however, if the application is vulnerable to the surrounding environment, as in the case of a Self-Denial Attack, memory leak, or race condition.

Supposing we move this to a microservice architecture, with entity services. We might end up with something like this example from the Spring tutorial:

![](/assets/images/software-engineering/the-entity-service-antipattern__with-entity-services.svg)

In this version, you should assume that each of the service boxes comprises multiple instances of that service.

Obviously there are more moving parts involved. That immediately means it's harder to maintain availability.

The challenges of performance analysis and debugging are well documented, so I won't belabor them.

But in this resulting context, where do features get created? A few of them are direct interactions of the "Online Shopping" service and the individual entity services. For example, creating an account is definitely just between Online Shopping and Accounts.

Most features, however, require more than one of the entities. They will use aggregates or intersections of entities.

For example, suppose we need to calculate the total price of a cartful of items. That involves the cart, the products (for their individual prices) and the account to find the applicable sales tax or VAT. I predict that it will be implemented in the Online Shopping service by making a bunch of calls to the entity services to get their data.

We can depict this with an "activation set" (a term I made up) to show which services are activated during processing of a single request type. For this picture, we focus on just the services and elide the infrastructure.

![](/assets/images/software-engineering/the-entity-service-antipattern__activation-set-es.svg)

So to price the cart, we have to activate four of the five services in our architecture.

That activation represents operational coupling, which affects availability, performance, and capacity.

It also represents semantic coupling. A change to any of the entity services has the potential to ripple through into the online shopping service. (In particularly bad cases, the online shopping service may find itself brokering between data formats: translating version 5 of the user data produced by Accounts into the version 3 format that Cart expects.)

A common corollary to entity services is the idea of "stateless business process services." I think this meme dates back to last century with the original introduction of Java EE, with entity beans and session beans. It came back with SOA and again with microservices.

What happens to our picture if we introduce a process service to handle pricing the cart?

![](/assets/images/software-engineering/the-entity-service-antipattern__activation-set-es2.svg)

Not much improvement.

Bear in mind this is the activation set for just one request type. We have to consider all the different request types and overlay their activation sets. We'll find the entity services are activated for the majority of requests. That makes them a problem for availability and performance. It also means they won't be allowed to change as fast as we'd like. (Services with a high fan-in need to be more stable.)

So, let's look at the resulting context of moving to microservices with entity services:

- Performance analysis and debugging is more difficult. Tracing tools such as Zipkin are necessary.
- Additional overhead of marshalling and parsing requests and replies consumes some of our precious latency budget.
- Individual units of code are smaller.
- Each team can deploy on its own cadence.
- Semantic coupling requires cross-team negotiation.
- Features mainly accrue in "nexuses" such as API, aggregator, or UI servers.
- Entity services are invoked on nearly every request, so they will become heavily loaded.
- Overall availability is coupled to many different services, even though we expect individual services to be deployed frequently. (A deployment look exactly like an outage to callers!)

In summary, I'd say both criteria are met to label entity services as an antipattern.

Stay tuned. In [[dev.software-engineering.services-by-lifecycle]], we'll look at what to do instead of entity services.
