
# Prisma Migration 가이드

## 개요

Prisma의 마이그레이션 시스템(`migrate dev`, `migrate deploy`)의 동작 원리, Shadow Database 개념, 그리고 실무 워크플로우를 정리한 문서.

## 명령어 해설

```sh
npx prisma migrate dev --name add-compliance-export-log
```

| 부분                 | 설명                                            |
| -------------------- | ----------------------------------------------- |
| `npx`                | `node_modules/.bin`의 로컬 패키지 바이너리 실행 |
| `prisma migrate dev` | 개발 환경용 마이그레이션 명령                   |
| `--name`             | 마이그레이션 폴더 이름 지정                     |

실행 결과로 `prisma/migrations/20260206XXXXXX_add_compliance_export_log/migration.sql` 파일이 생성된다.

## migrate dev vs migrate deploy

|                            | `migrate dev`        | `migrate deploy`          |
| -------------------------- | -------------------- | ------------------------- |
| **용도**                   | 개발 중 스키마 변경  | 프로덕션/스테이징 배포    |
| **마이그레이션 파일 생성** | O (자동 생성)        | X (이미 있는 파일만 적용) |
| **Prisma Client 재생성**   | O (자동)             | X                         |
| **DB 리셋 제안**           | O (충돌 시 프롬프트) | X (절대 리셋 안 함)       |
| **Shadow Database 사용**   | O                    | X                         |
| **대화형 프롬프트**        | O                    | X (실패 시 에러로 종료)   |

요약하면 `dev`는 **마이그레이션을 만드는** 명령, `deploy`는 **만들어진 마이그레이션을 적용하는** 명령이다.

## Shadow Database

`migrate dev` 실행 시 Prisma가 내부적으로 생성하는 **임시 데이터베이스**. 변경사항의 정확한 diff를 계산하기 위한 깨끗한 기준점으로 사용된다.

### 동작 방식

```
1. 임시 DB 생성 (shadow database)
2. 기존 마이그레이션 파일들을 처음부터 순서대로 전부 적용
3. → "DB가 있어야 할 정확한 상태" 확보
4. 이 상태와 schema.prisma를 비교하여 diff 산출
5. diff를 기반으로 새 마이그레이션 SQL 생성
6. 임시 DB 삭제
```

### 실제 DB 인스턴스 필요 여부

Shadow database는 **실제 DB 인스턴스가 필요**하다. 로컬 DB에 `CREATE DATABASE` 권한이 있으면 자동 처리되지만, 클라우드/관리형 DB(RDS, PlanetScale 등)에서는 권한이 없어 별도 지정이 필요하다.

```prisma
datasource db {
  provider          = "mysql"
  url               = env("DATABASE_URL")
  shadowDatabaseUrl = env("SHADOW_DATABASE_URL")
}
```

`SHADOW_DATABASE_URL`에 별도의 빈 DB를 연결하면 된다.

## 이미 테이블이 존재하는 상태에서 migrate dev 실행 시

`schema.prisma`에 정의되어 있지만 마이그레이션 이력에 없는 테이블이 DB에 이미 존재하면, `CREATE TABLE`이 중복 실행되어 **에러가 발생**한다.

### 해결: Baseline 마이그레이션

```sh
# 1. 마이그레이션 파일만 생성 (DB에 적용하지 않음)
npx prisma migrate dev --name add-compliance-export-log --create-only

# 2. 이 마이그레이션을 "이미 적용된 것"으로 표시
npx prisma migrate resolve --applied 20260206XXXXXX_add_compliance_export_log
```

## 표준 워크플로우

DB 변경사항이 있을 때마다 마이그레이션 파일을 생성하고 commit에 포함시켜야 한다.

```
1. schema.prisma 수정
2. npx prisma migrate dev --name 변경내용
3. 생성된 마이그레이션 파일 + schema.prisma 함께 commit & push
4. 프로덕션 배포 시 npx prisma migrate deploy → 자동 반영
```

### commit에 포함되는 파일

```
prisma/
  schema.prisma                              ← 스키마 변경
  migrations/
    20260206XXXXXX_add_compliance_export_log/
      migration.sql                          ← 자동 생성된 SQL
```

### 마이그레이션 파일을 Git에 포함하는 이유

- **다른 개발자**: pull 후 `migrate dev`만 실행하면 동일한 DB 상태
- **CI/CD**: 배포 파이프라인에서 `migrate deploy`로 자동 적용
- **이력 추적**: Git 히스토리로 스키마 변경 이력 확인 가능
- **롤백 판단**: 문제 발생 시 어떤 SQL이 실행됐는지 파일로 확인 가능

## 참고

- [Prisma Migrate 공식 문서](https://www.prisma.io/docs/concepts/components/prisma-migrate)
- Rails의 `db/migrate/`, Django의 `migrations/`도 동일한 방식의 마이그레이션 시스템을 사용
