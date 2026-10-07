
> https://www.michaelnygard.com/blog/2018/01/services-by-lifecycle/

This post took a lot longer to pull together than I expected. Not because it was hard to write, but because it was too easy to write _too much_. Like a [pre-bonsai tree](https://www.youtube.com/watch?v=96aW1V8DhEU), it would grow out of control and get pruned back over and over.

In the meantime, I delivered [a workshop](https://n6consulting.com/workshop/arch-without-end-state/) and spent some lovely holiday time with my family.

But it’s a new year now, and January is devoid of holidays so it’s high time I got back to business.

## Avoiding the Entity Service

In my [last post](dev.software-engineering.the-entity-service-antipattern.md), I made a case against entity services. To recap, an entity service is a set of CRUD operations on a business entity such as _Person_, _Location_, _Contract_, _Order_, etc. It’s an antipattern because it creates high semantic and operational coupling. Edge services suffer from common-mode failures through their shared dependency on the entity services. Changes or outages in the entity services have large “failure domains.”

A lot of good advice springs from Eric Evan’s hugely influential book “Domain-Driven Design.” It was written before the service era, but seems to apply well now. I’m not an expert on DDD, though, so I’m going to offer some techniques that may or may not be described there. (I dig the “bounded context” idea, but need to re-read the whole book before I comment on it more.)

There are several ways to avoid entity services. This post explores just one (though it’s one I particularly like.) Future posts will look at additional techniques.

### Focus on Behavior Instead of Data

When you think about what a service _knows_, you always end up back at CRUD. I recommend thinking in terms of the service’s responsibilities. (And don’t say it’s responsible for _knowing some data_!) Does it apply policy? Does it aggregate a stream of concepts into a summary? Does it facilitate some kinds of changes? Does it calculate something? And so on.

Once you know what a service does, you can figure out what it needs to know. For instance, a service that restricts content delivery based on local laws needs to know a few things:

1. What jurisdiction applies?
2. What classifiers are on the content?
3. What classifiers are not allowed in that jurisdiction?

Notice that #1 and #2 are specific to an individual request, while #3 is slowly-changing data. Thus it makes sense for the service to _know_ #3 and be _told_ #1 and #2.

This leads us to a deeper discussion about what the service knows. How does that data get into the service? Is there a GUI for a legal team? Maybe there’s a feed we can purchase from a data vendor. Maybe we need to apply machine learning based on lawsuits and penalties incurred when we violate local laws. (I’m kidding! Don’t do the last one!) The answers to these questions will firm up your design and situate your service in its ecosystem.

### Model Like It’s 1999

When modeling, I like to use a technique from object-oriented design. [CRC cards](http://wiki.c2.com/?CrcCard) let me lay out physical tokens that represent services. Then I can play a game where I simulate a request coming in at the edge. A service can add information to a request and pass it along to another service, following the “Tell, Don’t Ask” principle.

If you are in a team, you can deal out cards to players then simulate a request by passing a physical object around. That will quickly reveal gaps in a design. Some common gaps that I see:

1. A service doesn’t know where to send the request. It lacks knowledge of other services that can continue processing. The solution is either to statically introduce it to the next party or to provide URLs in the data that lead to the handler.
2. A service receives a request that is insufficient. The incoming request either lacks information or has an implicit context that should be turned into data on the request.

While playing the CRC game, it’s OK to assume your service already has data it naturally depends on. That is, slowly-changing data the service uses should be considered an asynchronous process relative to the current request. But do make note of that slowly-changing data so you remember to build in the flows needed to populate it.

If you follow “Tell, Don’t Ask” strictly, then the activation set will be a strict tree. Anywhere a service calls out to more than one downstream, it should be sending instructions forward in parallel rather than serially making queries followed by an instruction.

### Dealing with Consistency

If it were just a matter of passing requests along with extra data, then life would be simple. As often happens, trouble comes from side effects.

Services are not pure functions. If a service call _always_ results in the same result for the same parameters, then you don’t need a service. Make a library and avoid the operational overhead! Services only make sense when they change something in the world. That means state and state changes are unavoidable concerns in a service-based architecture.

Consistency immediately comes up as an issue. Many words have already been written about [CAP](https://en.m.wikipedia.org/wiki/CAP_theorem). Some good, some misguided, and some pure marketing. I even wrote an earlier post about the subtle differences between the [C in CAP versus the C in ACID](http://thinkrelevance.com/blog/2013/12/23/beware-inconsistent-definitions-of-consistency).

Let’s look at one way to deal with consistency in the face of changing state.

### Divide Services by Lifecycle in a Business Process

Many business processes have entities that go through a series of milestones. In a particular state, changes are allowed to certain attributes but not others. Once a subset of the properties are “valid” (whatever _that_ means) the entity can transition to the next stage of the business process.

Instead of viewing this as a single entity with a bunch of booleans, or a CURRENT*STATE attribute (which implies a state machine that is unknown to consumers) we can view each state as a \_different thing*.

For example, consider this process from a peer-to-peer lending situation:

1. A loan requestor starts by creating a project proposal. The requestor can provide descriptive text, an amount to request, some media assets (projects with big vivid pictures get funded faster.)
2. Once the loan request is completed, the requestor submits it for approval. At this point, the requestor is no longer allowed to change the amount requested.
3. An analyst from the host company reviews the proposal. In parallel, a background job checks the requestor’s credit score, repayment history, and criminal record.
4. The analyst reviews the request and either assigns a target interest rate, rejects the request outright, or indicates that more information is needed from the requestor.
5. Once approved, the proposal is visible to funders. Funders can commit to a certain amount (contingent on _their_ credit scores.) At this stage, none of the proposal information can be changed, although the whole proposal could be withdrawn.
6. Once fully funded, funders must transfer money within 3 days. No additional funders are allowed to join the project at this time, but they can go on a waiting list in case some of the committed funders fail to supply the money.
7. Once funds are in the funders' accounts, it all gets transfered into a short-term holding account. The project information, all the individuals' information (tax IDs, etc.) goes to an underwriter who produces a legal loan document for all parties to sign.

For the moment, we’re leaving out some of the tributaries of this flow.

Notice how moving through the business process causes previous information to become effectively read-only?

The original form of this system was a monolith that had a state field on a “Loan” model object. That was a _wide_ object, since it had everything from the initial proposal through to the ultimate payment. If we made that into a “Loan” microservice we would exactly end up with an entity service, CRUD operations, and high coupling into that service, as shown below.

![With loan entity service](/assets/images/software-engineering/services-by-lifecycle__with-loan-entity-service.svg)

Try playing CRC with this design. You’ll find that all requests reach the Loan service.

What is less evident from the diagram is about the cost of embedding a state model into the entity service directly. If we put a state field on the Loan, then every Loan must go through the same state machine. It locks us into a single kind of business process. At the time, we already knew the company was exploring direct-funded loans through a banking partner. So there would be a minimum of two flavors of process. (Or one process with proliferating branches.)

I briefly considered using [my DEVS library](https://github.com/mtnygard/devs) to represent the state plus state machine as EDN data on each Loan, but ultimately decided against it.

Instead, I thought we could make each state into its own service, as shown here.

![With Lifecycle](/assets/images/software-engineering/services-by-lifecycle__with-lifecycle.svg)

Now as the business process moves along, we’re really sending documents to each service. For example, from Proposal to Project, we send a “ProjectStarter” document that contains all the attributes needed for a Project. When the analyst approves a project, the analyst GUI (or backend for same) creates a “LoanStarter” and sends it to the UnfundedLoan service. Likewise, once all funding is received, the “Collection” service creates a “LoanPackage” document and sends it to the “Underwriting” service. (That’s “collection” as in “gatherer of documents” not “collection” as in “break your kneecaps.") Further downstream, we set up a schedule of payments to receive from the requestor and payments to issue to the backers. We also keep a set of ledgers to track balances per account.

Each of the services has facilities to add or update information relevant to that service. It ignores anything in the incoming documents that it doesn’t need.

This gives us a lot of flexibility in how we build the overall process.

Consider our direct-funding scenario. We need a new “DirectFunding” service that finds suitable candidates. It sends a document out to the bank and receives a response. On a favorable response, DirectFunding can create its own version of the LoanPackage document for underwriting. In other words, treating these stages as services connected by well-defined document formats allows us to introduce more pathways without creating the state machine from hell.

As an additional benefit, we can easily monitor the flow of documents to see when the process is healthy. We can monitor each service’s activity to create a cumulative flow diagram. We get a lot of visibility. And since some stages are triggered by humans (e.g., the analysts) we can even figure out how our staff model must scale with business throughput.

It should also be clear that this style works well with event transfer instead of document transfer. It would be natural to put all the documents onto a message bus.

Overall, I think this style offers a nice degree of alignment between the technology and the business. The only “downside” I can see is that it requires a service developer to understand how that service contributes to value streams and business processes.

### Backtracking, Errors, and Races

There is still a minute window of opportunity for _perceived_ inconsistency to sneak in. For example, what happens if the requestor tries to change the proposal while the analyst is reviewing it? Or worse, what if they change it in those milliseconds between when the analyst clicks “Approve” in the GUI and when the document goes over to the Project service? For that matter, how do we tell the Proposal service that the proposal can no longer be edited without withdrawing the request and resubmitting as a new Project?

This post is already getting too long, so I’m going to answer those questions next time. It shouldn’t take another month since we’re past the holiday-fun-times and into the serious winter months.
