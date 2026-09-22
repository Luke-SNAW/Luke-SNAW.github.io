---
id: gs5jpkqov1bwlesy2iy7h9a
title: 11 Heynote 리밸런싱 수식
desc: ""
updated: 1790127000000
created: 1790047909188
published: false
---

# fin.portfolio.11 — heynote math 모드 리밸런싱 수식

> [[03 계좌 배치·리밸런싱 운용서|fin.portfolio.03-rebalancing]]의 R-4 규칙을 [heynote](https://github.com/heyman/heynote/) math 모드에서 매월 점검용으로 돌리기 위한 수식 모음이다. **계산 도구이며 규칙 원본이 아니다** — 밴드 폭·목표 비중이 바뀌면 R-4.1을 고친 뒤 이 문서의 `tCache`~`band`/`tol`을 맞춘다[[3.6-변하는-숫자는-한-곳에서만-관리한다|fin.portfolio.00-index#3-분할-기준]]과 같은 원칙).

## HN-1 전제

- 기존에 계좌별 원화·달러 평가액을 합산하는 수식(`rp`, `isa`, `pension`, `irp`, `krwGold`, `total*` 계열)이 이미 있다고 가정한다. USD 금액은 `숫자USD in KRW` 형태로 직접 변환한다 — math 모드가 변수에는 이 변환을 적용하지 못해서다.
- 아래 수식은 그 결과물인 `totalCache`, `totalQQQ`, `totalSchd`, `totalGold`, `total`, 그리고 리츠(O) 평가액을 이어받아 쓴다.

## HN-2 분모 — O를 뺀 4-슬리브 합

R-4.1의 목표 비중(성장주 55 / SCHD 20 / 금 15 / 현금 10)은 4개 슬리브 기준이며 리츠(O)는 이 합에 들어가지 않는다. 기존 `percentCache` 등은 분모로 `total`(O 포함)을 썼기 때문에 네 비중의 합이 100%에 못 미쳤다 — **버그로 보고 분모를 `sleeveTotal`로 교체했다.**

```
oKRW=19633257.141132727
sleeveTotal=total-oKRW

pCache=totalCache/sleeveTotal*100
pQQQ=totalQQQ/sleeveTotal*100
pSchd=totalSchd/sleeveTotal*100
pGold=totalGold/sleeveTotal*100
pCache+pQQQ+pSchd+pGold
```

> O를 포함해 계산하던 기존 방식이 의도한 것이었다면 `sleeveTotal=total`로 되돌린다.
> `totalGold`에는 GDX가 그대로 섞여 있다([[X-1|fin.portfolio.06-excluded#x-1-gdx--제외]] 제외 대상). 금 목표(15%) 대비 실제로는 GDX가 금현물 몫을 대신 채우고 있다는 점을 감안해서 읽는다.

## HN-3 목표·밴드 상수 (R-4.1 원본)

```
tCache=10
tQQQ=55
tSchd=20
tGold=15
band=20
tol=10
```

> **2026-09-23 갱신.** 기준안이 50/25/15/10 → 55/20/15/10으로 바뀌면서 `tQQQ`·`tSchd`만 변경. `tCache`·`tGold`·`band`·`tol`은 불변.

## HN-4 목표 대비 상대 이격 (%)

```
gCache=(pCache/tCache-1)*100
gQQQ=(pQQQ/tQQQ-1)*100
gSchd=(pSchd/tSchd-1)*100
gGold=(pGold/tGold-1)*100
```

## HN-5 밴드 이탈 판정 → 매매 발동 여부

```
trigCache=abs(gCache)>=band
trigQQQ=abs(gQQQ)>=band
trigSchd=abs(gSchd)>=band
trigGold=abs(gGold)>=band
rebalNeeded=trigCache or trigQQQ or trigSchd or trigGold
```

`rebalNeeded=false`면 [[HN-8|#hn-8-월-납입금-라우팅-r-47]]만 보고 끝낸다([[R-4.6|fin.portfolio.03-rebalancing#r-46-밴드-안-자산은-건드리지-말라]] — 밴드 안 자산은 교정 목적으로 건드리지 않는다).

## HN-6 1단계 — halfway-back (R-4.2)

이탈한 자산만 목표의 ±`tol`% 선까지 되돌린다. 결과는 원화 매매액(+매수 / −매도).

```
a0Cache=trigCache ? tCache*(1+sign(gCache)*tol/100)/100*sleeveTotal-totalCache : 0
a0QQQ=trigQQQ ? tQQQ*(1+sign(gQQQ)*tol/100)/100*sleeveTotal-totalQQQ : 0
a0Schd=trigSchd ? tSchd*(1+sign(gSchd)*tol/100)/100*sleeveTotal-totalSchd : 0
a0Gold=trigGold ? tGold*(1+sign(gGold)*tol/100)/100*sleeveTotal-totalGold : 0
net=a0Cache+a0QQQ+a0Schd+a0Gold
```

## HN-7 2단계 — 순액을 밴드 안 자산에 이격 비례로 상쇄

`net`이 0이 아니면(매도 대금이 남거나, 매수에 자금이 더 필요하면) 밴드 안에 있는 자산 중 이격 방향이 반대인 쪽에 이격 크기 비례로 나눈다([[R-4.6|fin.portfolio.03-rebalancing#r-46-밴드-안-자산은-건드리지-말라]] 허용 항목 — "이탈 자산 매도 대금을 밴드 안 자산에 재투자" 등).

```
wCache=trigCache ? 0 : max(0, net<0 ? -gCache : gCache)
wQQQ=trigQQQ ? 0 : max(0, net<0 ? -gQQQ : gQQQ)
wSchd=trigSchd ? 0 : max(0, net<0 ? -gSchd : gSchd)
wGold=trigGold ? 0 : max(0, net<0 ? -gGold : gGold)
wSum=wCache+wQQQ+wSchd+wGold

tradeCache=a0Cache+(wSum>0 ? -net*wCache/wSum : 0)
tradeQQQ=a0QQQ+(wSum>0 ? -net*wQQQ/wSum : 0)
tradeSchd=a0Schd+(wSum>0 ? -net*wSchd/wSum : 0)
tradeGold=a0Gold+(wSum>0 ? -net*wGold/wSum : 0)
tradeCache+tradeQQQ+tradeSchd+tradeGold
```

`tradeCache+tradeQQQ+tradeSchd+tradeGold`는 항상 0에 가까워야 한다(자산군 간 이동일 뿐 총액 불변). 얼마를 어느 자산으로 옮길지 정했으면, **어느 계좌에서 실행할지는 [[R-3|fin.portfolio.03-rebalancing#r-3-매도-우선순위]] 매도 우선순위**(구간 단위 한계세율 순서)를 그대로 따른다 — 이 문서는 그 순서를 계산하지 않는다.

## HN-8 월 납입금 라우팅 (R-4.7)

납입금은 전체 기준 **상대 이격**이 가장 큰(가장 저비중인) 슬리브로 보낸다. 계좌마다 살 수 있는 자산이 다르므로 계좌 제약 안에서 고른다([[R-4.7|fin.portfolio.03-rebalancing#r-47-납입금--무료-리밸런싱]] 계좌별 라우팅 표).

```
irpPay=250000
pensionPay=500000
isaPay=1670000
genPay=880000

irpSafe=irpPay*0.3
irpRisk=irpPay-irpSafe
irpRiskPick=gQQQ<=gSchd ? "IRP 위험분→성장주(QQQ)" : "IRP 위험분→SCHD"
pensionPick=min(gQQQ,gSchd,gCache)==gQQQ ? "연금저축→QQQ" : (min(gQQQ,gSchd,gCache)==gSchd ? "연금저축→SCHD" : "연금저축→초단기채")
isaPick=gQQQ<=gSchd ? "ISA→QQQ" : "ISA→SCHD"
genPick=min(gGold,gCache,gQQQ)==gGold ? "일반→금현물" : (min(gGold,gCache,gQQQ)==gCache ? "일반→현금" : "일반→QQQ/VGT")
```

> IRP는 위험자산 몫(70%) 안에서만 QQQ/SCHD 중 고르고, 30%는 항상 안전자산으로 고정한다([[R-2.4|fin.portfolio.03-rebalancing#r-24-irp-위험자산-70-한도--계좌-단위-하드-제약]]).
> 일반 계좌는 금·현금·QQQ·VGT 네 자산 중에서 고른다 — 여기서는 세 후보(`gGold`, `gCache`, `gQQQ`)로 단순화했으니, VGT까지 따로 볼 거면 `gVGT`를 추가해 `min`에 넣는다.
> 문자열 결과(`"연금저축→QQQ"` 등)가 heynote에서 안 보이면 `pensionPick` 대신 `gQQQ`, `gSchd`, `gCache`의 대소 비교(`gQQQ<gSchd`, `gQQQ<gCache` 등 boolean)로 직접 확인한다.

## HN-9 IRP 70% 한도 확인 (R-2.4)

```
irpRiskPct=(irpQQQ+irpSchd)/irpTotal*100
irpRiskPct<=70
```

## HN-10 알려진 한계

- 계좌 간 실제 이동 경로(R-3 매도 우선순위, 세율 구간 소진)는 계산하지 않는다 — 얼마를 어느 방향으로 옮길지까지만 나온다.
- 연 1회 계좌별 기준 비율 재산정([[R-2.3|fin.portfolio.03-rebalancing#r-23-계좌-운용-규칙]] 규칙 5)은 별도 절차이며 이 수식에 없다.
- `totalGold`의 GDX 혼입, `total`의 O 포함 여부는 원본 평가액 계산 쪽(계좌 합산 수식) 문제이므로 이 문서가 아니라 그 수식에서 고친다.

## HN-11 변경 이력

- 2026-09-23 [[A-1|fin.portfolio.02-allocation#a-1-기준안]] 기준안 변경(50/25/15/10 → 55/20/15/10) 반영 — HN-3의 `tQQQ`·`tSchd`만 수정
- 2026-09-22 최초 작성 — R-4 규칙을 heynote math 수식으로 구현, 분모의 O 포함 오류 수정
