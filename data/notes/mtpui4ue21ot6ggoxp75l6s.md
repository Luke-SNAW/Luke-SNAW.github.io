
> https://dev.mysql.com/blog-archive/mysql-explain-analyze/

[MySQL 8.0.18 was just released](https://dev.mysql.com/blog-archive/the-mysql-8-0-18-maintenance-release-is-generally-available/), and it contains a brand new feature to analyze and understand how queries are executed: EXPLAIN ANALYZE.

## What is it?

EXPLAIN ANALYZE is a profiling tool for your queries that will show you where MySQL spends time on your query and why. It will plan the query, instrument it and execute it while counting rows and measuring time spent at various points in the execution plan. When execution finishes, EXPLAIN ANALYZE will print the plan and the measurements instead of the query result.

This new feature is built on top of the regular EXPLAIN query plan inspection tool, and can be seen as an extension of the EXPLAIN FORMAT=TREE that was added earlier in MySQL 8.0. In addition to the query plan and estimated costs, which a normal EXPLAIN will print, EXPLAIN ANALYZE also prints the actual costs of individual iterators in the execution plan.

## How do I use it?

An EXPLAIN FORMAT=TREE will show us the query plan and cost estimates:

```sql
EXPLAIN FORMAT=TREE
SELECT first_name, last_name, SUM(amount) AS total
FROM staff INNER JOIN payment
  ON staff.staff_id = payment.staff_id
     AND
     payment_date LIKE '2005-08%'
GROUP BY first_name, last_name;

-> Table scan on <temporary>
  -> Aggregate using temporary table
    -> Nested loop inner join  (cost=1757.30 rows=1787)
      -> Table scan on staff  (cost=3.20 rows=2)
      -> Filter: (payment.payment_date like '2005-08%')  (cost=117.43 rows=894)
        -> Index lookup on payment using idx_fk_staff_id (staff_id=staff.staff_id)  (cost=117.43 rows=8043)
```

But it doesn’t tell us if those estimates are correct, or on which operations in the query plan the time is actually spent. EXPLAIN ANALYZE will do that:

```sql
EXPLAIN ANALYZE
SELECT first_name, last_name, SUM(amount) AS total
FROM staff INNER JOIN payment
  ON staff.staff_id = payment.staff_id
     AND
     payment_date LIKE '2005-08%'
GROUP BY first_name, last_name;

-> Table scan on <temporary>  (actual time=0.001..0.001 rows=2 loops=1)
  -> Aggregate using temporary table  (actual time=58.104..58.104 rows=2 loops=1)
    -> Nested loop inner join  (cost=1757.30 rows=1787) (actual time=0.816..46.135 rows=5687 loops=1)
      -> Table scan on staff  (cost=3.20 rows=2) (actual time=0.047..0.051 rows=2 loops=1)
      -> Filter: (payment.payment_date like '2005-08%')  (cost=117.43 rows=894) (actual time=0.464..22.767 rows=2844 loops=2)
        -> Index lookup on payment using idx_fk_staff_id (staff_id=staff.staff_id)  (cost=117.43 rows=8043) (actual time=0.450..19.988 rows=8024 loops=2)
```

There are several new measurements here:

- Actual time to get first row (in milliseconds)
- Actual time to get all rows (in milliseconds)
- Actual number of rows read
- Actual number of loops

Another tool in the MySQL query analysis toolbox:

- To examine the query plan: EXPLAIN FORMAT=TREE
- To profile the query execution: EXPLAIN ANALYZE
- To understand plan choices: [Optimizer trace](https://dev.mysql.com/doc/internals/en/optimizer-tracing.html)
