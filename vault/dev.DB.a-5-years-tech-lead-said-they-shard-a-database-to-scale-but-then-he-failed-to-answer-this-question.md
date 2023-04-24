---
id: dupv50hv9j8gm104qlwm9o7
title: "A 5 years+ tech lead said they shard a database to scale but then he failed to answer this question"
desc: ""
updated: 1682321769201
created: 1682321642227
published: false
---

> https://iorilan.medium.com/a-5-years-tech-lead-said-they-shard-a-database-to-scale-but-then-he-failed-to-answer-this-question-8be39115dcb0

Never talk about something you do not fully understand during an interview

Another interview story.

Q: “Introduce yourself and the recent project you are working on, as detail as possible”.

A: “Sure, I’m …, working at an internet company, a public-facing platform that serves millions of requests per minute..blabla.. my team is a search module, and we provide search services to other teams.”

Q: “Ok, what technology is used in your team, and what is your scope, any challenges you have been facing, and how have you solved them”.

A: “blabla… by the way we scaled our database (MySQL) by sharding. it is fast and scalable”.

Q: “Interesting, why go for sharding?”

A: “It is a big table. data keep increasing in a single table, search becomes slow as it grows, we need them to be split into different machines. so the search is faster and scales horizontally”

Q: “Okay. how do you shard it, range-based or key based? If key, what is the sharding key?”

A: “We use hash, sharding key is xx.”

Q: “Could you tell me how to query the recent 500th to 1000th updated records and order by modified date? ”

A: “….” ## after 3 minutes

Q: “You have to query all databases and order by modified (must be indexed well) and limit 500 offsets 500 then merge in memory right?” I tried to continue the conversation.

A: “No we have our own algorithm to do it more efficiently…”

He drew something on the whiteboard Id \[0,5000\]-machineA, Id\[5001, 10000\]-machineB, … then I reminded him “you told me your sharding key is hash right 😄?”, he stopped and spent a few minutes thinking, didn’t come up any more answer.

Then we discussed something else, and the interview finished in another 3 mins.

To this topic, there are much more difficult questions ahead in my mind:

- When you add a new machine, do you need re-shard? and how did you handle it?
- How do you handle schema changes?
- How do you join tables? Does your code have no sub-query? and what if you have to use it? Is there an alternative approach?
- How do you make sure data integrity? after you did sharding, you threw away the entire ACID (primary key only applies to local shard table) which came from RDBMS: data loss and inconsistency now become possible.
- And all the aggregating functions like count, sum, and max become challenging, there must be a high-performance and mature sharding proxy or “merging engine” like [vitess](https://vitess.io/docs/) or [shardingsphere](https://github.com/apache/shardingsphere) in the middle. and you need to master this engine to save your ass.
- How is the transaction handling different from a single database?
- …

Never talk about something you are not sure about during an interview. 🙂

Today let’s spend a few minutes talking about scaling the database.

First thing, you will not want to go sharding in the first place.

Unless you tried all the possible options, otherwise, never shard your database (even for NoSQL which naturally support distributed system, do not shard until you have to).

Why?

It makes things super complicated.

So let’s follow this interviewee’s problem, he has a database table, that keeps growing, and makes queries slow, how to solve it?

## First, split tables

Yes, sharding, but vertically.

To mitigate the table growing issue, we need to split the columns into 2 categories:

- Frequently changes (red)
- No or fewer changes (blue)

So that we can eliminate tracking those unchanged rows.

[split tables](https://miro.medium.com/v2/resize:fit:653/1*zr0c-xfU71AzJM_bAwSo-g.png)

So let’s say it is an online shopping system. We have a product table with some columns rarely change after first creation, like _id, name photo_. and some columns that may need to be updated frequently like _supplier or warehouse_id and verified employee id_.

by splitting it into 2 tables. we reduced the writes into the product_basic table.

So indirectly we reduced the potential locks on the old big table, and improved the performance.

Okay you may ask “Wait. this is the problem: we have a table, that keeps growing, and using the above solution will still end up with a huge product_etx table”

Sure we can continue to try something else.

## Then, try the simplest way first, to Archive

Keep the busy database small.

Archive the old records (split the cold and hot data). create an archiving database and move data over there every month or year.

Do not forget to compress the files if your database supports this feature.

So if you need to search historical data, go to this archive database, if you find the schema is not what you want, you can even create a reporting database and flow the data there for your purpose (you can build an ETL in between if needed).

So you may ask “Wait, What if after archiving it is still slow, because we can only archive 5 years ago data”.

Sure. we try something, and no still not sharding.

## Read-Write Splitting

[Read-Write Splitting](https://miro.medium.com/v2/resize:fit:632/1*j8oiqeGGAjbiOLCd3CM3XA.png)

- Master-Slave + replica
- Read goes to slaves, Write into master
- One way sync master to slaves (most database support this)

If archiving itself doesn’t solve the problem. on top of that, we split read/write.

You may want to check out CQRS + event sourcing which is a very mature proven working solution for years.

You may wonder What if this case “very high concurrency (10k+ RPS) happens, so race-conditioning the same rows causes a lot of deadlocks. it may even kill MySQL.”

Sure, you can add a cache for that high frequent accessed table data in front to protect the database.

But since you introduced cache then remember to write through or use invalidate date to control the expiration of the caching data.

And if needed, make a cache cluster as well.

“No, the cache only deal with the concurrency but didn’t do anything to the fast-growing table, archiving too much data is not an option, and read-write is not enough to get the performance.”

Well. okay. let’s try one more.

## Table Partition

[Table Partition](https://miro.medium.com/v2/resize:fit:659/1*08G7EiJFwpddMfOb9JgxUQ.png)

By time range. the data will be split into different partition physical files and all are managed by MySQL.

Yes the limitation, or the difference from sharding (range based) is, all partitions are on the same machine.

You may ask ”Wait, It didn’t solve the issue, right? it is not scalable. I can not scale the solution by adding a new machine.”

but you can add a new disk, right?

“In the end, the machine will be a bottleneck”.

Well, true, you are right. let’s continue.

## Sharding, but range based

[Sharding, but range based](https://miro.medium.com/v2/resize:fit:670/1*eqH2cV_Cjm8jRv29MdzPRg.png)

In our application logic layer, we can route the data to different databases based on logical ids.

It could be _customer_id or user_id, time range, location_id, or city_id, etc._ the load will be balanced at the application layer.

If one of the machines has a problem, only affects the particular location or city or range of customers.

This solution is scalable, balanced the load, and also splits the risk.

Okay you may ask ”what if in my case, the single location or city_id data grows still very very huge? Yes, I mean the data hotspot case, so we need another solution.”

Well, you should choose the sharding key very very carefully to avoid this happening…

Btw, this is the max level of complexity I could accept for a database solution. beyond which is a bit out of control.

## Key-based sharding

Let’s say 2 machines. the hashing function is as simple as row_id%2. row_id%2==0 go to machine1 and another one go machine2

[Key-based sharding](https://miro.medium.com/v2/resize:fit:700/1*S-jfRXHuBRWu0YKAoQU_EA.png)

It only looks simple, but If possible, I never want to reach here.

The “cons” make me stop thinking about it.

**Cons**

- I can never use incremental Id as the primary key.
- Primary or foreign keys and unique keys do not make sense anymore. it is only applied to the shard database table. we need another solution to get this feature back.
- The hashing function needs to be chosen very very carefully. e.g. For the above sample, when I add a machine, need to change the function into row_id%3. which is very very bad — re-shard is the cost is very very high: migration is complicated, potentially may lose data, and the downtime is unknown.
- Need to rewrite many queries (into very simple ones). no subquery, no joins, and no aggregate functions can be used.
- The transaction is hard to control. [distributed system transaction is already complicated](https://iorilan.medium.com/i-asked-this-system-design-question-to-3-guys-during-a-developer-interview-and-none-of-them-gave-9c23abe45687), sharding makes it even harder.
- When a slow query (after a query from multiple machines then merges and sorts in memory) happens, my luck depends on caching or the engine in the middle like [vitess](https://vitess.io/docs/) or [shardingsphere](https://github.com/apache/shardingsphere).
- With above. horizontal sharding seems more suitable for NoSQL. but I don’t try until I have to.

**Pros (compared to range based)**

- No data hotspot problem
- Nothing more -\_-!

So, we may still want to know, “I know all the cons, what if we have to use it”. so when this happens, don’t build it yourself, even if you are confident to handle all the above “cons”.

- Try with NoSQL first. it is naturally distributed and mostly has more built-in features to support sharding
- If you have to use SQL like MySQL. use some proven engine like vitess (used by youtube). [here is an example of how slack did it.](https://slack.engineering/scaling-datastores-at-slack-with-vitess/)
- If doesn’t work, try another engine, keep trying, and use the existing solution, never build it yourself.

## Recap

when scaling a big table with growing data.

#1 Try the simplest way first

#2 It does not work then slowly adds complexity

#3 Keep balancing the benefits that the complexity brings.

#4 Never jump into any complicated solutions (even if it looks sexy).

- Scale up: Add RAM/CPU (CPU bound) or use SSD (I/O bound). whenever possible.
- Reuse existing mature proven solutions. e.g. handle growing logs searching, throwing them into ELK.
- Review table fields. categorize the fields by updating frequency. put those fields updated more frequently into one table and others into another table.
- Archive history data + Split read and write + replica + Cache (In many cases, we stopped here, all below solutions has risk)
- Table partition (by date range). — risk: be mindful of the physical file size and the usage of an information schema.
- Sharding, range based (choose the key carefully, avoid hotspot data) — risk: think carefully when choosing the key, avoid hotspot. and if this happens, changing back to key-based is almost impossible.
- Is the data structure could be fit into any NoSQL? migrate there — risk: mysqldump is not possible. select into outfile csv then import seems the only way, to benchmark more and test all languages, and special chars.
- Shard by key. check Vitess and other existing proven shard engines. setup and reuse. — risk: Sorry I don’t know what could happen to you, good luck. :)

## Last

That’s it, hope you liked it.

Again, never talk about something you do not fully understand during an interview.
