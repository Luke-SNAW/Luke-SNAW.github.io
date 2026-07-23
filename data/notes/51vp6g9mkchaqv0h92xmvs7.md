
> https://fly.io/blog/all-in-on-sqlite-litestream/

## Summary of Kagi

SQLite is a powerful embedded database that can serve as the core data and persistence layer for many production applications, rather than just for unit testing.

Modern hardware advancements have made the scaling limitations of SQLite less relevant for most applications, which often don't require handling terabytes of data.

SQLite's simplicity and performance advantages make it an attractive option, as database optimization is becoming less crucial for typical applications.

Litestream is an open-source project that enables reliable replication and distribution of SQLite databases, addressing common concerns around resilience and concurrency.

Litestream allows SQLite databases to be easily replicated to cloud storage or between database instances, providing resilience and scalability.

Embedding the database directly in the application process can dramatically reduce latency compared to client-server database architectures.

The reduced latency and simplified architecture of SQLite with Litestream can improve developer productivity and the user experience of applications.

While Litestream has some limitations, the author is committed to continually improving it to make SQLite a viable option for more full-stack applications.

The author advocates for reconsidering the conventional wisdom that relegates SQLite to only being used for unit tests, and argues it can serve as the core data layer for many production applications.

The document showcases the author's expertise in databases and their passion for making SQLite a more robust and practical option for modern application development.

## Summary of Perplexity

This article discusses the potential of using SQLite as the primary database for full-stack applications, challenging the conventional n-tier architecture wisdom. The author, Ben Johnson, argues that SQLite, combined with Litestream (an open-source replication tool), can be a viable and efficient alternative to traditional client-server databases like PostgreSQL for many applications[1].

Key points include:

1. SQLite's advantages: Simplicity, performance, and reliability.
2. Litestream: A tool that adds replication capabilities to SQLite, addressing concerns about resilience and scalability[1].
3. Operational simplicity: SQLite with Litestream requires less configuration and management compared to traditional databases.
4. Latency benefits: SQLite's embedded nature allows for significantly lower query latency compared to client-server databases[1].
5. Scalability: Litestream enables live replication and distributed read replicas, allowing for global scalability of read-heavy applications[1].

The author argues that while SQLite may not be suitable for all use cases, it should be considered more seriously for many full-stack applications due to its simplicity, performance, and the added reliability provided by Litestream[1].

Citations:
[1] https://fly.io/blog/all-in-on-sqlite-litestream/

## GeekNews

> https://news.hada.io/topic?id=6557

- BoltDB(임베디드 키밸류 DB)를 만든 벤 존슨이 이제 FlyIO에서 Litestream 개발중
- 풀스택 어플리케이션의 상식적인 구조는 n-Tier : 앱서버 + DB서버  
   → 이 아키텍처에서 SQLite는 유닛테스트용으로만 사용했지만, 이제는 데이터 및 지속 레이어로 충분히 사용 가능
- Litestream 은 Replication을 통해서 SQLite를 풀스택 어플리케이션에 사용가능하게 만들어주는 오픈소스

## 어플리케이션 데이터베이스의 간략한 역사

- 50년이 긴 시간이 아니지만, 소프트웨어가 데이터를 관리하는 방법은 엄청난 변화가 있었음  
   → 70년대에는 관계형 데이터베이스라는 것을 정의한 "Codd의 법칙" 이 있었음  
   → 모든 데이터는 테이블에 있고, CRUD, 스키마, SQL 언어 등  
   → 80년대와 90년대에는 Oracle/DB2/Postgres/MySQL등 SQL 데이터베이스가 폭발적으로 많아짐  
   → 2000년대의 XML 데이터베이스는 안 좋았고, 같은 시간대에 훌륭한 컬럼 DB들이 등장  
   → 2010년대에는 대규모 오픈소스 분산 DB 프로젝트들이 출시되고, 이제는 누구나 클러스터를 만들고 테라바이트 단위의 데이터를 쿼리 가능
- 데이터베이스가 진화하면서, DB를 어플리케이션에 연결하는 전략도 발전  
   → Codd 이후로 티어로 분리  
   → 가장 처음엔 데이터베이스 티어  
   → 그다음엔 memcached 와 Redis의 캐슁 티어  
   → 백그라운드 잡 티어(Sidekiq), 라우팅 티어(PgBouncer), Distribution 티어 등  
   → 많은 튜토리얼이 3-Tier 인 것 처럼 얘기하지만, 얼마나 많은 티어들이 들어올지 모르니 "n-Tier"라고 부르고 있음
