---
id: rbvc7to4emhgev54r1gbc50
title: Just Use Postgres for Everything
desc: ""
updated: 1670804528080
created: 1670804129283
---

> How to reduce complexity and move faster
>
> https://www.amazingcto.com/postgres-for-everything/

_Technology is about tradeoffs. Using Postgres for everything is a tradeoff. Of course you use the right tool for the job. Often this is Postgres. Helping dozens of startups I have seen many more people overcomplicate setups than companies that use tools that are too simple for the job. If you have 1M+ customers, and 50+ developers, and you need Kafka and Spark amd Kubernetes, go ahead. If you have more systems than developers, just use Postgres. Thanks to Hugo and BunnyCDN for keeping the page fast. PS: Postgres for everything doesn’t mean one server for everything ;-)_

**TLDR; just use Postgres for everything.**

We have invited complexity through the door. But it will not leave as easily.

![Complexity](http://www.radicalsimpli.city/Complexity2005_2021.svg)

There is [Radical Simplicity](http://www.radicalsimpli.city/) though.

One way to simplify your stack and reduce the moving parts, speed up development, lower the risk and deliver more features in your startup is **“Use Postgres for everything”**. Postgres can replace - up to millions of users - many backend technologies, Kafka, RabbitMQ, Mongo and Redis among them.

Use Postgres for caching instead of Redis with [UNLOGGED tables](https://www.compose.com/articles/faster-performance-with-unlogged-tables-in-postgresql/) and TEXT as a JSON data type. [Use stored procedures](https://chat.openai.com/chat) to add and enforce an expiry date for the data just like in Redis.

Use Postgres as a message queue with [SKIP LOCKED](https://www.enterprisedb.com/blog/what-skip-locked-postgresql-95) instead of Kafka (if you only need a message queue).

Use Postgres with [TimescaleDB](https://www.timescale.com/) as a data warehouse.

Use Postgres with [JSONB](https://scalegrid.io/blog/using-jsonb-in-postgresql-how-to-effectively-store-index-json-data-in-postgresql/) to store Json documents in a database, search and index them - instead of Mongo.

Use Postgres as a cron demon to take actions at certain times, like sending mails, with [pg_cron](https://github.com/citusdata/pg_cron) adding events to a message queue.

Use Postgres for [Geospacial queries](https://postgis.net/).

Use Postgres for [Fulltext Search](https://supabase.com/blog/postgres-full-text-search-vs-the-rest) instead of Elastic.

Use Postgres to [generate JSON in the database](https://www.amazingcto.com/graphql-for-server-development/), write no server side code and directly give it to the API.

Use Postgres with a [GraphQL adapter](https://graphjin.com/) to deliver GraphQL if needed.

There I’ve said it, **just use Postgres for everything**.

---

Sure, PostgreSQL can be used for sessions, but Redis has solved this problem on virtually every single platform a long time ago. Your customer probably doesn't even know what a session is, but they will definitely learn about them when your in-house implementation inevitably encounters an edge case.

Of course, PostreSQL has wonderful search capabilities but it was never intended to be used as a search engine. Solr was created in 2004 and is still being improved and used in production every day. Do you know what will happen to your full-text search when your customer types in a mix of English and Chinese characters?

Yes, PostgreSQL addition of SKIP LOCKED was neat but AFAIK the author of that feature himself recommended using a traditional job queue unless you had a very good reason against it. RabbitMQ was designed as a message queue and when you read the documentation you realize that they had encountered virtually every single problem and figured out a way to deal with it so that you don't have to. The documentation pretty much tells you what problems you are going to have later so that you can plan for them today.

> https://news.ycombinator.com/item?id=33936703
>
> Sure, if your use case requires it, use Redis for sessions or RabbitMQ for queues. But you can also use a library with postgres, or even write the 40 lines of code yourself.
>
> Each component has its own debugging requirements and tooling. Each component adds a bunch of complexity. Sometimes it's worth it, sometimes it's not. It's not as clear-cut as you're making it be. There are pros and cons to both alternatives.
