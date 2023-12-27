---
id: bpw92y9ez0959qtnaedllfs
title: How Pinterest scaled to 11 million users with only 6 engineers
desc: ""
updated: 1703654866126
created: 1703654655270
---

> https://read.engineerscodex.com/p/how-pinterest-scaled-to-11-million

In January 2012, Pinterest hit 11.7 million monthly unique users with only 6 engineers.

Having launched in March 2010, it was [the fastest company to race past 10 million monthly users at the time](https://techcrunch.com/2012/02/07/pinterest-monthly-uniques/#:~:text=11.7%20million%20unique%20monthly%20U.S.%20visitors%2C%20crossing%20the%2010%20million%20mark%20faster%20than%20any%20other%20standalone%20site%20in%20history.).

[Pinterest](https://pinterest.com/) is an image-heavy social network, where users can save or “pin” images to their boards.

> When I say “users” below, I mean “monthly active users” (MAUs).

## **Lessons from Scaling Pinterest**

- **Use known, proven technologies.** Pinterest’s dive into newer technologies at the time led to issues like data corruption.
- **Keep it simple.** (A recurring theme!)
- **Don’t get too creative.** The team settled on an architecture where they could add more of the same nodes to scale.
- **Limit your options**.
- **Sharding databases > clustering.** It reduced data transfer across nodes, which was a good thing.
- **Have fun!** New engineers would contribute code in their first week.

[The Instagram team had similar lessons from scaling to 14 million users with 3 engineers](https://engineercodex.substack.com/p/how-instagram-scaled-to-14-million).

## **March 2010: Closed beta launch, 1 engineer**

Pinterest launched in March 2010 with 1 small MySQL database, 1 small web server, and 1 engineer (along with the 2 co-founders).

https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F19d5d064-82c0-4d31-916d-70bfeb1527a9_1124x448.png

## **January 2011: 10,000 users, 2 engineers**

Nine months later in January 2011, Pinterest’s architecture had evolved to handle more users. They were still invite-only and had 2 engineers.

They had:

- a basic web server stack (Amazon EC2, S3, and CloudFront)
  - Django (Python) for their backend
- 4 web servers for redundancy
- NGINX as their reverse proxy and load balancer.
- 1 MySQL database at this point + 1 read-only secondary
- MongoDB for counters
- 1 task queue and 2 task processors for asynchronous tasks

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F8cd7c12c-bdc0-494d-ac86-b65f09b2a2f6_1255x615.png

## **October 2011: 3.2 million users, 3 engineers**

From January 2011 to October 2011, Pinterest grew extremely fast, doubling users every month and a half.

Their iPhone app launch in March 2011 was one of the factors fueling this growth.

When things grow fast, technology breaks more often than you expect.

Pinterest made a mistake: **they over-complicated their architecture immensely.**

They had only 3 engineers, but 5 different database technologies for their data.

They were both manually sharding their MySQL databases and clustering their data using Cassandra and Membase (now Couchbase).

**[Their “overcomplicated stack"](https://www.infoq.com/presentations/Pinterest/):**

- Web server stack (EC2 + S3 + CloudFront)
  - [Pinterest started moving to Flask (Python) for their backend](https://www.quora.com/What-challenges-has-Pinterest-encountered-with-Flask)
- 16 web servers
- 2 API engines
- 2 NGINX proxies
- 5 manually-sharded MySQL DBs + 9 read-only secondaries
- 4 Cassandra Nodes
- 15 Membase Nodes (3 separate clusters)
- 8 Memcache Nodes
- 10 Redis Nodes
- 3 Task Routers + 4 Task Processors
- 4 Elastic Search Nodes
- 3 Mongo Clusters

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F386fd87b-f932-4310-82cf-07860bc36e98_1357x1047.png

Subscribe

### ⚠️ Clustering gone wrong

> **Database clustering** is the process of connecting multiple database servers to work together as a single system.

In theory, clustering automatically scales datastores, provides high availability, free load balancing, and doesn’t have a single point of failure.

Unfortunately, in practice, clustering was overly complex, had difficult upgrade mechanisms, and **it had a big single point of failure.**

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb2198073-6421-434e-be2f-2904aa5ff975_1462x645.png

Each DB has a Cluster Management Algorithm that routes from DB to DB.

When something goes wrong with a DB, a new DB is added to replace it.

In theory, the Cluster Management Algorithm should handle this just fine.

In reality, there was a bug in Pinterest’s Cluster Management Algorithm that **corrupted data on all their nodes, broke their data rebalancing, and created some unfixable problems**.

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffabc91cd-53b2-47f2-9d71-c50e7a3824aa_1306x538.png

Pinterest’s solution? **Remove all clustering tech (Cassandra, Membase) from the system. Go all-in with MySQL + Memcached (more proven).**

MySQL and Memcached are well-proven technologies. [Facebook used the two to create the largest Memcached system in the world, which handled billions of requests per second for them with ease.](https://engineercodex.substack.com/p/how-facebook-scaled-memcached)

Subscribe

## **January 2012: 11 million users, 6 engineers**

In January 2012, Pinterest was handling ~11 million monthly active users, with anywhere between 12 million to 21 million daily users.

At this point, Pinterest had taken the time to simplify their architecture.

They removed less-proven ideas, like clustering and Cassandra at the time, and replaced them with proven ones, like MySQL, Memcache, and sharding.

**Their simplified stack:**

- Amazon EC2 + S3 + [Akamai](https://www.akamai.com/) (replaced CloudFront)
- [AWS ELB (Elastic Load Balancing)](https://aws.amazon.com/elasticloadbalancing/)
- 90 Web Engines + 50 API Engines ([using Flask](https://www.quora.com/What-challenges-has-Pinterest-encountered-with-Flask))
- 66 MySQL DBs + 66 secondaries
- 59 Redis Instances
- 51 Memcache Instances
- 1 Redis Task Manager + 25 Task Processors
- Sharded [Apache Solr](https://solr.apache.org/) (replaced Elasticsearch)
- **Removed Cassanda, Membase, Elasticsearch, MongoDB, NGINX**

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F34e259af-7bfe-4734-ab56-f793dabe2cb2_1608x767.png

### How Pinterest manually sharded their databases

> **Database sharding** is a method of splitting a single dataset into multiple databases.
>
> **Benefits:** high availability, load balancing, simple algorithm for placing data, easy to split databases to add more capacity, easy to locate data

When Pinterest first sharded their databases, they had a feature freeze. Over the span of a few months, **they sharded their databases incrementally and manually:**

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F33d7cfda-8807-4adf-a927-7e7f3e9faaf5_789x443.png

[Source: Scaling Pinterest](https://www.infoq.com/presentations/Pinterest/)

The team removed table joins and complex queries from the database layer. They added lots of caching.

Since it was extra effort to maintain unique constraints across databases, they kept data like usernames and emails in a huge, unsharded database.

All their tables existed on all their shards.

#### An small example of manual sharding

Since they had billions of “pins”, their database indexes ran out of memory.

They would take the largest table on the database and move it to its own database.

Then, when that database ran out of space, they would shard.

Subscribe

## **October 2012: 22 million users, 40 engineers**

In October 2012, Pinterest had around 22 million monthly users, but their engineering team had quadrupled to 40 engineers.

**The architecture was the same. They just added more of the same systems.**

- Amazon EC2 + S3 + CDNs (EdgeCast, Akamai, Level 3)
- 180 web servers + 240 API engines (using Flask)
- 88 MySQL DBs + 88 secondaries each
- 110 Redis instances
- 200 Memcache instances
- 4 Redis Task Managers + 80 Task Processors
- Sharded Apache Solr

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fff18b5dd-2d71-4d8b-864a-4455e374bc62_1608x767.png

They started moving from hard disk drives to SSDs.

An important lesson learned: **limited, proven choices was a good thing**.

Sticking with EC2 and S3 meant they had limited configuration choices, leading to less headaches and more simplicity.

**However, new instances could be ready in seconds.** This meant that they could add 10 Memcache instances in a matter of minutes.

Subscribe

## **Pinterest’s Database Structuring**

### IDs

[Like Instagram](https://engineercodex.substack.com/p/how-instagram-scaled-to-14-million), Pinterest had a unique ID structure because they had sharded databases.

Their 64-bit ID looked like:

https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F269be284-a074-4898-857b-2a8903ba4b48_590x110.png

[Source: Scaling Pinterest](https://www.infoq.com/presentations/Pinterest/)

> **Shard ID:** which shard (16 bits)
>
> **Type:** object type, such as pins (10 bits)
>
> **Local ID:** position in table (38 bits)

The lookup structure for these IDs was **a simple Python dictionary.**

---

### Tables

They had Object tables and Mapping tables.

**Object tables were for pins, boards, comments, users, and more.** They had a Local ID mapped to a MySQL blob, like JSON.

**Mapping tables were for relational data between objects, like mapping boards to a user or likes to a pin.** They had a Full ID mapped to a Full ID and a timestamp.

All queries were PK (primary key) or index lookups for efficiency. They cut out all JOINs.

---

**This article is based on [Scaling Pinterest](https://www.infoq.com/presentations/Pinterest/), a talk given by the Pinterest team in 2012.**
