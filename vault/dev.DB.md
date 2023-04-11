---
id: eha8xvsaz0zdh4f18pqqls2
title: DB
desc: ""
updated: 1681174815664
created: 1656645858715
---

## Collections

- [Soft Deletion Probably Isn't Worth It](https://brandur.org/soft-deletion)
  - https://news.ycombinator.com/item?id=32156009
- [Index Merges vs Composite Indexes in Postgres and MySQL](https://sirupsen.com/index-merges)
  > Composite indexes are about 10x faster than index merges. In Postgres, the gap is larger than in MySQL because Postgres doesn't support index-only scans for queries that involve index merges.
- [MySQL for Developers](https://planetscale.com/courses/mysql-for-developers/introduction/course-introduction) #bookshelf
- [How does database sharding work?](https://planetscale.com/blog/how-does-database-sharding-work)

  > why are you not using a database that does sharding for you? Over the past few years the so-called “serverless” database has gotten a lot more traction.

  > This is the most important paragraph in the article. In a world where things like Dynamo/Cassandra or Spanner/Cockroach exist, manually-sharded DB solutions are pretty much entirely obsolete. Spanner exists because Google got so sick of people building and maintaining bespoke solutions for replication and resharding, which would inevitably have their own set of quirks, bugs, consistency gaps, scaling limits, and manual operations required to reshard or rebalance from time to time. When it's part of the database itself, all those problems just... disappear. It's like a single database that just happens to spread itself across multiple machines. It's an actual distributed cloud solution.  
  > My current employer uses sharded and replicated Postgres via RDS. Even basic things like deploying schema changes to every shard are an unbelievable pain in the ass, and changing the number of shards on a major database is a high-touch, multi-day operation. After having worked with Spanner in the past, it's like going back to the stone age, like we're only a step above babysitting individual machines in a closet. Nobody should do this. — [GeneralMayhem](https://news.ycombinator.com/item?id=35478332)

## SQLite

- [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)

## PostgreSQL

- [MySQL vs PostgreSQL in 2023.](https://dbconvert.com/blog/mysql-vs-postgresql/)

### [Features I'd like in PostgreSQL](https://gilslotd.com/blog/features_id_postgresql)

- –i-am-a-dummy mode
- Unit test mode (random result sorting)
- Query progress in psql
- Pandas-like join validation
- JIT support for CREATE INDEX
- Reduce the memory usage of prepared queries
