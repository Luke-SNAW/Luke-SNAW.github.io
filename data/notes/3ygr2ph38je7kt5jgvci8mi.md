
> https://antonz.org/temp-tables/

Sometimes you want to combine data from multiple tables into one and query the results. For example, join vacancies together with employers and regions:

[Combine, then query](https://antonz.org/temp-tables/combine-then-query.png)

```sql
select v.*, e.name, a.name
from vacancy as v
  join employer as e on e.id = v.employer_id
  join area as a on a.id = v.area_id
```

The question is how to reference the combined dataset in further queries. There are three ways of doing that:

1. Common Table Expressions (CTEs)
2. Views
3. Temporary tables

[CTE](https://antonz.org/temp-tables/cte.png)

A **Common Table Expression** is basically a named subquery:

```sql
with combined_cte as (
  select v.*, e.name, a.name
  from vacancy as v
    join employer as e on e.id = v.employer_id
    join area as a on a.id = v.area_id
)
select ...
from combined_cte
where ...
group by ...
order by ...
```

The CTE is repeated in each query and computed on the fly. So if the subquery for the combined dataset is slow, the entire query will be even slower.

[View](https://antonz.org/temp-tables/view.png)

A **view** works like a CTE, but you can reference it by name and not repeat the subquery every time. Views are computed on the fly, similar to CTEs.

```sql
-- 1) create once
create view combined_view as
select v.*, e.name, a.name
from vacancy as v
  join employer as e on e.id = v.employer_id
  join area as a on a.id = v.area_id;

-- 2) use everywhere
select ...
from combined_view
where ...
group by ...
order by ...
```

PostgreSQL and others have materialized views, which store data on disk. But not SQLite.

[Temporary table](https://antonz.org/temp-tables/temp-table.png)

A **temporary table** is like a real table: it stores data on disk, and you can build indexes. But it exists only while the database connection is open.

```sql
-- 1) create once
create temp table combined_temp as
select v.*, e.name, a.name
from vacancy as v
  join employer as e on e.id = v.employer_id
  join area as a on a.id = v.area_id;

-- 2) use everywhere
select ...
from combined_temp
where ...
group by ...
order by ...
```

Technically, SQLite stores temporary tables in a separate `temp` database. It keeps that database in a separate file on disk, visible only to the current database connection. The temporary database is deleted automatically as soon as the connection is closed.

**Temporary database location**

On unix-like systems, the directory for storing the temp database can be one of the following:

1. The directory set by `PRAGMA temp_store_directory` (deprecated)
2. The `SQLITE_TMPDIR` environment variable
3. The `TMPDIR` environment variable
4. `/var/tmp`
5. `/usr/tmp`
6. `/tmp`
7. The current working directory (`.`)

SQLite picks the first one with both write and execute permissions.

To store the temp database in memory, set `PRAGMA temp_store = MEMORY`.

[documentation](https://sqlite.org/tempfiles.html)

Temporary tables are great for experimenting when you're just getting to know the data. Do whatever you want — everything will be forgotten after disconnecting from the database ツ

---

## https://news.hada.io/topic?id=6581

여러 개의 테이블을 하나로 묶어서 쿼리할 때 선택할 수 있는 옵션은 3가지 : CTE, View, 임시테이블

- CTE : 서브쿼리들을 묶어서 실시간으로 계속 계산되기 때문에 서브쿼리가 느리면 같이 느려짐
- View : CTE 처럼 동작하지만 레퍼런스 가능하고 서브쿼리를 계속 반복하지는 않음. 하지만 역시나 계속 실시간 계산. PostgreSQL 같은 경우는 디스크에 저장하는 Materialized View가 있지만 SQLite에는 없음
- Temporary Table : 실제 테이블 처럼 디스크에 데이터를 저장하고 인덱스 생성도 가능. 하지만 DB 커넥션이 살아있는 동안에만 존재함.
  - SQLite는 임시 테이블을 별도의 temp 데이터 베이스에 저장함
  - temp db는 아예 디스크에서 별도의 파일로 관리하며 현재 DB 커넥션에게만 보임
  - 커넥션이 종료되면 자동으로 삭제
- 임시테이블은 데이터에 대해 뭔가를 알아보고 실험하기에 좋으니 편하게 활용 가능