- 50년의 시간동안 CPU,메모리,디스크가 수백배 빠르고 저렴해지는 것도 보았음  
   → 2010년대 데이터베이스 혁신을 실제 정의하는 단어는 "빅데이터"임  
   → 하지만 하드웨어 개선으로 2020년에 와서는 그 컨셉도 유지하기 어려워졌음  
   → 1996년에 1GB DB 관리는 정말 큰 일이었지만, 2022년엔 노트북이나 t3.micro에서도 운영해도 충분
- 우리가 새로운 DB 아키텍처에 대해 생각할 때, 확장성 제한때문에 최면이 걸림  
   → 페타바이트 또는 최소 테라바이트 단위를 데이터를 처리하지 못하면 대화에 끼지도 못함  
   → 하지만 대부분의 어플리케이션은 성공하더라도 테라바이트의 데이터를 보기 어려움  
   → 우린 못을 박기 위해 착암기(JackHammer)를 쓰고 있는 것

## SQLite의 달콤한 릴리즈

- 이런 경향을 잘 반영하는 데이터베이스가 있음
- 세계에서 가장 유명한 SQL DB중 하나이고, 미국 의회 도서관의 공식 보관 형식이며, 신뢰성과 가늠하기 어려운 크기의 테스트 스위트로 유명하고, 성능도 너무 훌륭
- 이 정도면 이름을 말할 필요도 없겠지만.. 뒤에서 손들고 있는 분을 위해.. 이건 바로 **SQLite** 이야기임
- SQLite는 임베디드 DB임. 일반적인 아키텍처 티어에선 존재하지 않는, 당신의 어플리케이션 서버 프로세스에 링크되는 그냥 라이브러리 임  
   → 다른 서버에 의존하지 않고 혼자 실행 되는 "싱글 프로세스 어플리케이션"
- 내가 DB를 만드는 사람이기 때문에 이런 종류의 어플리케이션에 관심을 가짐
- 나는 Go 에코시스템에서 유명한 임베디드 Key/Value DB인 BoltDB를 만들었음
- BoltDB는 안정적이고, 인프로세스 DB에서 기대하는 것처럼 Nitro가 달린 장난감 자동차 같은 성능을 보여줌
- 하지만, BoltDB는 제한점이 있음  
   → 스키마가 Go코드로 정의되기 때문에 DB 마이그레이션이 어려움. 직접 당신이 도구를 만들어야 함. 심지어 REPL도 없음
- 당신이 조심만 한다면, 이런 종류의 DB를 쓰면 엄청난 성능을 얻을 수 있음
- 하지만 일반적인 용도로는 이런 DB를 운영하기 원하지 않을 것
- 나는 BoltDB를 더 많은 어플리케이션에서 사용가능하게 만들기 위해 뭘 해야할지를 고민했는데, 내가 도달한 결론은 "SQLite가 딱 그것을 위해 만들어졌다는 것"
- SQLite에도 물론 제약이 있음. 가장 큰것은 단일 프로세스 어플리케이션은 SPOF(Single Point of Failure)가 있다는 것: 서버를 잃어버리면 데이터베이스도 잃어버림. 이것은 SQLite의 결함이 아니라 디자인이 원래 그렇게 된 것

## Enter Litestream

- 많은 사람들이 SQLite를 기본으로 사용하지 않는 두가지 큰 이유는  
   → 첫째 스토리지 오류에 대한 복원력(Resilience)  
   → 둘째 규모가 클 때의 동시성(Concurrency)
- Litestream이 이 두가지 문제에 대해서 할 말이 있음
- Litestream은 SQLite 의 WAL(Write Ahead Log) 모드 저널링을 제어함으로써 동작
- WAL모드에서는 쓰기 오퍼레이션들이 SQLite의 메인 DB 파일외의 별도 로그파일에 추가됨
- Reader들은 쿼리를 충족시키기 위해 WAL 파일과 메인DB를 모두 확인함
- 일반적으로 SQLite는 자동으로 WAL에서 메인 DB로 페이지를 자동 체크포인트를 실행함
- Litestream은 이 중단단계에서 끼어들어 자동 체크포인트를 방지하는 무한 읽기 트랜잭션을 오픈하고, WAL업데이트를 직접 캡쳐하고 복제하고, 스스로 체크포인트를 트리거함
  > Litestream에 이해해야 하는 가장 중요한 것은 그냥 SQLite라는 것. 애플리케이션은 표준 SQLite를 사용하며, 종속성을 추가하거나 쿼리를 분석하거나 프록시 동작을 하는게 아님. 그냥 SQLite가 가진 저널링 및 동시성 기능을 활용하는 것. 대부분의 경우 당신의 코드는 Litestream의 존재를 인식하지 못할 수도 있음
