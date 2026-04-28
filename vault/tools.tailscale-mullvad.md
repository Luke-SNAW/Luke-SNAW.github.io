---
id: hh6dg4s7v68pa2y78ft2s6g
title: Tailscale + Mullvad Exit Node 세팅 가이드
desc: ""
updated: 1777337287965
created: 1777337261418
---

Tailscale과 Mullvad VPN을 연동하여 프라이버시 보호 인터넷 브라우징 환경을 구축하는 방법을 설명합니다.

---

## 개요

Tailscale은 Mullvad와 파트너십을 맺어 Mullvad의 전 세계 VPN 서버를 Tailscale의 **exit node**로 사용할 수 있게 했습니다. 이를 통해 다음이 가능합니다.

- 집이나 외출 중 인터넷을 안전하고 프라이빗하게 브라우징
- 공용 Wi-Fi에서 도청 방지
- 전 세계 특정 지역을 통한 인터넷 접속
- 비표준 포트 트래픽을 Mullvad 네트워크 엣지를 통해 전달

### Tailscale vs Mullvad — 무엇이 다른가?

| 구분   | Tailscale                               | Mullvad                             |
| ------ | --------------------------------------- | ----------------------------------- |
| 역할   | 기기 간 연결 (개인 사설 인터넷)         | 인터넷 익명 브라우징                |
| 목적   | 내가 소유한 서비스/기기에 안전하게 접근 | 광고주, ISP, 위협 행위자로부터 보호 |
| 암호화 | end-to-end WireGuard 암호화             | WireGuard 기반 트래픽 마스킹        |

두 서비스를 함께 사용하면 **Tailscale의 강력한 암호화 + Mullvad의 익명 브라우징**을 동시에 누릴 수 있습니다.

---

## 요구 사항 및 제한 사항

- **Tailscale v1.48.2 이상** 필요 (현재 베타 기능)
- Mullvad VPN 애드온을 별도로 구매해야 함
- 아래 기능과는 호환되지 않음:
  - 커스텀 DERP 서버
  - Google-synced 그룹을 이용한 ACL 정책
- Windows 클라이언트에서는 전체 Mullvad exit node 목록을 UI에서 볼 수 없음 (CLI 사용 필요)
- Admin console과 tailnet policy file 중 **하나**로만 Mullvad 접근을 관리해야 함

---

## 라이선스 및 요금

- 기본 애드온: **5개 디바이스 슬롯** 포함
- 가격: **디바이스 5개당 월 $5**
- 이용 가능 플랜:
  - Personal Pro / GitHub Community: 월간 또는 연간 구독 가능
  - Personal / Standard / Premium: 월간 구독만 가능
  - Enterprise: 계정 팀에 별도 문의

---

## Step 1. Mullvad 애드온 활성화

