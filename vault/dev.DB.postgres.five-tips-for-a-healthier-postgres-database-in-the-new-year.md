---
id: ur54de0oabkmy73h4qfbc7t
title: Five Tips For a Healthier Postgres Database in the New Year
desc: ''
updated: 1676252268292
created: 1676252126029
---

> https://www.crunchydata.com/blog/five-tips-for-a-healthier-postgres-database-in-the-new-year

## Set a statement timeout

Long running (usually unintentionally so) queries can wreck havoc on a database. They can hold up other queries, replication, or other database processes. Most applications are designed for typical queries to run in a few milliseconds. You may have long running queries for reporting, but these are best offloaded to a read replica for reporting and analytics. To prevent those long running queries you can set a `statement_timeout`:

```sql
ALTER DATABASE mydatabase SET statement_timeout = '60s';
```

_For good measure you may also want to set your `idle_in_transaction` timeout as well, which will cancel long running transaction that are no longer performing work._

## Ensure you have query tracking

Understanding what is going on inside your database is always a good idea. Which queries are slow? Which queries are run too many times? Enter the most useful Postgres extension that exists: `pg_stat_statements`.

Pg_stat_statements records every query that runs against your database, parameterizes it, and then records a variety of metrics about it. That makes it easy to answer the above questions. If you don't have it installed already do it today by running:

```sql
CREATE EXTENSION pg_stat_statements;
```

Once it's in place you can take a look at our [deep dive](https://www.crunchydata.com/blog/tentative-smarter-query-optimization-in-postgres-starts-with-pg_stat_statements) on all the insights it can show you.

## Log slow running queries

While `pg_stat_statements` is useful for looking at frequently run queries or queries that may always be slow, sometimes you have extreme outlier queries. With `pg_stat_statements` you may review your queries every few months. Meanwhile your Postgres logs likely [feed into](https://docs.crunchybridge.com/how-to/logging/?CrunchyAnonId=caesivkkyecnldlsqpittjuniiyazdbraadbozbw) some other central system that you are monitoring daily and have alerting on. Catching these slow outlier queries early can be a great canary for things you should quickly move off to a read-replica for scaling or that you should rewrite to be more efficient. You can [log all slow queries](https://www.crunchydata.com/blog/logging-tips-for-postgres-featuring-your-slow-queries) that take over a certain time with `log_min_duration_statement`.

For many SaaS applications setting your `log_min_duration_statement` to something like 1 second: `1s` or even as low as 100 milliseconds: `100ms` can be a big asset.

## Improve your connection management

If you're using Rails, Django, Hibernate or any other framework/ORM you've likely set a connection pool in your application settings for your database. That connection pool is likely reducing latency in new connections to your database, but is also limiting the performance available for your database. On versions prior to Postgres 14, connections consumed extra overhead leaving `idle` connections as wasted space. The solution to this is not to replace your in app connection pooling, but rather add a server side connection pooler such as PgBouncer. With PgBouncer you're able to scale to 10s of thousands of connections with no problem. You can take a quick look at your existing database to see if PgBouncer would help:

```sql
SELECT count(*),
       state
FROM pg_stat_activity
GROUP BY 2;
```

If you see `idle` is above 20 it's recommended to explore using PgBouncer. Adding PgBouncer is often a no brainer to get better performance without any heavy refactoring required. And to make it easy if you're on [Crunchy Bridge](https://docs.crunchybridge.com/how-to/pgbouncer/?CrunchyAnonId=caesivkkyecnldlsqpittjuniiyazdbraadbozbw) it's already available to you.

## Find your goldilocks range for indexes

There seems to be a common lifecycle of indexes within applications. First you start off with almost none, maybe a few on primary keys. Then you start adding them, one by one, two by two, until you've got quite a few indexes for most any query you can run. Something is slow? Throw an index at it. What you end up with is some contention on overall throughput of your database, and well a lot of indexes that became a tangled ball of yarn over time.

We've got a slew of write-ups and guides on indexes and unfortunately there isn't a "this is your one thing to read and your done". But a few key things and you can be in a better place:

- [A primer on indexes](https://www.crunchydata.com/blog/three-easy-things-to-remember-about-postgres-indexes)
- [Check for unused indexes](https://www.crunchydata.com/blog/cleaning-up-your-postgres-database)
- [Index types in Postgres](https://learn.crunchydata.com/postgresql-devel/courses/basics/indextypes)
- [A starter lesson on indexes](https://learn.crunchydata.com/postgresql-devel/courses/basics/introindex)

## Here's to less database problems in 2022

Our goal at Crunchy is to make Postgres great. One part of that is helping our customers understand their database and providing them with support and guidance for all their Postgres needs.

With [Crunchy Bridge](https://www.crunchydata.com/products/crunchy-bridge/) we're working towards making all of the above easier, so it's one less thing you have to worry about. We've already had customers migrate and see [3-5x performance improvement](https://www.crunchydata.com/case-studies/rival-iq/) over their existing cloud providers. We know if you're here you're already a fan of Postgres. In this coming year we look forward to making the developer experience of Postgres better than it's ever been.

---

## [pg_stat_statements is not free](https://news.ycombinator.com/item?id=34754445)

pg_stat_statements is useful, but it isn't completely free, e.g. https://www.alibabacloud.com/blog/postgresql-v12-how-pg-stat-statements-causes-high-concurrency-performance-issues_597790 (admittedly from pg12, which is three major versions ago).

Most people should probably leave it enabled, but if you have a database with a very defined and understood query pattern, then it might be worth running _perf_ and checking if it is costing you.
