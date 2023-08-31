---
id: eha8xvsaz0zdh4f18pqqls2
title: DB
desc: ""
updated: 1693466275442
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

- [A 5 years+ tech lead said they shard a database to scale but then he failed to answer this question](https://iorilan.medium.com/a-5-years-tech-lead-said-they-shard-a-database-to-scale-but-then-he-failed-to-answer-this-question-8be39115dcb0)
- [OrmHate](https://martinfowler.com/bliki/OrmHate.html)
  > Essentially the ORM can handle about 80-90% of the mapping problems, but that last chunk always needs careful work by somebody who really understands how a relational database works.  
  > ... A framework that allows me to avoid 80% of that is worthwhile even if it is only 80%.  
  > To avoid the mapping problem you have two alternatives. Either you use the relational model in memory, or you don't use it in the database.

## SQLite

- [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)
- [Absurd Success](https://www.marginalia.nu/log/87_absurd_success/)
  > The author describes making several improvements to their search engine that significantly increased its performance and scalability. They reworked the URL database to use a single SQLite table instead of large MySQL tables, generating unique IDs during indexing rather than relying on database auto-increment. This reduced RAM usage and allowed indexing to continue while the database was updated. They also changed how the reverse index was constructed, building multiple smaller pre-indexes in memory and then merging them, instead of using a large in-memory lexicon. This avoided writing terabytes of random data to disk and allowed indexing disparate datasets together. Overall these changes halved RAM usage and addressed all known scaling issues, improving the system considerably more than expected.

## PostgreSQL

- [MySQL vs PostgreSQL in 2023.](https://dbconvert.com/blog/mysql-vs-postgresql/)

### [Features I'd like in PostgreSQL](https://gilslotd.com/blog/features_id_postgresql)

- –i-am-a-dummy mode
- Unit test mode (random result sorting)
- Query progress in psql
- Pandas-like join validation
- JIT support for CREATE INDEX
- Reduce the memory usage of prepared queries
