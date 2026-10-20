
> https://itnext.io/rest-graphql-or-rpc-a-decision-paralysis-0acaa84b5a27

...

## Conclusions

API design is a difficult choice that should be driven by a product discovery phase, where you understand the innate nature of your application, and other actors in the system.

Finger to the wind.

Use **REST** if:

- you are building an API to interact with your database using CRUD operations
- your data model is not heavy on relations
- you have a limited number of user roles and access requirements

Use **GraphQL** If:

- you are building a gateway to connect multiple data sources or services
- your data model is heavy on relations and represents a graph
- you have high-granularity access requirements
- you are building an API targeted mostly at front-end applications
- you have a large number of API clients with varying data requirements

Use **RPC** if:

- you want to be flexible in naming and routing conventions
- you want to build semantic, easy to read APIs
- you need to address diverging, volatile, or complex use cases
- your services interact outside of the HTTP protocol
- you want to build a robust future-proof API decoupled from implementation and data storage concerns

If you ask for my personal opinion, I think the future is RPC. I love GraphQL for front-end development, but I don’t think it’s an ideal solution for cross-service communication, and once you tip your toes into it it bites your foot off, and makes things so much harder to reason about. By all means, use GraphQL as a proxy for your read-model, but don’t bring it into a mix as part of your internal services. And as for the REST, let it rest.

---

Ever since AJAX capabilities landed in our browsers some 20+ years ago, developers around the world had been busy pushing these technologies to their limits, engineering creative ways of challenging the foundations of the original internet, and transforming it from a web of static pages to a web of dynamic data flows.

Application programming interfaces (APIs) that power all this data exchange have gone through many iterations, and it’s unsurprising that in 2023 many development teams struggle with decisions about the design and implementation of their APIs. With a variety of programming languages, transfer protocols, and infrastructure architectures, finding a way to define reliable contracts for data transfer, and more so to implement and maintain them in the face of changing requirements, is no easy feat.

Dealing with APIs on a daily basis, and observing the discussions around their design in my professional circles, it appeared to me it would be useful to put down some of my thoughts in writing. With **REST**, **GraphQL** and **RPC** being the most commonly discussed design patterns, I will focus on those and summarise some of my thoughts and experiences. Having worked with all 3 of them, I realise there is no silver bullet, and I think we are a long way away from having a common ground, similar to W3C standards, which helped bring sense and structure to browser technologies.

Before we start, let me clarify some of the assumptions:

