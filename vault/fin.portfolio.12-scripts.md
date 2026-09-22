---
id: 7pqz3m0k9x4vt2adws61bfe
title: 12 Scripts
desc: ""
updated: 1790126000000
created: 1790100000000
published: false
---

# 12 시뮬레이션 스크립트

> [[09 백테스트|fin.portfolio.09-backtest]]의 수치를 재생성하는 코드. 결론은 담지 않는다 — 결론은 09에 있다.
> 상위: [[00 인덱스|fin.portfolio.00-index]] · 번호 접두어 **S**

> ⚠️ **재실행 필요 (2026-09-23).** [[A-1|fin.portfolio.02-allocation#a-1-기준안]]의 기준안이 50/25/15/10 → 55/20/15/10으로 바뀌었다. 아래 스크립트의 `BASE`(및 관련 목표 비중) 상수는 아직 옛 50/25 값이다. 새 기준안 결과를 얻으려면 상수를 55/20/15/10으로 바꾸고 재실행한 뒤 [[09 백테스트|fin.portfolio.09-backtest]]의 해당 절을 갱신해야 한다.

## S-1 수록 범위

| 스크립트               | 재생성하는 절 | 상태                                                                              |
| ---------------------- | ------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ------------------------- |
| `b11_regime_switch.py` | [[B-11        | fin.portfolio.09-backtest#b-11-하락폭-기반-전환-규칙-검증-2026-09-22]] 전체       | 보존됨                                                                |
| (없음)                 | [[B-3         | fin.portfolio.09-backtest#b-3-기준안-결과-성장주50--schd25--금15--현금10]]~[[B-10 | fin.portfolio.09-backtest#b-10-schd-비중-축소-시뮬레이션-2026-09-22]] | 세션에만 존재, 보존 안 됨 |

`b11_regime_switch.py`는 B-11뿐 아니라 **기준안·공격적안의 기준선도 같은 엔진으로 다시 계산**하므로, 배분을 바꿔 돌려보는 출발점으로도 쓸 수 있다. `BASE`·`A65` 상수와 `simulate()`의 `lo`·`exit_rule` 인자만 고치면 된다.

## S-2 실행

```
pip install scipy
python3 b11_regime_switch.py fin.portfolio.10-raw-data.md
```

입력은 [[10 원본 데이터|fin.portfolio.10-raw-data]]의 마크다운 원문 그대로다. 별도 CSV 변환이 필요 없다.

**두 가지 파싱 규칙이 [[B-1.1|fin.portfolio.09-backtest#b-11-재현-검증-2026-09-22]]의 일치 조건이다.** 어느 하나라도 어긋나면 벤치마크가 맞지 않는다.

- 같은 달에 여러 행이 있으면 **day가 큰 행**(최신 관측치)을 쓴다 — 2026-09는 월봉 Sep 1이 아니라 Sep 17 행
- SCHD 상장 전 구간 접합은 **가격이 아니라 수익률**로 한다. VIG 가격에서 SCHD 가격으로 그냥 넘어가면 접합 월에 −54%의 가짜 낙폭이 생긴다

## S-3 b11_regime_switch.py

```python
#!/usr/bin/env python3
"""
B-11 재현 스크립트 — 하락폭 기반 전환 규칙 검증
=================================================
fin.portfolio.09-backtest B-11의 모든 수치를 재생성한다.

전제
  - 입력: fin.portfolio.10-raw-data.md (Yahoo Finance 월간 표를 붙여넣은 원본)
  - 방법론: B-2와 동일 (자산 프록시, 달러 단일 통화, 밴드 상대 ±20% / halfway-back ±10%,
            월 1회 점검, 납입금을 최저비중 슬리브에 전액 투입)
  - 구간: 2006-09 ~ 2026-09 (240개월), 초기 1000 + 월 10
  - 2026-09 가격은 월봉이 아니라 마지막 관측치(Sep 17, 2026) 행 — B-1.1 일치 조건

사용법
  python3 b11_regime_switch.py /path/to/fin.portfolio.10-raw-data.md

의존성: scipy (brentq). 없으면 이분법으로 대체 가능.
"""
import re, sys, statistics as st
from scipy.optimize import brentq

# ---------------------------------------------------------------- 1. 데이터 파싱
MON = {m: i + 1 for i, m in enumerate(
    ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'])}
ROW = re.compile(
    r'^\|\s*([A-Z][a-z]{2})\s+(\d{1,2}),\s*(\d{4})\s*\|'
    r'\s*([\d,\.]+)\s*\|\s*([\d,\.]+)\s*\|\s*([\d,\.]+)\s*\|\s*([\d,\.]+)\s*\|\s*([\d,\.]+)\s*\|')

def load(path):
    txt = open(path, encoding='utf-8').read()
    secs, cur = {}, None
    for line in txt.split('\n'):
        m = re.match(r'^## ([A-Z]+)\s*$', line)
        if m:
            cur = m.group(1); secs[cur] = []
        elif cur is not None:
            secs[cur].append(line)
    out = {}
    for tk, lines in secs.items():
        d = {}
        for line in lines:
            m = ROW.match(line)
            if not m:
                continue
            y, mo, day = int(m.group(3)), MON[m.group(1)], int(m.group(2))
            adj = float(m.group(8).replace(',', ''))
            k = f'{y}-{mo:02d}'
            # 같은 달에 여러 행이 있으면 최신 관측치(큰 day)를 쓴다 → B-1.1 일치 조건
            if k not in d or day > d[k][0]:
                d[k] = (day, adj)
        out[tk] = {k: v[1] for k, v in sorted(d.items())}
    return out

def months(a, b):
    out = []; y, m = map(int, a.split('-')); ey, em = map(int, b.split('-'))
    while (y, m) <= (ey, em):
        out.append(f'{y}-{m:02d}'); m += 1
        if m == 13: y, m = y + 1, 1
    return out

# ---------------------------------------------------------------- 2. 수익률
def build_returns(P, MS):
    def schd_ret(k0, k1):
        # SCHD 상장 전(2011-10 이전)은 VIG. 접합은 '가격'이 아니라 '수익률'로 한다.
        if k0 in P['SCHD'] and k1 in P['SCHD']:
            return P['SCHD'][k1] / P['SCHD'][k0]
        return P['VIG'][k1] / P['VIG'][k0]
    R = {}
    for i in range(1, len(MS)):
        k0, k1 = MS[i-1], MS[i]
        R[k1] = [P['QQQ'][k1] / P['QQQ'][k0],     # 성장주
                 schd_ret(k0, k1),                 # SCHD 대응
                 P['GLD'][k1] / P['GLD'][k0],      # 금
                 1.02 ** (1/12)]                   # 현금 연 2%
    return R

# ---------------------------------------------------------------- 3. R-4 규칙
BAND, TOL = 0.20, 0.10

def rebalance(v, tgt):
    """밴드 발동 시 이격 최대 자산을 tolerance 선까지 되돌리고,
       초과분을 이격 방향이 반대인 자산에 이격 크기 비례로 배분."""
    v = list(v); fired = False
    for _ in range(50):
        tot = sum(v); w = [x / tot for x in v]
        dev = [w[i] / tgt[i] - 1 for i in range(4)]
        out = [i for i in range(4) if abs(dev[i]) > BAND + 1e-12]
        if not out:
            break
        fired = True
        i = max(out, key=lambda j: abs(dev[j]))
        target_w = tgt[i] * (1 + (TOL if dev[i] > 0 else -TOL))
        move = (target_w - w[i]) * tot
        opp = [j for j in range(4) if j != i and (dev[j] > 0) != (dev[i] > 0) and abs(dev[j]) > 1e-12]
        if not opp:
            opp = [j for j in range(4) if j != i]
        s = sum(abs(dev[j]) for j in opp)
        v[i] += move
        for j in opp:
            v[j] -= move * abs(dev[j]) / s
    return v, fired

def contribute(v, tgt, amt):
    tot = sum(v)
    dev = [(v[i] / tot) / tgt[i] - 1 for i in range(4)]
    v[min(range(4), key=lambda j: dev[j])] += amt
    return v

# ---------------------------------------------------------------- 4. 시뮬레이터
BASE = (0.50, 0.25, 0.15, 0.10)
AGG55 = (0.55, 0.25, 0.15, 0.05)
A65 = (0.65, 0.15, 0.15, 0.05)

def simulate(P, R, MS, mode, agg=A65, lo=-0.20, exit_rule='half', start=1000.0, c=10.0):
    """mode: 'static_base' | 'static_agg' | 'switch'
       exit_rule: 'half' (하락폭 절반 회복) | float (고정 낙폭선, 예: -0.10)"""
    cur = agg if mode == 'static_agg' else BASE
    v = [start * t for t in cur]
    flows = [(-1, -start)]
    hist, log = [], []
    peakq = P['QQQ'][MS[0]]; depth = 0.0; agg_m = 0; fires = 0
    for i, k in enumerate(MS):
        if i > 0:
            r = R[k]; v = [v[j] * r[j] for j in range(4)]
        peakq = max(peakq, P['QQQ'][k])
        dd = P['QQQ'][k] / peakq - 1
        if mode == 'switch':
            if cur is BASE and dd <= lo:
                cur = agg; depth = dd
                tot = sum(v); v = [tot * t for t in cur]; log.append((k, 'AGG', dd, None))
            elif cur is agg:
                depth = min(depth, dd)
                back = depth / 2 if exit_rule == 'half' else exit_rule
                if dd >= back:
                    cur = BASE
                    tot = sum(v); v = [tot * t for t in cur]; log.append((k, 'BASE', dd, depth))
        if cur is not BASE:
            agg_m += 1
        if i > 0:
            v = contribute(v, cur, c); flows.append((i, -c))
        v, f = rebalance(v, cur); fires += f
        hist.append((k, sum(v), list(v), 'A' if cur is not BASE else 'B'))
    flows.append((len(MS) - 1, sum(v)))
    return dict(hist=hist, flows=flows, log=log, agg_months=agg_m, fires=fires)

def xirr(flows):
    return brentq(lambda r: sum(cf * (1 + r) ** (-t / 12) for t, cf in flows), -0.9, 2.0)

def mdd(hist, a=None, b=None):
    s = [(k, t) for k, t, _, _ in hist if (a is None or a <= k <= b)]
    pk, w = -1e18, 0.0
    for _, t in s:
        pk = max(pk, t); w = min(w, t / pk - 1)
    return w

# ---------------------------------------------------------------- 5. 실행
def main(path):
    P = load(path)
    MS = months('2006-09', '2026-09')
    R = build_returns(P, MS)

    def line(name, res):
        h = res['hist']
        return (name, h[-1][1], xirr(res['flows']) * 100, mdd(h) * 100,
                mdd(h, '2021-06', '2024-06') * 100, mdd(h, '2019-12', '2020-12') * 100,
                res['agg_months'], len(res['log']), res['fires'])

    runs = [
        ('기준안 50/25/15/10', simulate(P, R, MS, 'static_base')),
        ('공격적안 55/25/15/5', simulate(P, R, MS, 'static_agg', agg=AGG55)),
        ('상시 65/15/15/5', simulate(P, R, MS, 'static_agg', agg=A65)),
        ('전환안 −20% / 절반회복', simulate(P, R, MS, 'switch')),
        ('전환안 −20% / −10% 고정', simulate(P, R, MS, 'switch', exit_rule=-0.10)),
    ]
    print('== B-11.1 전체 20년 ==')
    print(f"{'':24s}{'최종':>9s}{'XIRR':>8s}{'MDD':>8s}{'2022형':>8s}{'2020형':>8s}{'공격':>6s}{'전환':>5s}{'밴드':>5s}")
    for n, res in runs:
        _, f, x, m, m22, m20, am, sw, fi = line(n, res)
        print(f'{n:24s}{f:9,.0f}{x:7.2f}%{m:7.1f}%{m22:7.1f}%{m20:7.1f}%{am:5d}월{sw:5d}{fi:5d}')

    sw = runs[3][1]
    print('\n== B-11.2 전환 이력 (절반회복) ==')
    for k, s, dd, dep in sw['log']:
        extra = f' (최저 {dep*100:.1f}%)' if dep is not None else ''
        print(f'  {k}  {"공격 진입" if s=="AGG" else "기준 복귀"}  낙폭 {dd*100:.1f}%{extra}')

    print('\n== B-11.3 상태별 구간 기여 분해 ==')
    # 월 k의 수익률은 직전 월의 상태에서 발생
    state = {h[0]: h[3] for h in sw['hist']}
    lab = {MS[i]: state[MS[i-1]] for i in range(1, len(MS))}
    segs = []
    for k in MS[1:]:
        if not segs or segs[-1][0] != lab[k]:
            segs.append([lab[k], k, k])
        else:
            segs[-1][2] = k
    def wret(k, w): return sum(w[j] * R[k][j] for j in range(4))
    gain = loss = 1.0
    print(f"{'':5s}{'구간':22s}{'기준안':>9s}{'65안':>9s}{'상대':>9s}{'개월':>5s}")
    for stt, a, b in segs:
        ks = [k for k in MS if a <= k <= b]
        rb = ra = 1.0
        for k in ks:
            rb *= wret(k, BASE); ra *= wret(k, A65)
        rel = rb / ra - 1
        print(f'{"방어" if stt=="B" else "공격":5s}{a}~{b:11s}{(rb-1)*100:8.1f}%{(ra-1)*100:8.1f}%{rel*100:+8.1f}%{len(ks):5d}')
        if stt == 'B':
            if rel > 0: gain *= 1 + rel
            else: loss *= 1 + rel
    print(f'  방어 상태 중 이득 누적 {(gain-1)*100:+.1f}% / 손해 누적 {(loss-1)*100:+.1f}% / 순 {(gain*loss-1)*100:+.1f}%')

    print('\n== B-11.4 진입·복귀 임계 민감도 ==')
    print(f"{'진입':>6s}{'복귀':>12s}{'최종':>10s}{'XIRR':>8s}{'MDD':>8s}{'전환':>5s}{'공격%':>7s}")
    for lo in (-0.15, -0.20, -0.25, -0.30):
        for ex, nm in (('half', '절반회복'), (-0.10, '−10% 고정'), (-0.05, '−5% 고정')):
            r = simulate(P, R, MS, 'switch', lo=lo, exit_rule=ex)
            print(f'{lo*100:5.0f}%{nm:>12s}{r["hist"][-1][1]:10,.0f}'
                  f'{xirr(r["flows"])*100:7.2f}%{mdd(r["hist"])*100:7.1f}%'
                  f'{len(r["log"]):5d}{r["agg_months"]/len(MS)*100:6.0f}%')

    print('\n== B-11.5 10년 롤링 (121개 윈도우) ==')
    res = {}
    for nm, kw in (('기준안', dict(mode='static_base')),
                   ('상시65', dict(mode='static_agg', agg=A65)),
                   ('전환안', dict(mode='switch'))):
        xs, ms_ = [], []
        for s in range(0, len(MS) - 120):
            w = MS[s:s+121]
            r = simulate(P, R, w, **kw)
            xs.append(xirr(r['flows']) * 100); ms_.append(mdd(r['hist']) * 100)
        res[nm] = (xs, ms_)
        print(f'{nm:8s} XIRR 중앙 {st.median(xs):6.2f}%  최악 {min(xs):6.2f}%  최선 {max(xs):6.2f}%'
              f'  MDD 중앙 {st.median(ms_):6.1f}%  최악 {min(ms_):6.1f}%')
    a, b = res['전환안'][0], res['상시65'][0]
    print(f'  전환안이 상시65를 이긴 윈도우 {sum(x>y for x,y in zip(a,b))}/{len(a)}')
    a2, b2 = res['전환안'][0], res['기준안'][0]
    print(f'  전환안이 기준안을 이긴 윈도우 {sum(x>y for x,y in zip(a2,b2))}/{len(a2)}')

    print('\n== B-11.6 1999-03~2026-09 QQQ 전체 기간 상태 경로 (가격만) ==')
    q = P['QQQ']; pk = 0; cur = 'B'; depth = 0
    for k in sorted(q):
        pk = max(pk, q[k]); dd = q[k] / pk - 1
        if cur == 'B' and dd <= -0.20:
            print(f'  {k} 공격 진입 {dd*100:.1f}%'); cur, depth = 'A', dd
        elif cur == 'A':
            depth = min(depth, dd)
            if dd >= depth / 2:
                print(f'  {k} 기준 복귀 {dd*100:.1f}% (최저 {depth*100:.1f}%)'); cur = 'B'
    print(f'  최종 상태: {"공격" if cur=="A" else "기준"}')
    for a in ('1999-03', '2006-09'):
        pk = 0; below = tot = 0
        for k in sorted(q):
            if k < a: continue
            pk = max(pk, q[k]); tot += 1
            below += (q[k] / pk - 1 <= -0.20)
        print(f'  {a}~ 고점대비 −20% 이하 개월 {below}/{tot} ({below/tot*100:.0f}%)')

if __name__ == '__main__':
    main(sys.argv[1] if len(sys.argv) > 1 else 'fin.portfolio.10-raw-data.md')
```
