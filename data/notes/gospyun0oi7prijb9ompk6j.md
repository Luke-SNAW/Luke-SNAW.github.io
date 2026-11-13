
> https://www.unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html

> The name SQLite is a nice name, but the "lite" part is misleading, it sounds like it is only useful for tiny things - which is very wrong. SQLite should be named AwesomeSQL, because that is what it is. SQLite is probably the only database you will ever need in most cases.

[SQLite](https://sqlite.org/) is a relational database management system contained in a C library. It is [ACID-compliant](https://sqlite.org/transactional.html) and implements most of the SQL standard.

It is a popular choice as embedded database software for storage in application software, such as web browsers and mobile phones, and it is the most widely deployed database engine in the world. However, contrary to popular belief SQLite isn't only useful in embedded devices. Whenever you build a website that doesn't need to scale to several machines, then you will in most cases be fine using only SQLite, and not only that, but you will find that your job has just become much easier with SQLite.

In contrast to many other database management systems, SQLite is not a client-server database engine, but you actually very rarely need that. If your application software runs on the same physical machine as the database, which is what most small to medium sized web applications does, then you probably only need SQLite.

Several processes or threads may access the same database concurrently and read accesses can be run in parallel. Because the database consists of a single file, a write access can only be satisfied if no other accesses are currently writing to the database. However, with a configurable [busy timeout](https://sqlite.org/c3ref/busy_timeout.html) set and with [write-ahead logging (WAL)](https://sqlite.org/wal.html) enabled, SQLite enables concurrent reads and writes. This means that writers queue up. Each application does its database work quickly and moves on, and no lock lasts for more than a few milliseconds.

SQLite is [very fast](https://www.sqlite.org/fasterthanfs.html) and it is [very well documented](https://sqlite.org/docs.html).

Even if you start out small and later need to upscale, as long as your web application can run on the same machine as the database, which it can in 99% of the time, you can just upgrade the hardware to a beefier machine and keep business as usual.

The only time you need to consider a client-server setup is:

- Where you have multiple physical machines accessing the same database server over a network. In this setup you have a shared database between multiple clients.
- If your machine is extremely write busy, like accepting thousand upon thousands of simultaneous write requests every second, then you also need a client-server setup because a client-server database is specifically build to handle that.
- If you're working with very big datasets, like in the terabytes size. A client-server approach is better suited for large datasets because the database will split files up into smaller files whereas SQLite only works with a single file.

I have run SQLite as a web application database with thousands concurrent writes every second, coming from different HTTP requests, without any delays or issues. This is because even on a very busy site, the hardware is extremely fast and fully capable of handling that.

Most problems arise when you follow trends and hype and put your applications together by all the "shiny stuff". Then you have all the added complexity because of all the abstractions, and all these things cause problems once performance becomes an important factor.

If you setup SQLite correctly, then in about 99% of the time you actually only need that.

But, what is so great about SQLite then, you might ask?

Well, first of all, all database administration tasks becomes much easier. You don't need any database account administration, the database is just a single file.

Furthermore, you don't need a separate database process running that you need to monitor. If your application is up, then your database is also up!

You can split up your database into multiple separate databases, and you can even give each user his/hers own database on the server. Depending on the application type, you can have a single database that contains all user account information, such as username and password, and you use this for the login session, but once the login has been confirmed, you use another personal database for the work the client is doing. Should the client ever need a copy of his database, simply copy the file and ship it.

> Please note that it is only safe to make a copy of an SQLite database file as long as there are no transactions in progress by any process. If the previous transaction failed, then it is important that any rollback journal (the -journal file) or write-ahead log (the -wal file) be copied together with the database file itself. The recommended way to make a backup is to use the [Online Backup API](https://sqlite.org/backup.html).

Take a look at the [Command Line Shell For SQLite](https://sqlite.org/cli.html) to see some of the really cool stuff you can do with SQLite.

## Differences you need to be aware of

There are two things you need to pay special attention to when you come from one of the popular client-server based databases and that is that the `AUTOINCREMENT` command is different, and also that SQLite uses a dynamically and weakly typed SQL syntax that does not guarantee the domain integrity.

The [`AUTOINCREMENT`](https://sqlite.org/autoinc.html) command in SQLite means that on an `INSERT`, if a `INTEGER PRIMARY KEY` column is not explicitly given a value, then it will be filled automatically with an unused integer, usually one more than the largest ids in use. This is true regardless of whether or not the `AUTOINCREMENT` keyword is used. However, if the `AUTOINCREMENT` keyword appears after `INTEGER PRIMARY KEY`, then that changes the assignment algorithm to prevent the reuse of ids over the lifetime of the database. This means that the purpose of `AUTOINCREMENT` in SQLite is to prevent the reuse of ids from previously deleted rows.

Dynamic and weakly types SQL syntax means that you can insert a string into a column defined as an integer. SQLite will attempt to convert data between formats where appropriate, the string "123" into an integer in this case, but it does not guarantee such conversions and will store the data as-is if such a conversion is not possible. This is **not** a bug, but it is [considered a feature](https://sqlite.org/different.html) (see under "Manifest typing").

## Useful settings

You can list all supported PRAGMA keys for setup with:

```
PRAGMA pragma_list;
```

The settings below are some of the settings I use when I deploy SQLite on a web application. Many other relevant settings exist and your millage may vary.

```
PRAGMA journal_mode = wal;
```

`WAL` and `busy_timeout` are the most important setting when working with a web application.

The `busy_timeout` is associated with each connection to the database and as such you need to set the timeout for each connection.

If e.g. you're using the native SQLite driver in PHP, you need to set the following for each connection:

```php
$sqlite_db->busyTimeout(30000);
```

Where the number in the parentheses is the timeout in milliseconds, in this case 30 seconds.

If you're using PHP PDO instead, then you need to set it like this:

```php
$pdo = new PDO('sqlite:my_database.sqlite', '', '',
array(
PDO::ATTR_TIMEOUT => '30000',
...
)
);
```

Other options that might be relevant, depending on your specific needs are [`PRAGMA temp_store`](https://www.sqlite.org/pragma.html#pragma_temp_store) and [`PRAGMA synchronous`](https://www.sqlite.org/pragma.html#pragma_synchronous)

Be sure you know and understand what each option means.

## Final notes

SQLite is one of those projects that I wish I had known about long before I did. I had heard about it, but for many years I never thought about taking a serious look at it because I was under the false impression that is was a tiny database only useful for personal address books and small embedded devices.

I highly recommend you take a look at SQLite!

## Relevant reading

- [Consider SQLIte](https://blog.wesleyac.com/posts/consider-sqlite)
- [Consider SQLIte](https://news.ycombinator.com/item?id=29727707) (Hacker News)
- [Consider SQLIte](https://lobste.rs/s/0q9w7n/consider_sqlite) (Lobsters)
- [Distinctive Features Of SQLite](https://sqlite.org/different.html)
- [SQLite Autoincrement](https://sqlite.org/autoinc.html)
- [SQLite FAQ](https://sqlite.org/faq.html)
- [Why SQLite succeeded as a database](https://news.ycombinator.com/item?id=22367104) (Hacker News)
- [SQLite small blob storage: 35% Faster Than the Filesystem](https://news.ycombinator.com/item?id=14550060) (Hacker News)
- [SQLite: Small, Fast, Reliable – Choose any three](https://news.ycombinator.com/item?id=8033210) (Hacker News)

---

## [irskep](https://news.ycombinator.com/item?id=34813140)

This sentiment pops up regularly on HN, and I've seen at least one article per month for the past few months, but the trouble is, none of them seem to help you actually deploy it. They assume you're comfortable spinning up public web servers.
If you want to use a PaaS to deploy an app, because you don't want to spend your time learning to be a sysadmin, then all the tutorials are going to put you on the Postgres path, because that's what's supported. (Of course, you'll then end up paying $15+/mo for Postgres, which is hilarious for most hobby projects storing 50MB of data.) But in reality, you could just scale vertically on one machine and be completely fine. No need for "distributed" anything, in theory.

## [briHass](https://news.ycombinator.com/item?id=34813227)

The biggest one missing is date and/or time. The workarounds all suck:

- Store the date as a huge, wasteful string in ISO8601 format

- Store it as Unix epoch seconds

- Store it as a fractional Julian day

Besides the first one, you have to remember how the date is stored and ensure all client libraries handle the conversion. If you want to view or manipulate the latter 2 formats in SQL, you need to chain a bunch of conversion functions.
