---
id: gyry0ci0rohsl5gvjpsvws1
title: DB tools
desc: ""
updated: 1712276537354
created: 1646011997576
---

## Collections

- [Why IndexedDB is slow and what to use instead](https://rxdb.info/slow-indexeddb.html)
- [Why I enjoy PostgreSQL - Infrastructure Engineer's Perspective](https://www.shayon.dev/post/2022/17/why-i-enjoy-postgresql-infrastructure-engineers-perspective/)
- [NocoDB](https://github.com/NocoDB/NocoDB) - Open Source Airtable Alternative - turns any MySQL, Postgres database into a collaborative spreadsheet with REST APIs.
- [ShareDB](https://github.com/share/sharedb) - Realtime database backend based on Operational Transformation (OT)
- [rqlite](https://github.com/rqlite/rqlite) - The lightweight, distributed relational database built on SQLite
- [Litestream](https://github.com/benbjohnson/litestream) is a standalone disaster recovery tool for SQLite. It runs as a background process and safely replicates changes incrementally to another file or S3.
- [Zapatos](https://github.com/jawj/zapatos) - Zero-abstraction Postgres for TypeScript: a non-ORM database library
- [DuckDB](https://duckdb.org/why_duckdb) is an in-process SQL OLAP Database Management System [— What’s the Hype About?](https://betterprogramming.pub/duckdb-whats-the-hype-about-5d46aaa73196)
  - Processing and storing tabular datasets, e.g. from CSV or Parquet files
  - Interactive data analysis, e.g. Joining & aggregate multiple large tables
  - Concurrent large changes, to multiple large tables, e.g. appending rows, adding/removing/updating columns
  - Large result set transfer to client
- [sqlc](https://github.com/kyleconroy/sqlc) - A SQL Compiler
- [Steampipe](https://github.com/turbot/steampipe) is the universal interface to APIs. Use SQL to query cloud infrastructure, SaaS, code, logs, and more.
  - https://github.com/turbot/steampipe-plugin-googlesheets
- [libgsqlite](https://github.com/0x6b/libgsqlite) - A SQLite extension which loads a Google Sheet as a virtual table.
- [libSQL](https://github.com/libsql/libsql) is a fork of SQLite that is both Open Source, and Open Contributions.
- [Is ORM still an 'anti pattern'?](https://github.com/getlago/lago/wiki/Is-ORM-still-an-%27anti-pattern%27%3F)

  > - ["ORMs make the easy parts slightly easier, but they make the hard parts really hard"](https://news.ycombinator.com/item?id=36500429)

  > - Sequelize is extremely simpler and writing code with it is a joy compared to hibernate.
  > - A year ago i had to develop a big Java application without orm (cto’s choice): i didn’t remember how tedious, error prone and slow is development without orm!!! Never do it again!
  > - I think the best approach is to use orm for common crud tasks and add specific sql queries when things get a little bit complicated.
  >   [andretti1977](https://news.ycombinator.com/item?id=36503105)

- [Stop using Knex.js](https://gajus.medium.com/stop-using-knex-js-and-earn-30-bf410349856c) - Using SQL query builder is an anti-pattern
  > Knex.js (and other query builders) was designed to be a building block for ORMs; it does not add value when majority of the query is static.  
  > I recommend that you use a query builder for those few queries that need to be generated dynamically, and use raw SQL for everything else. It is not one or the other; the two work together.
  >
  > > [Slonik](https://github.com/gajus/slonik) - A [battle-tested](https://github.com/gajus/slonik#user-content-battle-tested) Node.js PostgreSQL client with strict types, detailed logging and assertions.
- [What’s the Difference Between OLAP and OLTP?](https://aws.amazon.com/compare/the-difference-between-olap-and-oltp/)

## SQL client

- [DBeaver](https://github.com/dbeaver/dbeaver) - Free universal database tool and SQL client
- [DataGrip](https://www.jetbrains.com/datagrip/)

## Query builder

- [Kysely](https://github.com/kysely-org/kysely) is a type-safe and autocompletion-friendly typescript SQL query builder.

## SQLite

### Tools

- [LiteFS - Distributed SQLite](https://fly.io/docs/litefs/)
- [Turso](https://turso.tech/) which uses SQLite under the hood and even has a concept called "embedded replicas" for zero latency reads.
- [Litestream](https://docs.servicestack.net/ormlite/litestream#litestream)

### [SQLite is not without its shortcomings.](https://www.epicweb.dev/why-you-should-probably-be-using-sqlite#weaknesses)

- SQLite does not support subscriptions which can be a limitation on certain real-time use cases. However, there are plenty of reasons to recommend against using database subscriptions for real-time use cases anyway. Scaling real-time use cases is quite challenging, and personally have really enjoyed letting [Partykit](https://www.partykit.io/) do that part for me in my apps.
- SQLite being a file on disk does make connecting from external clients effectively impossible. But with [Fly.io](http://fly.io/) at least, it’s easy to run prisma studio on the production server and proxy that for local access. If you need to connect to it from another app, then you’re out of luck and have to set up HTTP endpoints on the host app for any data you need ([for now](https://github.com/superfly/litefs/issues/326)).
- SQLite does not support plugins like [TimescaleDB](https://github.com/timescale/timescaledb) for Postgres. While time-series data is possible with SQLite, I do not have experience with this use case and can't speak to the challenges there. My intuition says it's not advisable to use SQLite for that use case, but maybe someone else can offer me more insight.
- SQLite does not support enums which means you're forced to use strings. I have mixed feelings about this, but I mostly don't like enums anyway. The main drawback to this is when it comes to the typings for the client which doesn't allow you to ensure all values of a column are only within a set of specific possible values for the string. However, with Prisma client extensions, handling this kind of enforcement at the client (and typing) level [is possible](https://github.com/L-Steinmacher/epic-stack-with-prisma-client-extensions).

> https://news.ycombinator.com/item?id=38036921
