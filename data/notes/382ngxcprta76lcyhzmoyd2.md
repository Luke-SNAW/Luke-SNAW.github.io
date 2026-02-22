
> https://restfulapi.net/richardson-maturity-model/

## 1. What is Richardson Maturity Model

Leonard Richardson analyzed a hundred different web service designs and divided these designs into four categories. These categories are based on **how much the web services are [REST compliant](https://restfulapi.net/rest-architectural-constraints/)**.

This model of division of REST services to identify their maturity level – is called **Richardson Maturity Model**.

![The levels of maturity according to Richardson’s model](assets/images/back-end/richardson-maturity-model-0.webp)

Richardson used three main **factors to decide the maturity of a service**. These factors are

1. [URI](https://restfulapi.net/resource-naming/),
2. [HTTP Methods](https://restfulapi.net/http-methods/),
3. [HATEOAS (Hypermedia)](https://restfulapi.net/hateoas/)

The more a service employs these factors – the more mature it shall be considered.

## 2. Maturity Levels

In his analysis, Richardson described total 4 maturity levels as given below:

![Richardson Maturity Model](assets/images/back-end/richardson-maturity-model-1.webp)

- Level Zero
- Level One
- Level Two
- Level Three

Note that Roy Fielding has already made it very clear that [level 3 RMM is a pre-condition of REST](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven).

### 2.1. Level Zero

> Level zero of maturity does not make use of any of URI, HTTP Methods, and HATEOAS capabilities.

The services at zero maturity level have a single URI and use a single HTTP method (typically POST).

For example, most SOAP Web Services use a single URI to identify an endpoint, and HTTP POST to transfer SOAP-based payloads, effectively ignoring the rest of the HTTP verbs.

Similarly, XML-RPC-based services send data as _Plain Old XML_ (POX).

These are the most primitive ways of building SOA applications with a single POST method endpoint and using XML to communicate between the client and the server.

### 2.2. Level One

> Level one of maturity **makes use of URIs**, but does not use the HTTP Methods, and HATEOAS.

The services at maturity level one employ many URIs but only a single HTTP verb – generally HTTP POST.

These services will give each resource, available in the system, a unique URI. A unique URI separately identifies one unique resource – and that makes these services better than level zero.

### 2.3. Level Two

> Level two of maturity **makes use of URIs and HTTP Methods**, but does not use the HATEOAS.

The level two services generally host numerous URIs i.e. addressable resources.

Such services support several of the HTTP verbs on each exposed resource – Create, Read, Update and Delete (CRUD) services. Here the state of resources, typically representing business entities, can be manipulated over the network.

The designers of the level two services expect people to put some effort into mastering the APIs – generally by reading the supplied documentation.

Maturity level 2 is the most popular usecase of REST principles, which advocate using different verbs based on the HTTP request methods, while the system can have multiple resources.

### 2.4. Level Three

> Level three of maturity **makes use of all three, i.e. URIs and HTTP, and HATEOAS**.

Level three is the most mature level of Richardson’s model, which encourages **easy discoverability**. This level makes it easy for the responses to be self-descriptive by using HATEOAS.

Level three services lead the service consumers through a trail of resources, causing application state transitions as a result.

References:

[Act Three: The Maturity Heuristic](https://www.crummy.com/writing/speaking/2008-QCon/act3.html)
