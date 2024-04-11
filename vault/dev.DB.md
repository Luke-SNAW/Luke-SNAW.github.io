---
id: eha8xvsaz0zdh4f18pqqls2
title: DB
desc: ""
updated: 1712288251560
created: 1656645858715
---

## Collections

- [SQL for the Weary](https://gvwilson.github.io/sql-tutorial/)
- [Use cases of soft delete](https://rahulraj.io/a-better-deletion-approach-than-soft-delete/)
  > - You want to delete records, but also want to retain them for n number of days, just for a safer side against accidental deletion.
  > - You want to exclude some records (permanent retain) under explicit requirements, even if they match the criteria of an eligible record to be deleted.
  > - You don't want to delete the actual resource before returning the resource back. Basically, deletion before returning the value is not desired.
  > - You don't want to modify existing table schema(s) to accommodate soft delete key.
  > - You want the tables as loosely coupled as possible without having to worry about deletion logic.
- [Soft Deletion Probably Isn't Worth It](https://brandur.org/soft-deletion)
  - https://news.ycombinator.com/item?id=32156009
  - [Easy, alternative soft deletion: `deleted_record_insert`](https://brandur.org/fragments/deleted-record-insert)
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
- [Data Engineering Design Patterns](https://www.dedp.online/) #bookshelf
- [It's Time To Get Over That Stored Procedure Aversion You Have](https://bigmachine.io/databases/its-time-to-get-over-that-stored-procedure-aversion-you-have/)

## SQLite

- [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)
- [Absurd Success](https://www.marginalia.nu/log/87_absurd_success/)
  > The author describes making several improvements to their search engine that significantly increased its performance and scalability. They reworked the URL database to use a single SQLite table instead of large MySQL tables, generating unique IDs during indexing rather than relying on database auto-increment. This reduced RAM usage and allowed indexing to continue while the database was updated. They also changed how the reverse index was constructed, building multiple smaller pre-indexes in memory and then merging them, instead of using a large in-memory lexicon. This avoided writing terabytes of random data to disk and allowed indexing disparate datasets together. Overall these changes halved RAM usage and addressed all known scaling issues, improving the system considerably more than expected.
- [BIG DATA IS DEAD](https://motherduck.com/blog/big-data-is-dead/)
  > The author suggests that the real problem is often data hoarding rather than true "Big Data" challenges. Overall, the passage contends that the Big Data hype has passed and organizations should focus on using their data effectively rather than worrying about sheer data volume.

## PostgreSQL

- [MySQL vs PostgreSQL in 2023.](https://dbconvert.com/blog/mysql-vs-postgresql/)
- [Postgresql is enough](https://gist.github.com/cpursley/c8fb81fe8a7e5df038158bdfe0f06dbb)
  > - [As an application grows in complexity, you start to realize _why_ there's a stack, rather than just a single technology to rule them all. Trying to cram everything into Postgres (or lambdas, or S3, or firebase, or whatever other tech you're trying to consolidate on) starts to get really uncomfortable.](https://news.ycombinator.com/item?id=39274174)
  > - [... both worked: the PG queue was never grown out of, and generally SQS was easy to work with & reliable. But what I've also seen is "Let's introduce bespoke tech that nobody on the team, including the person introducing it, has experience in, for a queue that isn't even the main focus of what we're building" — this I'm less fine with.](https://news.ycombinator.com/item?id=39274805)
- [Simplify: move code into database functions](https://sive.rs/pg)
  - Databases outlive the applications that access them.
  - the database is actually [quite smart](https://www.postgresql.org/docs/current/server-programming.html).
  - examples: [constraints](https://www.postgresql.org/docs/current/ddl-constraints.html), [triggers](https://www.postgresql.org/docs/current/trigger-definition.html), functions, [create JSON directly](https://www.postgresql.org/docs/current/functions-json.html#FUNCTIONS-JSON-CREATION-TABLE).
  - If you like JavaScript, check out the promising [plv8](https://plv8.github.io/).
  - **branching? source code history(Migrations)?**
    - [How to work with stored procedures and not die trying](https://github.com/kblok/tech-posts/blob/master/working-with-stored-procedures.md)?
    - [You can use a DDL trigger to keep all revisions in a table in a separate database (and of course back up that database frequently).](https://dba.stackexchange.com/a/33544) - [SQL Server DDL Triggers to Track All Database Changes](http://www.mssqltips.com/sqlservertip/2085/sql-server-ddl-triggers-to-track-all-database-changes/)

### [Features I'd like in PostgreSQL](https://gilslotd.com/blog/features_id_postgresql)

- –i-am-a-dummy mode
- Unit test mode (random result sorting)
- Query progress in psql
- Pandas-like join validation
- JIT support for CREATE INDEX
- Reduce the memory usage of prepared queries
