---
id: b024gim88gcwxj5gml74ngl
title: Macbook Pro External Monitor Gpuswitch Fix
desc: ""
updated: 1781581763314
created: 1781581758833
---

# MacBook Pro 외부 모니터 인식 문제 해결 정리

> 환경: MacBook Pro 16" (2019, Intel UHD 630 + AMD Radeon Pro 5300M 듀얼 GPU)
> macOS 15.x / 빌드 24E263

---

## 1. 증상

- 절전모드(lock screen 후 sleep)에서 복귀하니 외부 키보드가 인식 안 됨
- USB kext 관련 터미널 명령어 실행 후 재부팅
- **재부팅 후부터 USB-C 허브(Belkin)에 HDMI로 연결된 외부 모니터 2개가 모두 인식 안 됨**
- 같은 허브에 연결된 마우스 등 USB 장치는 정상 동작
- 맥북 자체 화면은 정상

## 2. 핵심 단서

- **안전 모드(Safe Mode)에서는 외부 모니터가 출력됨**
- 일반 모드 + 안전 모드의 결정적 차이 → **그래픽 가속 / GPU 사용 방식**
- 안전 모드는 외장(AMD) GPU를 끄고 통합(Intel) GPU만 사용
- 즉, 자동 GPU 전환이 깨져서 외부 디스플레이를 담당하는 **AMD GPU로 전환이 안 되던 상태**

## 3. 시도한 방법 (효과 없었던 것들)

| 시도                               | 결과                        |
| ---------------------------------- | --------------------------- |
| USB 재연결 / 포트 변경             | ❌                          |
| 허브 전원 재투입                   | ❌                          |
| `killall WindowServer`             | ❌                          |
| `windowserver.plist` 삭제          | ❌                          |
| NVRAM 리셋 (Cmd+Opt+P+R)           | ❌                          |
| kext 캐시 재빌드 (`kmutil`)        | ❌ (KDK 없어 실패)          |
| 안전 모드 부팅 후 로그인           | ❌ (일반 모드 복귀 시 재발) |
| Karabiner / 보안 익스텐션 비활성화 | ❌                          |
| macOS 15.7.7 업그레이드            | ❌                          |
| 복구 모드(Cmd+R) macOS 재설치      | ❌                          |
| 다른 USB-C 포트 연결               | ❌                          |

## 4. 실제 해결 방법 ✅

GPU 전환 설정(`gpuswitch`)이 꼬여 있던 것이 원인.

```bash
# AMD(외장) GPU 강제 고정 → 즉시 외부 모니터 출력됨 (재부팅 불필요)
sudo pmset -a gpuswitch 1
```

이후 자동 전환(`2`)으로 되돌려도 정상 출력 유지됨 (값을 명시적으로 다시 써주면서 설정이 초기화된 것으로 추정).

```bash
sudo pmset -a gpuswitch 2   # 자동 전환으로 복구, 정상 동작 확인
```

> 참고: 그동안 시도했던 USB 관련 명령어들은 사실 이 문제와 무관했음.
> 재발 시 응급처치는 `gpuswitch 1`, 평소엔 `2`로 사용.

---

## 5. pmset 명령어 설명

`pmset` = **power management settings**. macOS 전원 관리 설정을 제어하는 명령어.

### 기본 문법

```bash
pmset [범위 플래그] [설정] [값]
```

### 범위 플래그

| 플래그 | 적용 범위                              |
| ------ | -------------------------------------- |
| `-a`   | 모든 전원 환경 (배터리 + 어댑터 + UPS) |
| `-b`   | 배터리(battery) 사용 시만              |
| `-c`   | 전원 어댑터(charger/AC) 연결 시만      |
| `-u`   | UPS 사용 시만                          |

예시:

```bash
sudo pmset -b displaysleep 5    # 배터리일 때만 5분 후 화면 끔
sudo pmset -c displaysleep 30   # 충전 중일 때만 30분 후 화면 끔
sudo pmset -a gpuswitch 1       # 전원 상태 무관하게 항상 AMD 고정
```

### 자주 쓰는 설정값

| 설정            | 의미                                              |
| --------------- | ------------------------------------------------- |
| `displaysleep`  | 화면 꺼지는 시간 (분)                             |
| `sleep`         | 시스템 절전 진입 시간 (분)                        |
| `disksleep`     | 하드디스크 절전 시간 (분)                         |
| `gpuswitch`     | GPU 전환 (`0`=통합/Intel, `1`=외장/AMD, `2`=자동) |
| `hibernatemode` | 최대 절전 모드 방식                               |
| `powernap`      | Power Nap 켜기/끄기 (0/1)                         |
| `womp`          | Wake on Network 접근                              |
| `standby`       | 스탠바이 모드                                     |

### 현재 설정 확인

```bash
pmset -g            # 현재 활성 전원 설정 보기
pmset -g custom     # 전원 환경별 전체 설정 보기
pmset -g batt       # 배터리 상태/잔량 보기
pmset -g assertions # 절전을 막고 있는 프로세스 확인
```

> `-g assertions`는 "왜 맥이 잠을 안 자지?" 싶을 때
> 어떤 앱이 절전을 막고 있는지 보여줘서 유용함.

### 주의점

- 변경 시 보통 `sudo` 권한 필요
- 설정은 **영구적** → 재부팅해도 유지됨 (잘못 설정하면 계속 적용)
- 기본값 복구는 각 설정을 수동으로 다시 지정해야 함

---

## 6. 교훈

- 증상(USB 키보드)과 실제 원인(GPU 전환)이 무관할 수 있음
- **안전 모드에서 정상 = 그래픽 가속/GPU 경로 의심** 신호
- 듀얼 GPU 맥북(2016~2019 Intel 모델)에서 외부 디스플레이 문제는
  `gpuswitch` 설정을 우선 점검할 것
