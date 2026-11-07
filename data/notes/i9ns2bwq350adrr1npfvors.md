
> https://stackoverflow.blog/2022/11/28/when-to-use-grpc-vs-graphql/

TLDR: Use GraphQL for client-server communication and gRPC for server-to-server. See the Verdict section for exceptions to this rule.

...

## Summary

Here’s a summary of the topics we’ve covered:

### Similarities between gRPC and GraphQL

- Typed interfaces with codegen
- Abstract away the network layer
- Can have JSON responses
- Server streaming
- Good forward compatibility
- Can avoid overfetching

### gRPC

#### Strengths

- Binary format:
  - Faster transfer over network
  - Faster serializing, parsing, and validation
  - However, harder to view and debug than JSON
- HTTP/2:
  - Multiplexing
  - Client and bidirectional streaming
- Built-in retries and deadlines

#### Weaknesses

- Need proxy or [Connect](https://connect.build/docs/protocol/) to use from the browser
- Unable to use most API proxies
- No standard way to know whether a method will mutate state

### GraphQL

#### Strengths

- Client determines which data fields it wants returned. Results in:
  - No underfetching
  - Team decoupling
  - Increased visibility
- Easier to combine data from multiple services
- Further developed introspection and tooling
- Declarative data fetching
- Reactive normalized client cache

#### Weaknesses

- If we already have gRPC services that can be exposed to the public, it takes more backend work to add a GraphQL server.
- HTTP GET caching doesn’t work by default.
- Rate limiting is more complex for public APIs.
- Maps aren’t supported.
- Inefficient text-based transport

## Verdict

### Server-to-server

In server-to-server communication, where low latency is often important, and more types of streaming are sometimes necessary, gRPC is the clear standard. However, there are cases in which we may find some of the benefits of GraphQL more important:

- We’re using GraphQL [federation](https://www.apollographql.com/docs/federation/) or schema stitching to create a supergraph of all our business data and decide to have GraphQL subgraphs published by each service. We create two supergraph endpoints: one external to be called by clients and one internal to be called by services. In this case, it may not be worth it for services to also expose a gRPC API, because they can all be conveniently reached through the supergraph.
- We know our services’ data fields are going to be changing and want field-level visibility on usage so that we can remove old deprecated fields (and aren’t stuck with maintaining them forever).

_There’s also the question of whether we should be doing server-to-server communication ourselves at all. For data fetching (GraphQL’s queries), it’s the fastest way to get a response, but for modifying data (mutations), things like Martin Fowler’s “synchronous calls considered harmful” (see [sidebar here](https://www.martinfowler.com/articles/microservices.html?ref=wellarchitected#SynchronousCallsConsideredHarmful)) have led to using async, event-driven architecture with either choreography or orchestration between services. [Microservices Patterns](https://www.manning.com/books/microservices-patterns) recommends using the latter in most cases, and to maintain DX and development speed, we need a [code-based orchestrator](https://www.youtube.com/watch?v=6lSuDRRFgyY) instead of a DSL-based one. And once we’re working in a code-based orchestrator like Temporal, we no longer make network requests ourselves—the platform reliably handles it for us. In [my opinion](https://twitter.com/lorendsr/status/1419880024929415173), that’s the future._

### Client-server

In client-server communication, latency is high. We want to be able to get all the data we need in a single round trip, have flexibility in what data we fetch for different views, and have powerful caching, so GraphQL is the clear winner. However, there are cases in which we may choose to use gRPC instead:

- We already have a gRPC API that can be used, and the cost of adding a GraphQL server in front of that isn’t worth the benefits.
- JSON is not a good fit for the data (e.g. we’re sending a significant amount of binary data).
