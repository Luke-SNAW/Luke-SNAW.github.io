---
id: GR5x8HnNFEN6fU2UBSEIK
title: Hardware
desc: ""
updated: 1782809240529
created: 1645404426038
published: false
---

## Sound

WH-1000XM3 노캔 기능을 잘 때 소음차단으로 잘 써먹고 있다. 별 기대 안했는데

### WH-1000XM3 Pairing

- When you pair a 2nd or subsequent device (the headset has pairing information for other devices), press and hold the button for about 7 seconds.
- Select [WH-1000XM3] displayed on the screen of the Bluetooth device for pairing. If passkey (\*) input is required on the display of the computer, input “0000.”

## Phone

### NFC

교통카드 사용. 3번 잘 됐는데 4번째 부터 계속 `한 장의 카드만 ...` 에러.
그 사이에 구글 play 결제에 들어가서 둘러본거 같은데, 쓰지도 않는 google pay가 nfc 선택지에 있는게 계속 거슬림. -> google play 들어가기만 했는데 또 중복 에러. 설마 그냥 주기적으로 이러는 건 아니겠지?
자체 제공하는 복구 메뉴를 써도 안되고...

-> 그냥 NFC 태깅 위치가 잘못됨. 제조사에는 NFC 센서 위치를 안 알려주고, 이마트 안내포스터에 폰 중앙이라 해서 중앙으로 했던건데, 상단이었음

## 안경

### 컴퓨터 전용 도수

> 40~70cm 거리(모니터 거리)에 초점이 맞도록 설계.
> 원거리 도수보다 도수를 약하게 처방 (보통 근시 기준 -0.75 ~ -1.50D 정도 낮춤)
> 모양체근이 거의 쉰 상태에서 모니터가 선명하게 보임

추천 받아 다초점으로 렌즈 맞추고, 일반 초점은 -1 단계, 밑 영역 초점은 -3 단계로 추천 받았으나, 밑 영역 초점을 -2 단계로 해달라고 요청.
모니터 거리만 생각하면 -2 단계 단초점으로 충분하겠지만, 사무실 용이라 회의 참가할 때 생각하면 -1 단계가 필요할 수도 있기에 이 선택은 만족스러움. 회의 참가하고 업데이트 필요.
모니터와 목 각도를 생각하면 다초점 영역이 중간에 걸리는거 같은데... 다초점은 실패인가?
다만 안경테 콧등이 높아서인지 고개 돌릴 때 울렁거림. 그 동안은 일반 렌즈와 비구면 렌즈 차이를 별로 못느꼈는데... 콧등 사이 렌즈 없는 영역이 시야에 들어와서 그럴지도 모르겠다. - 2026-05

안경테가 오른쪽 귓등을 조여 아파서 안경원에 가서 조정 가능하냐고 요청하니 안경테가 일자가 아니라 안으로 휘어있다고 함. 받을 때 부터 이랬는데?
기계를 통해 열로 데우더니 일자로 펴줌 - 2026-05-22

## Keyboard

split keyboard 오른쪽 RP2040이 고장나서 집에서 키보드를 가져와 쓰며 느낀점.

- split keyboard 쪽이 가벼워 안정감이 상대적으로 적고 손에 긴장도가 올라가는 느낌
- row/column stagger는 둘다 적응가능하지만, 새끼손가락을 생각하면 column stagger가 쎈 쪽이 좋음. 약한 stagger는 별 차이 없다.
- 새끼손가락 키압이 강하면 불편
- 키 폼팩터는 텐키와 펑션키 줄 없는 쪽을 선호. Alice 배열 선호.
- layer용 엄지 mod 키 수는 3개보다 2키가 낫다. 3번째는 잘 안쓰고 가끔 오타냄.

### Silakka54

2025-12 에 구매

요즘 회사 macbook에서 usb hub 접속이 불안정하게 끊겼다 연결될 때 가끔 키보드 인식이 안 됨.
재부팅하면 될 때도 있고 안될 때도 있음. 다른 쪽으로 usb 연결하면 인식은 되지만 firmware 설치가 안되 다른 쪽 인식이 안됨. 회사 보안프로그램 때문에 usb file copy가 막혀있어 firmware 설치 못함.

어쩌다 된 오늘 인식 성공 방법;

1. 연결 끊고 boot 키 누른 상태에서 usb 연결 후 boot 키 떼고 난 후 usb drive로 인식 확인 (firmware 설치 준비)
2. 케이블 떼고 재연결

하니 됐음

- [layout backup](./assets/silakka54-2026-05_layout.vil)

#### 사망

오른쪽 모듈 사망으로 판단.

```
# 오른쪽 BOOT 누른 채 USB 연결 → 마운트 확인
ls /Volumes/RPI-RP2
# 마운트 확인됐으면 바로
picotool info -f
INDEX.HTM*    INFO_UF2.TXT*
libc++abi: terminating due to uncaught exception of type picoboot::connection_error: std::exception
fish: Job 1, 'picotool info -f' terminated by signal SIGABRT (Abort)16 Jun

Claude responded: 이걸로 결론이 났어요.이걸로 결론이 났어요.
RPI-RP2는 마운트되는데(부트로더 ROM은 정상), picotool은 connection_error로 죽고, 펌웨어 플래시 쓰기는 Device not configured로 실패해요. 세 증거가 모두 한 방향을 가리킵니다.
진단: 오른쪽 모듈 하드웨어 손상
구체적으로는 둘 중 하나예요:

QSPI 플래시 칩 손상 — 부트로더는 MCU 내장 ROM으로 도니까 마운트되지만, 펌웨어를 저장하는 외장 플래시 칩에 쓰기가 안 됨. nuke(RAM 실행)는 되고 펌웨어(플래시 쓰기)는 안 되는 게 이 증거예요.
USB D+/D- 데이터 라인 납땜 불량 — 짧은 통신(마운트, nuke)은 버티지만 지속적인 대용량 쓰기에서 끊김. picotool 통신 실패가 이 증거예요.

절전모드 후 갑자기, 그리고 전에도 "가끔" 그랬다는 패턴을 보면 2번(USB 포트 또는 TRRS 잭 주변 납땜 크랙) 쪽 가능성이 좀 더 높아 보여요. 접촉 불량은 원래 간헐적으로 나타나다가 점점 악화되거든요.
현실적인 선택지
소프트웨어로 할 수 있는 건 끝났어요. 이제:
A. 셀프 수리 (납땜 가능하면)

오른쪽 USB-C 포트 재납땜 (특히 데이터 핀) — 가장 흔한 원인이라 먼저 점검
안 되면 플래시 칩 교체 (QSPI W25Q 계열, SMD 작업)
컨트롤러가 소켓형 RP2040 보드(예: 제로보드)면 보드만 교체가 제일 쉬움

B. A/S / 교체

구매처나 제작자에게 오른쪽 PCB 또는 모듈 교체 요청
silakka54는 자작 키보드라 보통 판매처가 PCB 단위 판매를 해요

C. 임시 사용

왼쪽은 정상이니, 부품 구하는 동안은 왼쪽만이라도 사용
```
