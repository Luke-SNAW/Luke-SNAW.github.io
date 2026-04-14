---
id: keq5k3pcw4htf9c31okrido
title: Lenovo
desc: ""
updated: 1775785997954
created: 1775785801940
---

## 1. Superfish 악성코드 (2014-2015) ⚠️ 가장 심각

### 개요

레노버가 2014년 하반기부터 2015년 초까지 "Superfish"라는 애드웨어를 프리인스톨하여 판매했습니다.

**관련 링크:**

- [Wikipedia - Superfish](https://en.wikipedia.org/wiki/Superfish)
- [The Hacker News - Lenovo Superfish Malware](https://thehackernews.com/search/label/Lenovo%20Backdoor%20Malware)

### 문제점

#### 암호화 연결 침해

- Superfish는 HTTPS 암호화 연결을 가로채고 동일한 개인키를 가진 자체 서명 인증서를 설치하여 중간자(Man-in-the-Middle) 공격을 가능하게 했습니다.
- 보안 전문가들은 이를 "역사상 가장 악성인 애드웨어"라고 표현했습니다.

#### 민감한 정보 탈취 가능

- 이 소프트웨어는 사용자의 다음 정보에 접근할 수 있었습니다:
  - 로그인 자격증명
  - 사회보장번호
  - 의료정보
  - 금융정보
  - 결제 정보

#### 레노버의 부실한 대응

- 처음에는 "보안 문제를 입증할 증거를 찾지 못했다"고 주장
- 언론 보도가 증가하자 겨우 인정
- 처음 제공한 삭제 방법은 취약점을 남겨두었고, 다시 언론에 지적되자 "제거 도구"를 공개

### 결과

**법적 처벌:**

- 8.3백만 달러의 집단소송 합의금
- 350만 달러의 FTC(연방거래위원회) 벌금

**관련 링크:**

- [FTC 공식 성명 - Lenovo Settlement](https://www.ftc.gov/news-events/news/press-releases/2017/09/lenovo-settles-ftc-charges-it-harmed-consumers-preinstalled-software-its-laptops-compromised-online)
- [Tom's Hardware - Lenovo Settlement](https://www.tomshardware.com/news/lenovo-settlement-superfish-scandal-progress,38657.html)

### 기술적 심각성

Superfish 취약점의 설계는 매우 무책임했습니다:

- 모든 영향받은 기기에 동일한 루트 인증서 설치
- HTTPS 트래픽 중간자 공격 가능
- 인증서 개인키가 약한 비밀번호("komodia")로 암호화됨

> "모든 레노버 사용자에게 동일한 집키를 주고 초인종 아래에 숨긴 것과 같다" - Hacker News 사용자의 평가

---

## 2. Lenovo Service Engine (LSE) 백도어 (2015)

### 개요

2015년 9월, 고급형 ThinkPad, ThinkCenter, ThinkStation까지도 악성코드가 프리인스톨되어 있음이 발각되었습니다.

**관련 링크:**

- [The Hacker News - Lenovo Rootkit](https://thehackernews.com/2015/08/lenovo-rootkit-malware.html)
- [Tech Worm - BIOS Level Backdoor](https://www.techworm.net/2015/08/lenovo-pcs-and-laptops-seem-to-have-a-bios-level-backdoor.html)

### 기술적 특징

#### 펌웨어 수준의 침투

- 마더보드 펌웨어에 숨겨진 "Lenovo Service Engine"이라는 코드
- Windows 설치 시 부팅 전에 자동으로 소프트웨어를 다운로드하여 설치
- Windows 파일을 덮어씀

#### 완전 포맷 후에도 재설치됨

- 시스템을 완전히 포맷해도 WPBT(Windows Platform Binary Table) 기능을 통해 소프트웨어가 자동 재설치됨
- 사용자가 OS를 깨끗하게 재설치해도 무의미

#### 설치된 악성 소프트웨어

- **OneKey Optimizer (OKO)**: 번들로 설치되는 소프트웨어
- **LenovoCheck.exe, LenovoUpdate.exe**: 삭제해도 재부팅 시 재생성됨

#### 보안 결함

- ForceUpdate 파라미터 및 SSL 미적용
- 중간자(Man-in-the-Middle) 공격에 취약
- 원격 코드 실행 가능

### 영향받은 기기

Windows 7, 8, 8.1이 설치된 다음 시리즈:

- Lenovo Flex
- Lenovo Yoga
- 기타 2014-2015년형 모델

**관련 링크:**

- [Make Use Of - Security Failings](https://www.makeuseof.com/tag/security-failings-demonstrate-avoid-lenovo/)

---

## 3. Lenovo Customer Feedback Program

### 문제점

- 사용자의 일상 사용 데이터를 수집
- Adobe가 소유한 온라인 마케팅 회사 Omniture로 전송
- Superfish와 Lenovo Service Engine 이후 발견되어 더욱 신뢰도 추락

### 유일한 긍정적 측면

- 다른 사례와 달리 언인스톨 가능 (완전히 제거 불가능하지 않음)

---

## 4. 펌웨어 수준의 취약점 (2021년 발견)

### 개요

2021년 ESET 보안 업체에 의해 발견된 심각한 펌웨어 취약점

**관련 링크:**

- [Dark Reading - Lenovo Firmware Vulnerabilities](https://www.darkreading.com/threat-intelligence/millions-of-lenovo-laptops-contain-firmware-level-vulnerabilities)
- [Heimdal Security - Lenovo UEFI Vulnerabilities](https://heimdalsecurity.com/blog/millions-of-laptops-impacted-by-lenovo-uefi-firmware-vulnerabilities)

### 기술적 세부사항

#### CVE-2021-3971, CVE-2021-3972

- UEFI 드라이버가 제조 과정에서만 사용되도록 설계됨
- 실수로 본체 BIOS 이미지에 포함된 채 출시
- 100개 이상의 소비자 랩톱 모델 영향

#### CVE-2021-3970

- 시스템 오류 감지 및 로깅 함수의 메모리 손상 버그
- System Management RAM(SMRAM) 임의 읽기/쓰기 가능

### 위협 수준

- 공격자가 부팅 중 악성코드를 주입 가능
- 운영체제 재설치 후에도 악성코드 잔존 가능
- 하드 드라이브 교체 후에도 제거 불가능
- BIOS 보호 기능을 비활성화 가능
- UEFI Secure Boot 우회 가능

### 비유: LoJax 말웨어

러시아 Sednit 그룹이 배포한 "LoJax" 펌웨어 수준 루트킷과 유사한 방식으로 악용될 수 있음

---

## 5. 하드웨어 수준의 백도어 의혹 (미확인)

### Bloomberg 보도

미국 군 조사관들이 키스트로크를 기록하고 데이터를 전송하는 백도어 칩이 레노버 마더보드에서 발견되었다는 보도

- 레노버는 이를 부인함
- 완전히 검증되지 않음

**관련 링크:**

- [Wikipedia - Lenovo](https://en.wikipedia.org/wiki/Lenovo)

---

## 6. 정부/군 차원의 제재

레노버의 이러한 보안 문제로 인해:

- 여러 국가의 **정보 기관(Intelligence Services)**이 제품 사용 금지
- **국방 관련 네트워크(Defense Services)** 공급 금지
- 보안이 중요한 기관에서는 신뢰할 수 없는 업체로 분류

**관련 링크:**

- [Legion Cyberworks - Lenovo Security Failures](https://legioncyber.com/lenovos-security-failures-and-hidden-risks/)

---

## 시간순 요약

| 시기                    | 사건                             | 심각도         |
| ----------------------- | -------------------------------- | -------------- |
| 2014년 9월 - 2015년 1월 | Superfish 악성코드 프리인스톨    | 🔴 매우 높음   |
| 2015년 5월              | Lenovo Service Engine 발견       | 🔴 매우 높음   |
| 2015년 8월              | LSE 펌웨어 백도어 적발           | 🔴 매우 높음   |
| 2015년                  | Lenovo Customer Feedback Program | 🟠 높음        |
| 2017년                  | FTC 합의 및 벌금                 | 💰 8.3M + 3.5M |
| 2021년                  | UEFI 펌웨어 취약점 발견          | 🔴 높음        |

---

## 전문가 평가

### Slate 칼럼니스트 David Auerbach의 평가

> "레노버는 기술 회사들이 사용자를 상품으로 취급할 때, 가장 기본적인 네트워크 보안도 선택사항이 될 수 있다는 것을 우리에게 가르쳐주었다."

### 보안 커뮤니티의 반응

- 레노버 기기를 볼 때 마다 의심스러운 인증서를 먼저 확인하는 조건반사 형성
- 비즈니스 스쿨에서 위기관리 실패 사례로 다루어짐

---

## 결론

### ✓ 당신의 우려가 정당한 이유

1. **반복된 위반**: 한두 번이 아니라 여러 차례 적발됨
2. **기술적 심각성**: 단순 버그가 아니라 의도적인 설계로 보임
3. **부실한 대응**: 처음엔 부인하고 나중에 인정하는 방식
4. **계속되는 문제**: 2015년 문제를 해결했는데 2021년 또 다른 취약점 발견

### ⚠️ 신뢰도 평가

**신뢰하기 어려운 이유:**

- 과거 동의 없이 백도어 성 소프트웨어 설치
- 펌웨어 수준까지 침투
- 투명성 부족 (처음엔 부인)
- 반복된 문제

**현재 상황 (2026년 기준):**

- 최근 보도된 심각한 사건은 없음
- 그러나 과거 행적으로 인한 신뢰도 회복 필요
- 보안이 중요한 경우: 다른 브랜드 권장

---

## 추가 자료

| 출처            | 링크                                                                                                                                                            | 내용                      |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| Wikipedia       | https://en.wikipedia.org/wiki/Superfish                                                                                                                         | Superfish 상세 정보       |
| Wikipedia       | https://en.wikipedia.org/wiki/Lenovo                                                                                                                            | 레노버 전반 정보          |
| FTC             | https://www.ftc.gov/news-events/news/press-releases/2017/09/lenovo-settles-ftc-charges-it-harmed-consumers-preinstalled-software-its-laptops-compromised-online | 공식 합의 성명            |
| The Hacker News | https://thehackernews.com/search/label/Lenovo%20Backdoor%20Malware                                                                                              | 레노버 백도어 관련 기사들 |
| CISA            | https://www.cisa.gov/news-events/alerts/2015/02/20/lenovo-superfish-adware-vulnerable-https-spoofing                                                            | 미 정부 보안 경고         |

---

_마지막 업데이트: 2026년 4월_
