---
id: d1taedacxa8xx4bcxvhfhz5
title: AWS RDS Blue/Green Deployment QA
desc: ""
updated: 1769661367292
created: 1769661323926
---

Claude Opus 4.5 문답

# AWS RDS Blue/Green 배포 Q&A

## 1. Blue 환경의 변경사항이 Green에 자동 반영되는가?

**네, 자동으로 복제됩니다.**

| 항목                               | 자동 복제 여부             |
| ---------------------------------- | -------------------------- |
| 데이터 변경 (INSERT/UPDATE/DELETE) | ✅ 자동 복제 (논리적 복제) |
| 스키마 변경 (DDL)                  | ⚠️ 복제되지만 주의 필요    |
| 파라미터 그룹 변경                 | ❌ 별도 적용 필요          |
| DB 엔진 버전                       | ❌ Green에서 별도 설정     |

**주의사항:**

- Green 환경은 생성 시점부터 Blue의 변경사항을 **논리적 복제(Logical Replication)**로 동기화
- DDL 변경(테이블 구조 변경 등)은 복제 지연이나 오류를 일으킬 수 있음
- Switchover 전까지 Green은 **읽기 전용**
- Switchover 시 약 1분 미만의 다운타임 발생

---

## 2. Switchover 후 엔드포인트는 어떻게 전환되는가?

**기존 엔드포인트로 접근하면 자동으로 새 Blue(이전 Green)에 연결됩니다.**

**Switchover 전:**
| 환경 | 인스턴스 ID | 엔드포인트 |
|------|------------|-----------|
| Blue (현재 운영) | `partners-product` | `partners-product.xxx.rds.amazonaws.com` |
| Green (대기) | `partners-product-green-1ngi7u` | `partners-product-green-1ngi7u.xxx.rds.amazonaws.com` |

**Switchover 후:**
| 환경 | 인스턴스 ID | 엔드포인트 |
|------|------------|-----------|
| 새 Blue (운영) | `partners-product` | `partners-product.xxx.rds.amazonaws.com` ← Green이 승격 |
| 이전 Blue | `partners-product-old1` | `partners-product-old1.xxx.rds.amazonaws.com` |

**핵심 포인트:**

- 애플리케이션의 `DATABASE_URL`을 변경할 필요 없음
- 이전 Blue 인스턴스는 `-old` 접미사가 붙은 새 이름으로 변경되어 유지됨

---

## 3. Switchover 중 데이터 조작은 어떻게 처리되는가?

**Switchover 중 쓰기 작업은 차단(block)됩니다. 따로 저장 후 나중에 적용되지 않습니다.**

**Switchover 과정:**

1. **쓰기 차단** - Blue 환경의 쓰기 작업 중단
2. **복제 완료 대기** - Green이 Blue의 모든 변경사항을 따라잡을 때까지 대기
3. **엔드포인트 전환** - DNS 전환
4. **쓰기 재개** - 새 Blue(이전 Green)에서 쓰기 허용

**쓰기 요청 처리 방식:**

| 상황                               | 결과                         |
| ---------------------------------- | ---------------------------- |
| Switchover 중 INSERT/UPDATE/DELETE | 연결 대기 또는 타임아웃 에러 |
| Switchover 중 SELECT               | 짧은 지연 후 성공 가능       |
| Switchover 완료 후                 | 정상 처리                    |

실패한 트랜잭션은 애플리케이션에서 재시도해야 합니다.

**애플리케이션 권장 사항:**

- DB 연결에 재시도 로직 구현
- 타임아웃 설정 적절히 조정
- Switchover는 트래픽이 적은 시간대에 수행

---

## 4. Switchover 후 롤백이 가능한가?

**자동 롤백 기능은 없습니다.** 하지만 수동으로 되돌릴 수 있습니다.

**Switchover 후 상황:**

- 이전 Blue 인스턴스(`partners-product-old1`)가 그대로 유지됨
- 이 인스턴스는 삭제하지 않는 한 계속 존재

**수동 롤백 방법:**

| 방법               | 설명                             | 주의사항                       |
| ------------------ | -------------------------------- | ------------------------------ |
| 인스턴스 이름 변경 | 이전 Blue의 이름을 원래대로 복원 | Switchover 이후 새 데이터 유실 |
| 새 Blue/Green 배포 | 이전 Blue를 소스로 새 배포 생성  | 시간 소요                      |

**핵심 문제점:**

```
Switchover 후 새 Blue에 쓰인 데이터는 이전 Blue에 없음
→ 롤백 시 Switchover 이후의 데이터 유실
```

**권장 사항:**

1. Switchover 전 스냅샷 생성
2. 이전 Blue 인스턴스 즉시 삭제하지 않기 (검증 기간 확보)
3. 충분한 테스트 후 Switchover 진행
4. 문제 발생 시 빠른 판단 필요 (새 데이터가 쌓이기 전에 결정)

---

## 5. Switchover 후 새 Blue의 데이터가 이전 Blue에 복제되는가?

**복제되지 않습니다.**

Switchover 완료 후 Blue/Green 배포는 **종료**됩니다.

**Switchover 후 상태:**

| 인스턴스                            | 상태                 | 복제         |
| ----------------------------------- | -------------------- | ------------ |
| 새 Blue (`partners-product`)        | 독립 운영            | ❌ 복제 없음 |
| 이전 Blue (`partners-product-old1`) | 독립 인스턴스로 유지 | ❌ 복제 없음 |

**Blue/Green 배포 생명주기:**

```
생성 → Blue에서 Green으로 복제 → Switchover → 배포 종료
                                              ↓
                                    두 인스턴스는 완전히 분리됨
```

**따라서:**

- Switchover 후 이전 Blue는 그 시점의 스냅샷 상태로 고정
- 롤백용으로 보관하려면 직접 유지해야 함
- 더 이상 필요 없으면 수동으로 삭제

이것이 롤백 시 "Switchover 이후 데이터 유실" 문제가 발생하는 이유입니다.