- 복잡해 보이지만, 실제로는 엄청 간단함. 써보면 그냥 "just works"라는 걸 알수 있음
  ```shell
  $ litestream replicate fruits.db [s3://my-bukkit:9000/fruits.db](https://s3//my-bukkit:9000/fruits.db)
  $ litestream restore -o fruits-replica.db [s3://my-bukkit:9000/fruits.db](https://s3//my-bukkit:9000/fruits.db)
  ```
- 일반적으로 사람들은 SQLite DB를 복제해서 S3에 저장하는 용도로 사용
- 운영상 큰 이점을 줌. 당신의 DB는 탄력적이고 쉽게 옮기거나 마이그레이션 가능해짐
- 하지만 Litestream으로 더 많은 것들을 할 수 있음.
- 다음 버전에서는 SQLite DB간에 실시간 복제가 가능해져서, 분산 Read Replica 와 Write-Leader DB를 셋업하는게 가능해 짐  
   → Read Replica는 Write를 캐치해서 Leader에게 Redirect 가능  
   → 많은 어플리케이션들은 Read-heavy니까 이 셋업은 어플리케이션에게 글로벌하게 스케일 가능한 DB를 제공할수 있게 되는 것

## 당신은 이 옵션(어플리케이션 DB로 SQLite를 사용하는 것)을 더 심각하게 받아들여야 함

- 나의 초창기 IT 직업중 하나는 2000년대 초 오라클DBA 였음
- 나는 오라클에 대해서 배우기 위해 수많은 책과 문서들을 읽는데 시간을 보냈음
- 관리자 매뉴얼은 거의 천페이지 가량이었고, 그건 수백개의 문서중 하나였음
- 쿼리를 최적화 하거나 쓰기를 개선하기 위해 뭘 해야 하는 지를 배우면 그 당시에는 큰 차이를 만들어냈음
- 초당 수십메가를 읽는 하드디스크가 있으므로, 더 나은 인덱스를 활용하면 5분 걸리는 쿼리를 30초 짜리 쿼리로 바꿔줄수 있음
- 하지만 DB최적화는 점점 일반 어플리케이션엔 중요하지 않아짐
- 1GB DB를 가지고 있다면 NVMe디스크는 1초 이내에 모든 것을 메모리에 담을 수 있음
- SQL 쿼리 최적화를 좋아하지만, 많은 어플리케이션 개발자들에게 이건 죽어가는 기술이 되고 있음
- 제대로 튜닝되지 않은 쿼리라도 많은 데이터베이스에서 1초이내에 실행 가능
- 최신 Postgres는 기적임. 수년간 그 코드를 읽으면서 많은 것들을 배웠음
- 쿼리 옵티마이저, 행단위 보안 정책, 6가지 유형의 인덱스 등
- 이런 기능을 원한다면 필요하겠지만, 대부분은 그렇지 않음
- 그리고 만약 이런 Postgres 기능을 원하지 않는다면, 책임이 뒤따름
- 여러개의 계정을 사용하지 않더라고 호스 기반 인증을 구성해야 하고, 방화벽을 해제해야함
- 더 많은 기능은 더 많은 문서를 의미하므로 실제로 당신이 운영중인 소프트웨어에 대해 알기 어려움
- Postgre14 의 문서는 거의 3천페이지임
- SQLite는 Postgres 기능의 서브셋을 가짐. 하지만 내가 일반적으로 원하는 기능의 99.9% 임
- 뛰어난 SQL 지원, 윈도우 기능, CTE, 전문 검색, JSON 지원 등
- 기능이 부족하자면 데이터가 내 애플리케이션 옆에 있으므로 가져와서 처리하기에 오버헤드가 별로 없음
- 한편 정말 해결해야 하는 복잡한 문제는 핵심 데이터베이스 기능으로는 해결되지 않음
- 대신 레이턴시와 개발자 경험 두가지만 최적화 하고 싶음
- 따라서, SQLite를 진지하게 고려해야 하는 한가지 이유는 운영이 정말 간단하기 때문
- 데이터베이스 계층을 설계하지 않고 그냥 어플리케이션 코드 작성에 시간을 쓰는 것이 가능
- 하지만 다른 문제가 있음

## 빛은 너무 느리다 : The Light is Too Damn Slow