- In a way, treating these 3 paradigms as equals is like comparing apples to oranges. After all, GraphQL is just a query language specification and could be instrumented in a way that is very similar to an RPC gateway. On the query side of things, it is also very similar to REST with it’s focus on resources, and in fact nothing prevents you from sending GraphQL documents as part of your REST calls, and use field resolvers as part of your controller implementation. So, for the sake of this article, I will be thinking of GraphQL as an implementation of the specification, i.e. a server akin Apollo capable of receiving and serving data over HTTP.
- Speaking of RPC, I am not referring to any specific implementation, such as [gRPC](https://grpc.io/), but rather a paradigm of using procedure calls instead of operating on resources with unique addresses in the network, as is common in REST. Even though I intend to draw parallels with other transfer protocols, for the purposes of this article, API will stand to mean data transfer over HTTP. I will put aside networking considerations to focus on actual API design rather than mechanics of data moving over the wire. As such, it’s best to think of an RPC implementation similar to [JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC) or [tRPC](https://trpc.io/) rather than gRPC (with its use of HTTP/2 for bidirectional streaming of binary data).

Let’s look at the various aspects of API design that need to be considered when making a decision and see how the 3 patterns hold up against these requirements.

## Schema Definition

Ability to express APIs in abstract terms using a schema definition language (SDL) is an important consideration to make when choosing our API design. SDLs allow us to detach our design from implementation details, focus on our data model, and express a contract in a way that is interoperable throughout a variety of clients that could be interacting with our API in the future. SDLs make it easier to build tooling to automate some of otherwise painstakingly manual processes, e.g. by generating client SDKs or types for our data transfer objects.

Working without an SDL is a deal breaker, as you end up having to maintain a set of documentation in some random format that will be difficult to keep up to date, evolve and communicate to API clients.

When evaluating an SDL consider what your development workflow is going to look like:

- **Schema-first approach** is practical for larger teams that deal with organisational complexity. Various teams can work together on defining the contract before moving forward with the actual implementation. This approach requires more time in planning and communication, but as a result allows the teams to work independently and in parallel, not having to deal with varying implementation schedules. This also results in better code quality as such a development flow requires mocks and tests to be feasible, perhaps even pushing development towards TDD. An added benefit of schema-first approach is that it’s agnostic to actual implementation details — underlying technology can always be swapped without affecting the workflow or impacting the clients. Using this approach however does require that everyone learn to speak a new language, so the syntax and usability are quite important considerations.
- **Code-first approach** is more practical for smaller teams that want to maintain agility, while having some level of contractual safety between clients and benefiting from the tooling within the SDL ecosystem. Code-first approach is tightly coupled with the tooling chosen for the development, and it comes with a risk of a costly effort that would be required to switch to a schema-first approach some time in the future, e.g. when the tools are no longer maintained by their authors, or the growing organisational complexity prevents the team from collaborating efficiently.

**GraphQL** in its essence is an SDL specification, which makes it a good candidate for expressing APIs. It has a built-in support for defining procedures (queries and mutations), input and response object types.

**REST** and **RPC** are abstract concepts and do not have a standard SDL, but there are several general purpose frameworks that can be used to describe HTTP-based APIs.

- [OpenAPI](https://www.openapis.org/) (formerly Swagger) is the most common SDL specification that allows API authors to express HTTP requests and responses in YAML or JSON. OpenAPI ecosystem features a number of [cool development tools](https://openapi.tools/)[.](https://openapi-generator.tech/)
- [AsyncAPI](https://www.asyncapi.com/) is another option to consider for **RPC** and other systems that focus on exchanging messages rather than resources. Its syntax is similar to OpenAPI, but it can better express the needs that go beyond the HTTP protocol.

APIs expressed through SDLs also help us address type safety and serialisation concerns, making contracts enforceable throughout our stack. There are several serialisation and validation patterns that we can build on top of our specs.

- [Protocol Buffers](https://protobuf.dev/) is a platform and language neutral mechanism to serialize structured data. Models expressed in OpenAPI can be exported into protobuf format with [gnostic](https://github.com/google/gnostic) making it easier to reliably exchange data between the server and the clients.
- [JSON-Schema](https://json-schema.org/) is another standard for expressing serialisable data, as well as validation requirements for such data. OpenAPI specs could be converted to JSON-Schema using [converters](https://github.com/openapi-contrib/openapi-schema-to-json-schema). It’s an interesting approach if you want to validate your data at various stages of the request lifecycle.
- [Modelina](https://modelina.org/) and other tools can be used to generate models from OpenAPI, AsyncAPI, and JSON-Schema.

When defining your schema, you may also want to explore existing conventions that ensure that your API design is as compatible as possible with other systems you may want to integrate with in the future.

- [JSON-RPC](https://www.jsonrpc.org/specification) is a convention for structuring your RPC messages.
- [cloudevents](https://cloudevents.io/) is a broader attempt to find a common language when documenting events in various formats and can be useful for various RPC considerations.
- Consider various filtering, sorting, and pagination conventions that already exist, e.g. [SCIM](https://datatracker.ietf.org/doc/html/draft-ietf-scim-api-12#section-3.2.2.2), [OData](https://docs.oasis-open.org/odata/odata/v4.01/odata-v4.01-part2-url-conventions.html), [CQL](https://portal.ogc.org/files/96288#cql-core).

Other things to keep in mind when dealing with SDL:

- does it allow you to describe your resources in a manner that would allow any client to easily understand the logic, resources and relationships
- does it allow you to express authentication requirements and accessibility of resources based on client roles/permissions
- does it support all the data types (scalars, enums and complex unions) that your application would require
- does it have the tooling necessary to serialise data in a format suitable for the HTTP (e.g. URL query and JSON) and other protocols
- does it allow you to express your data model, resources and procedures beyond the HTTP protocol, i.e. you would prefer to use the same SDL to describe data transfer in other communication protocols (such message queues, or even command line interfaces)

The great thing about the SDL is that it can serve as documentation for your API, both internally and externally. Making the schema accessible to the clients makes it possible for them to introspect the schema to discover the available resources within your API. There are wonderful GUI playgrounds that allow you to explore and interact with GraphQL (e.g. [Apollo Studio)](https://studio.apollographql.com/sandbox/explorer/?) and OpenAPI (e.g. [Swagger UI)](https://swagger.io/tools/swagger-ui/) schemas. And of course they integrate well with our beloved [Postman](https://www.postman.com/), allowing us to create collections from schema definitions, and even export collections into some of the common SDLs.

## Data Model

A decision about API design can not be made without a good understanding of the specifics and complexity of the underlying data model, and the needs of the clients in accessing the resources.

### Object-relational complexity

Relational model complexity is a major concern in API design, as traversing complex relational models via an API can be difficult. Relations that exist between your domain entities could be a deciding factor in favour or against a specific approach.

In a standard **REST** implementation, each resource has it’s own unique network address. You can access a resource with a straightforward `GET` request, e.g. `GET /users/1`. Things get murkier when you try to represent collections and relations, e.g. to get a list of user’s friends you would go to `GET /users/1/friends`, then however it gets ambiguous if you want to get a specific friend: it’s quite unclear whether you access it via `GET /users/1/friends/friendship-1` or `GET /friendships/friendship-1` or `GET /users/2`. It is also unclear where you should put your nested documents, e.g. should a user address be returned as part of the user resource, or should it be it’s own resource living on the `GET /user/1/addresses` edge. Such ambiguity plaques development teams with endless decisions about domain boundaries and their representation in the `REST` graph. Compromises are made between domain model uniformity and performance, making it hard for API clients to know exactly where to look.

Aside from that, **REST** places the burden of traversing the graph on the API client. If you ever tried to resolve a list of second-degree relations, you know what a nightmare it is, with a cascade of hundreds, if not thousands, of API requests. On top of it, if you are dealing with bidirectional relations, you have to account for node repetition as well as circularity, making it the responsibility of the client to implement some form of caching and deduplication to avoid infinite loops.

In order to alleviate some of this pain, REST API authors resort to creative solutions (a.k.a hacks) that allow relations to be resolved when a resource is requested. For example, Stripe API uses `expand` parameter. This does address the traversal concerns, but leads to non-deterministic response types, which again have to be dealt with by the API client, forcing it to do lots of type juggling and coercion.

With the emergence of social networks and their complex social graphs, **REST** had become quite unmanageable. **GraphQL**, as the name suggests, was created by Facebook as a way of traversing a complex social graph, representing an entirety of human society with its six degrees of separation. Facebook was trying to solve a problem inherent to social complexity with a multitude of actors and multidirectional relationships between them, and you should keep that in mind when evaluating whether or not your API design might benefit from it.

**GraphQL** is brilliant in its simplicity. By letting the client specify precisely what data it needs and fetch it in a single request, it shifts the responsibility of traversing and stitching the graph to the server. Embedding types and relations within the schema design, it can use field resolvers to extract the necessary data and traverse the query of any complexity. This doesn’t always come cheap, and leads to additional problems and tooling (e.g. data loaders to address the n+1 problems), but allows the server to use any number of data stores to aggregate properties and relations, making API clients agnostic to such implementation details.

At their core, both **REST** and **GraphQL** are focused on resources and their representation. This is usually tightly coupled with how we represent entities in our databases. In a sense, these entities always exist in their platonic form, regardless of who the observer is. This can be problematic in certain systems, where not all clients are created equal. Having a static schema or a graph that doesn’t account for use cases and requester roles can lead to all kind of issues in the design. Presume our employee model has a salary property which can only be accessed by an accountant role — how do we represent and implement this in our API design? Do we make the property optional? If it’s optional how do we know what the lack of a value represents (there is no data in the storage or there is no accessible data for this requester). Do we create another edge in REST that throws an HTTP error? Do we send null or an error in GraphQL? This ambiguity can lead to additional complexity and uncertainty on the client-side, and should be factored in at the API design stage.

Resource-centric approach to our API design tends to make us think about our APIs in terms of our data storage model. While it’s justified in some cases, it can be problematic if we couple our API too tightly with our databases. All too often, we reuse our ORM models as our API models, and rely on tools such as [Hasura](https://hasura.io/), [Prisma GraphQL](https://www.prisma.io/graphql), [PostgREST](https://postgrest.org/en/stable/index.html), and many others to interface directly with our database via API. These tools can save a great deal of time, but they blur the lines between the architectural layers, and make our API clients susceptible to breaking changes. Depending on how and where the clients are used, such an approach poses a risk to data integrity, and requires a solution to rectifying race conditions of running data and schema migrations, generating and tagging new SDK versions, and propagating the changes to all the clients. API versioning becomes an issue if data storage engine does not support any versioning. Aside from that complex access controls become a pain point requiring us to hook into these tools to manage roles and permissions.

**RPC** on the other hand is unopinionated about resources and their representation. It allows API authors to move away from trying to reproduce the data model and instead focus on use cases — procedures can be tailored towards specific needs of the clients and actors in the system. Unlike REST, where the client hardly has any say in what it gets, and GraphQL, where the client can indiscriminately request as much data as it wants (vis Cambridge Analytica), RPC can accommodate various requirements arising from different API applications. RPC servers can be instrumented in a way that rips the best from all worlds — from resolvers to untangle the graph to routing middleware to manage the request/response flow to isomorphic route and query level permission controls. RPC API can be built around immutable contracts and evolve over time to address changing requirements in a backward compatible manner. RPC allows us to separate API concerns from data persistence/storage concerns and other implementation details, leading to a more future-proof API design that doesn’t have to change every time the data schema changes.

While GraphQL is a good solution for a larger API surface, where the needs of the clients can not be well predicted, RPC could be a good alternative for smaller projects — essentially, instead of making the client write queries and enumerate all fields that have to be returned to the client, the response type could be explicitly defined as part of the RPC schema. In essence, the same could be said about REST, but that goes against the nature of the paradigm that dictates that each resource should be available at its own network locator.

### Updating Data

Let’s be honest, when it comes to updating data via **REST**, it’s a pain in the ass. Different HTTP methods that are supposed to make things transparent, instead raise all kinds of questions:

- what method should be used to soft-delete or archive a resource? Should it be a `DELETE` request with some flag, or `POST` request with an action name (in effect making it an RPC request?), or should it be `PATCH` request updating the `deleted` or `archived` property of an object?
- what about partial updates? Should we use `PUT` or `PATCH`? What about updates that have specific side effects, e.g. changing account email? Should they still go into a `PATCH` request, or be sent as `POST` with an action name?
- what about granularity of partial updates where certain actors are only allowed to make certain changes? How do we split and describe this logic in our REST API design?
- what about logic that does not really have any resources attached to it? Where should, for example, the various steps of the password reset flow live? Should they be in the root of the REST API or some edge of the API?
- what happens with nested documents? What if those nested updates require transactional safety?

The fact is, whenever you build an SDK around the REST API, you end up using procedure calls to describe the various actions that it performs, e.g. `deleteUser()` or `capturePayment()` rather than operating with get/post/put/patch/delete methods directly. My personal opinion is that REST is no longer suitable for modern day application design — requirements are far too complex to embed them into opinionated resource-centric API design.

Procedure calls are more suited for the complexity of modern day applications, allowing API designers to address specific use cases rather than trying to accommodate every possible scenario in a limited set of RESTful endpoints. Changing user password, is not the same as changing user email, or opting a user into a newsletter. All three may be part of the same resource, but hardly ever would you update a password and subscribe a user to the newsletter in the same request. All of these procedures have distinct side effects, and may require custom validation and permission checks.

RPC fits in nicely with CQRS principles. You can think of procedure calls as queries and commands, which make transport protocol considerations irrelevant. HTTP controllers receive and validate payloads, and then pass them on to query and command busses. This makes it easy to reuse procedure calls for any other transport — from command line to message queue to chatbots to whatever else that can receive a procedure call.

GraphQL mutations are in fact RPC. Aside from a terrible name that makes me think of unpredictable gene mutations and lockdowns, it is very flexible. The question however remains, what is to be considered a mutation — sending emails or downloading documents are procedures that don’t really mutate anything, so should they be part of the graph at all?

Another important thing to consider in the context of API design is whether or not data updates are synchronous or asynchronous. In distributed systems, synchronicity might not always be an option, so you should plan ahead to figure out a way to communicate persistence events to the API client, and how those are going to be reflected in API schema and documentation. Where your clients live will determine what technology you can use for that: webhooks, WebSockets, [Server-Side Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events), push notifications or something else. Here is an [interesting read](https://github.com/wso2/reference-architecture/blob/master/event-driven-api-architecture.md) on the subject of asynchronous event-driven APIs.

Speaking of distributed systems, we should also consider what implications using GraphQL might have. On one hand GraphQL is well suited for aggregating data from various sources and can be used as a gateway to your microservices. On the other hand, however, mixing GraphQL with other API designs across the stack (or even having multiple GraphQL servers) might become unwieldy. You will need to think about ways to stitch or federate your servers to ensure the integrity of the graph.

### Data Types

When it comes to API design there are a few considerations to make with regards to types of serialisable data that the API is going to transmit:

- how are you going to communicate serialisation requirements for custom scalar types
- how are you going to express mixed types and `oneOf` logic, and how will you discriminate such union types

Not all scalars are created equal. Having an API schema littered with `string` and `number` types is nothing short of a nightmare. A contract should be explicit about the requirements — API clients should not be second guessing what `{ contact: string }` means, especially if there is validation attached to that property:

- use string identities, e.g. `UUID`, `Email`, `IPv6`, `ISBN` etc, and be explicit about custom string patterns
- use integer identities, e.g. `Year`, `Timestamp` etc, and be explicit about ranges for custom integers
- use float identities, e.g. `Lat`, `Long` etc, and be explicit about ranges and precision for custom floats
- use enums to express finite lists of scalar options
- adopt a single date format, i.e. ISO Date string or Unix timestamp

Both GraphQL and OpenAPI support scalar type refinements, but they leave serialisation concerns to the servers and clients, so be sure to account for custom scalar type serialisation in your implementation. GraphQL, unlike OpenAPI, does not offer a native approach to documenting validation requirements at the schema-level, so be ready for some runtime error handling. There are some attempts to use non-standard directives to express [validation constraints](https://github.com/confuser/graphql-constraint-directive/blob/master/README.md) and [formatting requirements](https://github.com/Saeris/graphql-directives#formatdate), but you will need to instrument them yourself.

Another important aspect of modelling data in API design is mixed types. Presume your API is going to serve a catalogue of items available in a library. You may have to deal with books, magazines, films, cassettes, CDs etc, all with their own data model. Depending on the design, your API clients may need to discriminate between these models to infer the correct type to build the logic around it.

OpenAPI spec comes with built-in support for unions of any types. GraphQL on the other hand isn’t so useful when it comes to discriminated unions and mixed types. Mixed scalar types are a no go. While GraphQL supports unions, they should all share the same interface, and should not have overlapping fields of varying types — you will have to work around these constraints and it’s not always possible, so you end up with a scalar `JSON` type, which isn’t that great for type safety.

These limitations are most evident when you work with structured/rich text. If you are working with a Headless CMS that ships a flavour of structured text, e.g. [PortableText](https://github.com/portabletext/portabletext) or [Slate](https://docs.slatejs.org/concepts/10-serializing#plaintext), you will need to think of how to represent these content models in your API schema.

### Filtering, Sorting and Pagination

A standard oversight when designing an API is a standardised approach to filtering, sorting and pagination. As we start with a small dataset we fail to foresee the future with millions of records, and neglect these concerns, which later leads to rebuilding the API schema to accommodate the new requirements.

There is no one standard approach to these concerns and different APIs address them in different ways. Take a look at [SCIM](https://datatracker.ietf.org/doc/html/draft-ietf-scim-api-12#section-3.2.2.2), [OData](https://docs.oasis-open.org/odata/odata/v4.01/odata-v4.01-part2-url-conventions.html), [CQL](https://portal.ogc.org/files/96288#cql-core) for some ideas.

When it comes to filtering, I draw inspiration from [Prisma.io](https://www.prisma.io/docs/reference/api-reference/prisma-client-reference#filter-conditions-and-operators). They have designed a beautiful approach to querying the database, but their approach can as well be applicable to API design. Because these filters are serialisable, they can be easily integrated with HTTP requests, and will cover a wide range of requirements for filtering large datasets.

Pagination design is often dictated by the underlying data model, as well as the amount of traffic the database receives. Datasets that change often might benefit from cursor-based approach, while others can exist quite happily with an offset approach. Here is [an interesting article](https://ignaciochiazzo.medium.com/paginating-requests-in-apis-d4883d4c1c4c) on the subject.

One thing to note here is how we draw a line between `GET` and `POST` requests. Rooted in REST and early-day HTTP principles, this dogmatic allocation of `GET` requests for queries, and `POST` requests for data updates, make working with large filters a headache. If you look at pros of REST approach, it boasts cacheability, but let’s be honest, what was the last time your relied on browser cache or CDN for your API requests. The idea that using URL query parameters instead of body payload would somehow make the world a better place is frankly outdated. URL serialisation sucks. URL length is limited. So, let’s just dispose of this dogma, and use `POST` requests with JSON payloads for all API requests. That’s pretty much what GraphQL clients end up doing as they encounter URL query length limitations. Think of it in RPC terms — you are not getting the data, but you are posting a procedure to the server and receive an answer from it.

## Environment & Tooling

An API design decision can not be made without taking into account what server technologies will be used to serve it, and what clients will be used to access it.

Because REST has evolved alongside the HTTP protocol, it is based on a set of universal standards. The stack is really quite irrelevant — all server and client technologies are able to communicate over HTTP, and the tooling around orchestrating a REST server is quite rich, regardless what programming language or server infrastructure you choose.

RPC implementations vary. There are various frameworks that bring their own ideas to the table. There is [gRPC](https://grpc.io/) that is environment-agnostic, but is quite nuanced with regards to its bi-directional communication and use of Protocol Buffers. There is [tRPC](https://trpc.io/) with its full-stack TypeScript implementation that borrows from REST and GraphQL to create one of the most loved API tools. There is [ZeroC](https://zeroc.com/) and [UCall](https://unum-cloud.github.io/ucall/) and many others. Ultimately, nothing is stopping you from using REST tooling to build RPC APIs — get rid of the brain fart that the REST is and just give all your queries and commands proper names and send them over the wire using standard HTTP tooling. You can namespace your procedures with URL segments, similar to REST, but you don’t have to bake in resource IDs into the URL structure and deal with complexity of HTTP methods.

When it comes to GraphQL, the idea behind it is brilliantly simple:

- each client defines the data it needs using a query language designed specifically for expressing graph nodes in a very simple form
- the server parses the query, and passes each requested field through a resolver that has access to the root node and can access various data stores and/or external services to compute the return value

The problem with introducing a new language, however, is that it needs a lexer, which can parse the query into a more standard form that can be digested by various server technologies. As most API clients live in the browser, GraphQL tooling evolved around the needs of front-end applications, in a JavaScript ecosystem with browser compatibility in mind. While it makes GraphQL a very pleasant experience on the front-end, the tooling around server to server communication is very much lacking — from bootstrapping a client and figuring out caching and other nuances like fragmentation to writing and parsing queries that can be used by the said client. Even though GraphQL is designed for standard HTTP protocol, the problem is that GraphQL in itself is not standard and might not be the best choice for a versatile API design.

## Observability & Scalability

API health and performance are important metrics that allow us to make conclusions about our API design. Ability to observe these metrics continuously and react to latency and performance issues, as well as runtime errors, should be a motivating factor in our decision-making.

While single point of entry APIs offer simplicity, they are quite a headache in terms of observability and scalability. Figuring out the health of your GraphQL or JSON-RPC APIs is quite a challenge without extra instrumentation. While REST is most likely to provide you with detailed logs of what resources were accessed, how many times, and how long it took to process the request, getting the same stats for APIs that have a single endpoint is quite impossible. Instead you end up with millions of log entries for the same endpoint, and unless you make an effort to provision extra logging with operation/method names, you would have no idea what those requests were. Things are even worse with GraphQL that doesn’t believe in HTTP status codes, so all requests end up with 200 status code, so tracing and debugging really turns into adventure every single time.

Using a single point of entry is also a DevOps problem. Depending on the environment, you may want to provision more resources for API endpoints that have higher latency or require more computational resources, but instead you are forced to scale the entire API server with an entirety of its dependencies and the impact of its memory footprint.

A single point of entry also makes it difficult to rip the benefits of reverse proxies that can reroute specific requests, help with caching, observability, load balancing, encryption, access control and other concerns.

## Error Handling

HTTP codes are too generic. As I [wrote some years ago](https://medium.com/itnext/graceful-error-handling-in-rest-driven-web-applications-d4209b4937aa), APIs should be able to communicate problems to the clients, and subsequently the users. Whatever API design you chose, make sure you build a standardised approach to communicating errors to the client and contextualising them.

GraphQL’s error handling is a blessing and a curse. On one hand, it is very verbose, and can report errors from individual field resolvers. On the other hand, it makes debugging and error handling a pain — by merging success and error states into a single response it makes it so much harder for the clients to differentiate between network errors, invariants, schema validation issues, and actual success responses. According to the specification, partial success responses are in fact possible even if individual resolvers report errors, so it is quite cumbersome to try an reconcile null field values with errors (unless the GraphQL server prevents partial responses, as is the case with Apollo). So, give some consideration to how your server deals with errors, and how your clients are going to make sense of them.

As mentioned earlier, you may want to instrument additional tooling to help you with tracing errors in systems that have a single point of entry.

## Versioning

Whether or not your API requires versioning is largely a usage problem. If your API is consumed in house and you are able to evolve APIs while keeping clients up to date, it might not be an issue. If you are distributing your APIs externally, you might want to consider some form of versioning.

If your API exists largely as a proxy to your database model, versioning can be somewhat of an acute problem. Once the database schema changes, there isn’t really a way to maintain backwards compatibility, especially if your API is autogenerated from database models. So, give it some thought, when chosing your tooling.

As mentioned earlier, RPC could be an interesting option for decoupling the storage model from the API model, giving you more flexibility. You can evolve your API without necessarily versioning it by introducing new procedures and deprecating the old ones. GraphQL tends to brush off versioning, leaning into the same approach — add new fields and deprecate the old ones. The difference is that however with RPC you have more control over request routing and can still introduce versioning. With GraphQL your versioning capabilities are limited — you may need to spin up a different container that serves the older version of the graph. Besides you want to get rid of dead and outdated code from time to time, so some way of communicating breaking changes to the clients would have been a plus.

## Access Controls

You may want to invest some time giving access requirements a thought. Whether or not you require route/procedure level, resource level, or field level access can have a great impact on the your choice of API design.

Should resource-level checks be sufficient, you still need to consider, whether representation of the resource is identical for all users. Should you need higher granularity in access controls, you may need to find a way to communicate these requirements to the clients. Whatever route you take on the server (preventing access to the whole resource, or nulling the field value, or communicating an error on field access), it will be the responsibility of the client to deal with the fallout.

GraphQL is quite handy if you need field level access, though it does lack SDL level standars for documenting access requirements (aside from non-standard directives). REST API might not be an ideal solution for applications that need high levels granularity, as it prevents you from branching resource representation. RPC might offer some flexibility in designing the API with your particular requirements in mind.