1. [Tailscale Admin Console](https://login.tailscale.com/admin/settings/general) → **General** 설정 페이지로 이동
2. **Mullvad VPN** 섹션까지 스크롤
3. **Configure** 버튼 클릭
4. 결제 플로우를 따라 Mullvad 라이선스 구매

> **GitOps 사용자 주의:** tailnet policy file로 관리 중인 경우 결제 플로우가 잠길 수 있습니다. 이 경우 [Billing](https://login.tailscale.com/admin/settings/billing) 페이지 → **Manage add-ons**에서 라이선스를 구매하세요.

---

## Step 2. 디바이스에 Mullvad 접근 권한 부여

두 가지 방법 중 하나를 선택하세요. **혼용은 불가**합니다.

### 방법 A: Admin Console (UI)

1. **General** 설정 → **Mullvad VPN** → **Configure**
2. **Add devices** 클릭
3. Mullvad를 사용할 디바이스 선택 후 저장

> 디바이스 1개당 라이선스 슬롯 1개를 사용합니다. 디바이스를 추가/제거하면 청구 금액이 자동으로 조정됩니다.

### 방법 B: Tailnet Policy File (ACL)

Admin Console → **Access controls** 페이지에서 `nodeAttrs` 섹션을 추가합니다.

**특정 사용자에게 부여:**

```json
"nodeAttrs": [
  {
    "target": ["joe@example.com"],
    "attr": [
      "mullvad"
    ]
  }
]
```

**그룹 단위로 부여 (라이선스 풀 공유):**

```json
"nodeAttrs": [
  {
    "target": ["group:mullvad"],
    "attr": [
      "mullvad"
    ]
  }
]
```

> **라이선스 풀 공유 시 주의사항:**  
> 디바이스가 tailnet에 **접속하는 순간** 라이선스가 선착순으로 할당됩니다 (Mullvad 서버에 연결하는 시점이 아님). 구매한 슬롯이 모두 사용 중이면 이후 디바이스는 Mullvad exit node를 사용할 수 없습니다.

---

## Step 3. Mullvad Exit Node 사용하기

디바이스에 Mullvad 접근 권한이 부여된 후, 각 디바이스에서 개별적으로 exit node를 활성화해야 합니다.  
처음 사용 시 또는 몇 주간 미사용 후 재사용 시 동기화에 최대 **2분** 정도 소요될 수 있습니다.

### Android / iOS

1. 메뉴(⋯) → **Use exit node** 선택
2. 원하는 Mullvad exit node 선택
3. (선택) 로컬 네트워크 접근 허용 시 **Allow LAN access** 체크

### macOS

1. 메뉴바의 Tailscale 아이콘 클릭
2. **Use exit node** → Mullvad 서버 선택

### Windows

Windows UI에서는 전체 목록이 표시되지 않습니다. CLI를 사용하세요.

### Linux (CLI)

```bash
# 사용 가능한 Mullvad exit node 목록 확인
tailscale exit-node list

# exit node 설정
tailscale set --exit-node=<mullvad-exit-node-hostname>

# exit node 해제
tailscale set --exit-node=
```

### Apple TV (tvOS)

설정 앱 → Tailscale → **Use exit node**에서 Mullvad 서버 선택

---

## DNS 설정 (중요)

Tailscale **v1.48.3 이상**은 추가 DNS 설정이 필요 없습니다.

v1.48.1 ~ v1.48.2를 사용 중이라면 아래 중 하나를 설정해야 합니다.

**옵션 1: Allow local network access 활성화**

- exit node 사용 시 **Allow LAN access**를 활성화하면 로컬 DNS를 계속 사용할 수 있습니다.
- 단, DNS 리크가 발생할 수 있습니다.

**옵션 2: 글로벌 네임서버 설정 (권장)**

- Admin Console → DNS 설정에서 Mullvad의 Public DNS를 글로벌 네임서버로 추가
- **Override DNS servers** 활성화
- [mullvad.net/check](https://mullvad.net/en/check)에서 DNS 리크 없음을 확인할 수 있습니다.

---

## Mullvad 사용 해제

### 특정 디바이스 접근 권한 제거 (Admin Console)

1. **General** → **Mullvad VPN** → **Configure**
2. 해당 디바이스 옆 **Remove** → **Save**

### Tailnet Policy File에서 제거

`nodeAttrs`에서 해당 사용자 또는 그룹의 `mullvad` 속성을 제거합니다.

### 애드온 완전 제거

1. **Billing** 페이지 → **Manage add-ons**
2. **Mullvad VPN** → **Remove add-on**

---

## 기존 Mullvad 앱에서 마이그레이션하는 경우

Mullvad 단독 앱을 사용하다가 Tailscale 연동으로 전환하는 경우:

1. Mullvad VPN 앱 실행
2. Mullvad VPN **비활성화**
3. **Block connections without VPN** 설정 **끄기**

이후 Tailscale에서 Mullvad exit node를 정상적으로 사용할 수 있습니다.

---

## Tailnet Lock 사용 시: Mullvad Exit Node 서명

[Tailnet Lock](https://tailscale.com/docs/features/tailnet-lock)을 사용하는 경우 각 Mullvad exit node에 서명이 필요합니다. 서명하는 디바이스에도 유효한 Mullvad 라이선스가 있어야 합니다.

**단일 exit node 서명:**

```bash
# jq 설치 필요

# 1. Mullvad exit node의 NodeKey 확인
tailscale lock status --json | jq '[.FilteredPeers[] | select(.DNSName | contains("mullvad.ts.net")) | {DNSName, NodeKey: .NodeKey}] | sort_by(.DNSName)'

# 2. 서명
tailscale lock sign nodekey <nodekey-of-exit-node>
```

**여러 exit node 자동 서명 (스크립트):**

Linux, macOS, Windows에서 사용 가능한 자동화 스크립트:  
→ [github.com/tailscale-support/mullvad-script](https://github.com/tailscale-support/mullvad-script)

특정 국가 코드(두 글자) 또는 `..`(마침표 두 개)를 입력해 전체 노드를 서명할 수 있습니다.

---

## 프라이버시 및 익명성 참고 사항

| 항목                  | 내용                                                   |
| --------------------- | ------------------------------------------------------ |
| Tailscale이 아는 정보 | 사용자 신원, 어떤 Mullvad 서버에 연결했는지            |
| Mullvad가 아는 정보   | 어떤 기기가 연결됐는지만 (사용자 신원은 전달되지 않음) |
| 트래픽 내용           | WireGuard end-to-end 암호화로 Tailscale도 볼 수 없음   |

완전한 익명성이 필요한 경우 [EFF의 Surveillance Self-Defense 가이드](https://ssd.eff.org/)를 참고하세요.

---

## 관련 링크

- [Tailscale Blog: Mullvad Integration](https://tailscale.com/blog/mullvad-integration)
- [Tailscale Docs: Mullvad Exit Nodes](https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes)
- [Mullvad 서버 목록](https://mullvad.net/en/servers)
- [Mullvad DNS 리크 체크](https://mullvad.net/en/check)
- [Tailscale Admin Console](https://login.tailscale.com/admin/settings/general)