- 이론적인 한계에 부딪히기 시작. 진공상태에서 빛은 1밀리초에 186마일을 이동(필라델피아에서 뉴욕까지 왕복 거리)
- 네트워크 스위치, 방화벽 및 애플리케이션 프로토콜 레이어를 추가하면 더 느려짐
- 단일 AWS 리젼내에서 Postgres 쿼리에 대한 레이턴시 오버헤드는 최대 1밀리초 이내
- 이것은 Postgres가 느리다는 것이 아니라 데이터 이동 속도의 한계에 도달한 것
- 최신 어플리케이션은 HTTP 요청을 처리하며, 여러개의 데이터베이스 쿼리와 비즈니스 로직 또는 렌더링 하기 전에 이미 10ms를 소모함
- 애플리케이션 레이턴시에는 매직 넘버가 있음 : 100ms 이하의 응답은 거의 즉시처럼 느껴 진다는 것
- 즉시 응답하는(Snappy) 어플리케이션은 행복한 사용자를 만듦
- 100ms는 많은 것 같지만 무심코 먹어버리기 쉬움
- 100ms 임계값은 매우 중요하기 때문에 사람들은 레이턴시를 줄이기 위해 페이지를 프리렌더링하고 CDN에 태움
- 우린 데이터를 어플리케이션 가까이로 옮기는게 좋음. 얼마나? 정말 가깝게
- SQLite는 당신의 어플리케이션과 같은 머신에 있는 것만이 아니라, 당신의 어플리케이션 프로세스 안에 포함됨
- 데이터를 어플리케이션 옆에 두면 쿼리당 레이턴시가 10~20 마이크로세컨드(μ)로 떨어지는 것을 볼수 있음
- 즉 동일 리젼내의 Postgres 쿼리보다 50~100x 빠름
- 하지만, 더 많은 것이 있음. 쿼리당 지연시간을 효율적으로 제거했음. 우리 어플리케이션이 빠르면서도 더 간단함
- 큰 쿼리들을 더 작은 관리 가능한 쿼리로 분할할 수 있고, 새로운 기능을 구축하기 위해 N+1 쿼리 패턴을 찾는데 시간을 더 할애할 수 있음
- 레이턴시를 최소화 하는 것은 프로덕션만을 위한 것은 아님. 기존 클라이언트/서버 DB와 연통 테스트를 하는 것은 로컬에서 몇분씩 걸릴 정도로 곧 잘 늘어나며, CI로 푸시해도 고통은 계속 됨
- 코드 변경에서 테스트 완료까지의 피드백 루프를 줄이면 시간이 절약되고 개발하는 동안 포커스를 유지할 수 있음
- SQLite에서 한 줄 변경하는 것은 메모리에서 실행해서 통합 테스트를 몇 초 이내에 실행 가능

## 작고, 빠르고, 신뢰할수 있고, 글로벌 분산되어 있고 : 이 중에서 4개를 선택하세요

- Litestream 은 분산 되어있고, 복제되며, 가장 중요한 것은 **이해하기 쉬움**
- 진지하게, "한번 시도해 보세요" 알아야할 것이 별로 없습니다
- 내 주장은 이겁니다 :
  - SQLite를 위한 안정적이고 사용하기 쉬운 복제를 구축하면, SQLite에서만 운영되는 풀스택 어플리케이션을 매력적으로 만든다는 것
  - 예전 "Rails로 Blog로 만들기 튜토리얼"이 작성되었던 시절엔 이 옵션을 간과했지만, 요즘의 SQLite는 대부분의 어플리케이션 쓰기 부하를 견딜수 있으며, 복제본을 통해서 수많은 인스턴스에서 읽어갈수 있도록 로드밸런싱이 가능
- Litestream에도 제약이 있음
  - 싱글 노드 어플리케이션을 위해 만들었기 때문에, 서버리스 플랫폼이나 롤링 배포에는 잘 동작하지 않음
  - 모든 변경사항을 순차적으로 복원해야 하므로 DB 리스토어에 몇분가량 걸릴수 있음
  - 우리는 실시간 복제 기능을 준비하고 있지만, 별도 프로세스 모델은 복제 보장에 대한 세부제어 부분에서 제약이 있음
- 더 잘할 수 있음
  - 지난 1년간 내가 해온 일은 Litestream의 핵심을 정하고 정확성에 초점을 맞추는 것
  - 현재 도착한 위치에 만족함
  - 단순한 스트리밍 백업 도구로 시작했지만, 점차 안정적이고 분산된 데이터베이스로 발전 중
  - 나의 Fly.io에서의 일은 이걸 더 빠르고 심리스하게 만드는 것
  - Fly.io 와 상관없이 Litestream에 더 많은 개선들이 추가 될 것
- Litestream 은 Fly.io에서 새 집을 꾸렸지만, 계속 오픈소스 프로젝트 일 것
- 차후 몇년간 내 계획은 어플리케이션이 어디서 실행되는 지와 상관없이, 더 유용하게 만들고, SQLite 모델이 어디까지 나아갈수 있을지 확인하는 것
