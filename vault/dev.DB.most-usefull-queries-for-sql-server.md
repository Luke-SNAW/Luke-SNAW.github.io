---
id: ruxi56ufclxkq9d9zd9z0zu
title: Most Usefull Queries for Sql Server
desc: ""
updated: 1671694727012
created: 1671694478969
published: false
---

> https://towardsdev.com/most-usefull-queries-for-sql-server-596dda5742c1

## Find Most Expensive Queries

Find the most expensive queries for sql server. You can change the ORDER BY clause to get results against the different parameters. This query is valid on any version of SQL Server from SQL Server 2005 or later version of SQL Server. Source [link](https://blog.sqlauthority.com/2010/05/14/sql-server-find-most-expensive-queries-using-dmv/)

```sql
SELECT TOP 10 SUBSTRING(qt.TEXT, (qs.statement_start_offset/2)+1,
					   ((CASE qs.statement_end_offset WHEN -1 THEN DATALENGTH(qt.TEXT)
						ELSE qs.statement_end_offset END - qs.statement_start_offset)/2)+1),
	qs.execution_count,
	qs.total_logical_reads, qs.last_logical_reads,
	qs.total_logical_writes, qs.last_logical_writes,
	qs.total_worker_time,
	qs.last_worker_time,
	qs.total_elapsed_time/1000000 total_elapsed_time_in_S,
	qs.last_elapsed_time/1000000 last_elapsed_time_in_S,
	qs.last_execution_time,
	qp.query_plan
FROM sys.dm_exec_query_stats qs
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) qt
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle) qp
ORDER BY qs.total_logical_reads DESC -- logical reads
-- ORDER BY qs.total_logical_writes DESC -- logical writes
-- ORDER BY qs.total_worker_time DESC -- CPU time
```

## Find Most Expensive Queries with different query

You can find expensive queries for various resources like CPU, IO as well as for Elapsed time. If you pay attention there are a few commented ORDER BY clauses, you can use each of them to find resource expensive queries. Sources [link](https://blog.sqlauthority.com/2021/03/17/sql-server-list-expensive-queries-updated-march-2021/)

## Find the Currently Running Queries

## Find Sql Query text of a Spid

## Find indexes that are not used at all or used rarely

The `sys.dm_db_index_usage_stats` DMV tracks index usage statistics since the last time the SQL Server instance was restarted. This information can be useful for identifying which indexes are being used frequently and which ones are not being used at all. It can also help you to identify potential performance issues, such as scans that are slower than seeks or updates that are causing the index to become fragmented. The query returns the following information:

- `USER_SEEKS`: the number of times the index has been used to seek to a specific row
- `USER_SCANS`: the number of times the index has been scanned from start to finish
- `USER_LOOKUPS`: the number of times the index has been used to look up a row based on its index key
- `USER_UPDATES`: the number of times the index has been updated (e.g. when a row is inserted, updated, or deleted)

The query is using a join to the `sys.indexes` system catalog view to retrieve the index names. It is also using the `DB_NAME` function to retrieve the database name for the table or view.

To run this query, you will need to specify a database name by replacing `dbname` with the name of the database that you want to query.

````sql
use dbname
go

SELECT
OBJECT_NAME(IUS.[OBJECT_ID]) AS [OBJECT NAME],
DB_NAME(IUS.database_id) AS [DATABASE NAME],
I.[NAME] AS [INDEX NAME],
USER_SEEKS,
USER_SCANS,
USER_LOOKUPS,
USER_UPDATES
FROM sys.dm_db_index_usage_stats AS IUS
INNER JOIN sys.indexes  AS I
ON I.[OBJECT_ID] = IUS.[OBJECT_ID]
AND I.INDEX_ID = IUS.INDEX_ID```
````

## Find the 20 worst instantly performing queries

The `sys.dm_exec_query_stats` view provides statistical information about the performance of queries that have been executed on an instance of SQL Server. It returns one row for each query plan that is cached in the plan cache, along with statistical information about the number of times the plan has been executed and the total elapsed time and CPU time that have been consumed by the plan. The `sys.dm_exec_sql_text` function returns the text of a SQL batch or stored procedure given its `sql_handle`.

```sql
SELECT TOP 20
total_worker_time/execution_count AS Avg_CPU_Time
,Execution_count
,total_elapsed_time/execution_count as AVG_Run_Time
,total_elapsed_time
,(SELECT
SUBSTRING(text,statement_start_offset/2+1,statement_end_offset
) FROM sys.dm_exec_sql_text(sql_handle)
) AS Query_Text
FROM sys.dm_exec_query_stats
ORDER BY Avg_CPU_Time DESC
```

## List of all your tables in order of reserved size, ordered from largest to smallest

The code then inserts rows into the `#tmpTableSizes` table using the `EXEC sp_MSforeachtable @command1="EXEC sp_spaceused '?'"` command. This command executes the `sp_spaceused` stored procedure for each table in the database, and inserts the results into the `#tmpTableSizes` table. The `sp_spaceused` stored procedure returns the space used by a table, including the number of rows, reserved size, data size, index size, and unused space.

```sql
CREATE TABLE #tmpTableSizes
(
    tableName varchar(100),
    numberofRows varchar(100),
    reservedSize varchar(50),
    dataSize varchar(50),
    indexSize varchar(50),
    unusedSize varchar(50)
)
insert #tmpTableSizes
EXEC sp_MSforeachtable @command1="EXEC sp_spaceused '?'"

select  * from #tmpTableSizes
order by cast(LEFT(reservedSize, LEN(reservedSize) - 4) as int)  desc

DROP TABLE #tmpTableSizes
```

## Get all Database Names and Current Sizes

Get all database names and current size except system databases.

```sql
SELECT  DB_NAME(database_id) AS database_name,
    type_desc,
    name AS FileName,
    size/128.0 AS CurrentSizeMB
FROM sys.master_files
WHERE database_id > 6 AND type IN (0,1)
```

## List of all the Jobs

Get a list of all SQL Server Agent Jobs and Job steps.

```sql

SELECT
     job.job_id,
     notify_level_email,
     name,
     enabled,
     description,
     step_name,
     command,
     server,
     database_name
FROM msdb.dbo.sysjobs job
INNER JOIN   msdb.dbo.sysjobsteps steps
ON job.job_id = steps.job_id
WHERE  job.enabled = 1 -- remove this if you wish to return all jobs
```
