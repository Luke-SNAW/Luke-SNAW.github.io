---
id: 6z4jaa5ybm77l59xxuihl49
title: YAML 보안 취약점 정리
desc: ""
updated: 1773645336385
created: 1773644804482
---

## 개요

YAML은 "사람이 읽기 편한" 포맷을 목표로 설계되었지만, 그 과정에서 추가된 수많은 암묵적 규칙과 기능들이 오히려 **보안 취약점의 원인**이 되었다. 복잡한 DSL일수록 파서 구현이 어렵고 잘못 구성된 파서는 심각한 보안 문제를 야기한다.

---

## 주요 취약점

### 1. 역직렬화(Deserialization) 공격 — 원격 코드 실행(RCE)

YAML의 가장 치명적인 취약점. 많은 YAML 파서가 기본적으로 **임의 객체를 역직렬화**할 수 있어, 공격자가 YAML 파일을 통해 서버에서 코드를 실행시킬 수 있다.

**공격 예시 (PyYAML 기본 설정)**

```yaml
# 파싱 시 os.system("rm -rf /") 실행됨
!!python/object/apply:os.system
- "rm -rf /"
```

**Ruby (Psych 파서)**

```yaml
---
!ruby/object:Gem::Installer
i: !ruby/object:Gem::Package::TarReader
  io: !ruby/object:Net::BufferedIO
    io: !ruby/object:Gem::Package::TarReader::Entry
      read: 0
      header: "aa"
```

**원인**: `yaml.load()` 함수가 타입 태그(`!!`)를 통해 임의 Python/Ruby 객체를 인스턴스화함

**대응책**:

- Python: `yaml.load()` ❌ → `yaml.safe_load()` ✅
- Ruby: `YAML.safe_load()` 사용
- Java (SnakeYAML): `new SafeConstructor()` 사용

**관련 CVE 및 참고자료**:

- [CVE-2017-18342](https://www.cvedetails.com/cve/CVE-2017-18342/) — PyYAML 최초 주요 보안 권고 (RCE)
- [CVE-2022-1471](https://www.huntress.com/threat-library/vulnerabilities/cve-2022-1471) — SnakeYAML (Java) Critical RCE, Kubernetes·Spring Boot 등 광범위 영향
- [CVE-2022-32224](https://rubysec.com/advisories/CVE-2022-32224/) — Ruby on Rails Active Record YAML 역직렬화 RCE
- [GitHub Security Lab: Swagger YAML Parser (CVE-2017-1000207, CVE-2017-1000208)](https://securitylab.github.com/research/swagger-yaml-parser-vulnerability/) — SnakeYAML 악용 사례 심층 분석
- [From YAML to RCE: The PyYAML Deserialization Story](https://0d-amr.medium.com/from-yaml-to-rce-the-pyyaml-deserialization-story-4a7d1dfe4f43) — PyYAML CVE 계보 및 우회 기법 정리
- [YAML Deserialization Attack in Python (Exploit-DB)](https://www.exploit-db.com/docs/47655) — PyYAML 역직렬화 공격 기술 문서
- [Panic!! At the YAML — GreyNoise Labs](https://www.labs.greynoise.io/grimoire/2024-01-03-snakeyaml-deserialization/) — SnakeYAML 취약점 실습 분석
- [Ruby Security Field Guide: YAML](https://trailofbits.github.io/rubysec/yaml/index.html) — Ruby YAML 취약점 상세 가이드

---

### 2. 앨리어스 폭탄 (Billion Laughs / YAML Bomb)

XML의 "Billion Laughs" 공격과 동일한 원리. 앵커(`&`)와 앨리어스(`*`)를 중첩시켜 **지수적으로 메모리를 소모**시키는 DoS 공격.

**공격 예시**

```yaml
a: &a ["lol", "lol", "lol", "lol", "lol", "lol", "lol", "lol", "lol"]
b: &b [*a, *a, *a, *a, *a, *a, *a, *a, *a]
c: &c [*b, *b, *b, *b, *b, *b, *b, *b, *b]
d: &d [*c, *c, *c, *c, *c, *c, *c, *c, *c]
e: &e [*d, *d, *d, *d, *d, *d, *d, *d, *d]
# 파싱 시 메모리 수 GB 소모 → 서비스 다운
```

**원인**: 앨리어스 확장 시 깊이/크기 제한이 없는 파서

**대응책**:

- 앨리어스 확장 깊이 및 노드 수 제한 설정
- 외부 입력 YAML에서 앨리어스 기능 비활성화

**관련 CVE 및 참고자료**:

- [CVE-2019-11253](https://github.com/kubernetes/kubernetes/issues/83253) — Kubernetes API Server YAML 파싱 DoS (Billion Laughs). kube-apiserver가 매니페스트 크기 제한 없이 파싱해 발생
- [CVE-2023-47163](https://www.miggo.io/vulnerability-database/cve/CVE-2023-47163) — Remarshal YAML 파서 앨리어스 무한 확장 DoS
- [Wikipedia: Billion Laughs Attack](https://en.wikipedia.org/wiki/Billion_laughs_attack) — 공격 원리 및 YAML bomb 예시 포함
- [Palo Alto Networks: Kubernetes Billion Laughs 취약점 분석](https://www.paloaltonetworks.com/blog/2019/10/cloud-kubernetes-vulnerabilities/) — CVE-2019-11253 심층 분석
- [Laughter in the Wild: DoS Vulnerabilities in YAML Libraries (논문)](https://www.researchgate.net/publication/333505459_Laughter_in_the_Wild_A_Study_into_DoS_Vulnerabilities_in_YAML_Libraries) — 10개 언어 14개 YAML 라이브러리 DoS 취약점 체계적 연구

---

### 3. 타입 강제 변환 (Type Coercion) — 예측 불가능한 파싱

YAML은 값의 타입을 자동으로 추론하는데, 이 과정에서 **의도치 않은 값 변환**이 발생한다.

**문제 예시**

```yaml
# 개발자가 문자열을 의도했지만...
port: 080          # 8진수로 해석 → 64 (YAML 1.1)
enabled: yes       # true로 해석
api_key: 1234e5    # 부동소수점으로 해석 → 123400.0
version: 1.0       # float으로 해석 → 문자열 "1.0" 비교 실패
country_code: NO   # false로 해석 ← "Norway Problem"
country_code: ON   # true로 해석
date: 2024-01-15   # Date 객체로 해석
```

**Norway Problem**: 국가 코드 `NO`(노르웨이)가 `false`로 파싱되는 실제 버그. ISO 국가 코드 목록을 YAML로 관리할 때 발생.

**대응책**:

- 모든 값에 명시적 따옴표 사용: `country_code: "NO"`
- YAML 1.2 스펙을 지원하는 파서 사용 (타입 추론 규칙이 개선됨)

**관련 참고자료**:

- [The Norway Problem — StrictYAML 공식 문서](https://hitchdev.com/strictyaml/why/implicit-typing-removed/) — `NO`가 `false`로 파싱되는 실제 사례 및 원인 분석
- [The YAML document from hell](https://ruudvanasseldonk.com/2023/01/11/the-yaml-document-from-hell) — YAML 타입 강제 변환의 다양한 함정 총정리 (필독)
- [YAML? That's Norway problem (lab174.com)](https://lab174.com/blog/202601-yaml-norway/) — 2026년 1월 기준 주요 라이브러리 대부분이 여전히 YAML 1.1을 사용한다는 최신 분석
- [YAML: The Norway Problem — Bram.us](https://www.bram.us/2022/01/11/yaml-the-norway-problem/) — 개요 및 bool 타입 파싱 regex 설명

---

### 4. XXE / SSRF (파서 설정 오류)

일부 YAML 파서는 내부적으로 XML을 사용하거나, 외부 엔티티·리소스 로딩을 지원하는 경우가 있다.

**공격 시나리오**

```yaml
# 특정 파서에서 외부 파일 참조 가능
data: !include file:///etc/passwd

# SSRF — 내부 네트워크 요청 유발
config: !include http://169.254.169.254/latest/meta-data/
```

**대응책**:

- 외부 리소스 로딩 기능 비활성화
- 파서의 `safe` 모드 사용

**관련 CVE 및 참고자료**:

- [Jenkins Security Advisory 2020-04-16](https://www.jenkins.io/security/advisory/2020-04-16/) — Yaml Axis Plugin, AWS SAM Plugin, OpenShift Pipeline Plugin 등 YAML 파서 설정 오류로 인한 다수 RCE CVE 포함
- [Jenkins Security Advisory 2020-03-25](https://www.jenkins.io/security/advisory/2020-03-25/) — Pipeline AWS Steps Plugin(CVE-2020-2168), Azure Container Service Plugin(CVE-2020-2169) 등 임의 타입 인스턴스화 취약점
- [PortSwigger Web Security Academy: XXE to SSRF](https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-perform-ssrf) — XXE→SSRF 공격 실습 (EC2 메타데이터 탈취)

---

### 5. 파서 구현체별 동작 불일치 (Parser Differential Attack)

YAML 스펙이 복잡하여 각 언어의 파서마다 **동일한 입력에 다른 결과**를 반환할 수 있다. 이를 이용해 앞단 검증을 우회할 수 있다.

**공격 시나리오**

```
[입력 YAML] → [검증 파서 A: 무해한 값으로 해석] → 통과
                     ↓
              [실행 파서 B: 악성 값으로 해석] → 피해 발생
```

**실제 사례**: WAF나 보안 검증 레이어가 Ruby YAML로 파싱하고, 실제 앱은 Python YAML로 파싱할 때 결과 불일치 발생.

**대응책**:

- 파이프라인 내 모든 단계에서 동일한 파서 사용
- 검증과 실행에 서로 다른 파서 사용 금지

**관련 참고자료**:

- [Trail of Bits: Unexpected Security Footguns in Go's Parsers](https://blog.trailofbits.com/2025/06/17/unexpected-security-footguns-in-gos-parsers/) — Go의 JSON/XML/YAML 파서 차이를 이용한 인증 우회 공격 (CVE-2020-16250 포함) 심층 분석. JSON·XML·YAML 세 파서가 서로 다른 값을 반환하는 polyglot 구성 방법 설명
- [Swagger YAML Parser (CVE-2017-1000207, CVE-2017-1000208)](https://securitylab.github.com/research/swagger-yaml-parser-vulnerability/) — 서로 다른 언어·버전의 SnakeYAML 파서가 동일 입력을 다르게 해석하여 발생한 RCE 사례 (파서 불일치의 실제 보안 영향을 보여주는 사례)

---

### 6. 템플릿 인젝션과의 결합

YAML은 Jinja2, Go 템플릿 등의 템플릿 언어와 자주 혼용된다. 이 경우 **YAML 파싱 전에 템플릿이 먼저 평가**되므로, 템플릿 인젝션과 결합된 공격이 가능하다.

**공격 예시 (Ansible/Helm)**

```yaml
# 사용자 입력값이 템플릿에 삽입되는 경우
name: { { user_input } }

# 공격자 입력: {{ ''.__class__.__mro__[2].__subclasses__() }}
```

**대응책**:

- 사용자 입력을 템플릿 변수에 직접 삽입 금지
- 입력값 이스케이프 처리
- 템플릿 샌드박스 모드 사용

**관련 CVE 및 참고자료**:

- [CVE-2021-38305](https://jfrog.com/blog/23andmes-yamale-python-code-injection-and-properly-sanitizing-eval/) — Yamale YAML 스키마 검증기 코드 인젝션 (JFrog 분석). `eval()` 잘못 사용으로 스키마 파일을 통해 임의 Python 코드 실행 가능
- [Finding YAML Deserialization with Snyk Code](https://snyk.io/blog/finding-yaml-injection-with-snyk-code/) — geokit-rails 등 실제 오픈소스 프로젝트의 YAML 인젝션 사례

---

## 취약점 요약표

| 취약점         | 심각도      | 영향                   | 주요 대응책        |
| -------------- | ----------- | ---------------------- | ------------------ |
| 역직렬화 (RCE) | 🔴 Critical | 원격 코드 실행         | `safe_load()` 사용 |
| 앨리어스 폭탄  | 🟠 High     | 서비스 중단 (DoS)      | 앨리어스 깊이 제한 |
| 타입 강제 변환 | 🟡 Medium   | 로직 우회, 인증 오류   | 명시적 따옴표 사용 |
| XXE / SSRF     | 🟠 High     | 내부 정보 유출         | 외부 로딩 비활성화 |
| 파서 불일치    | 🟡 Medium   | 검증 우회              | 단일 파서 통일     |
| 템플릿 인젝션  | 🔴 Critical | 코드 실행, 데이터 탈취 | 입력값 이스케이프  |

---

## 근본 원인

YAML의 보안 문제는 기능 과잉(feature bloat)에서 비롯된다:

1. **암묵적 타입 변환** — 개발자의 의도와 다르게 동작
2. **Turing-complete에 가까운 복잡성** — 앵커/앨리어스, 태그, 다양한 스칼라 타입
3. **파서 구현 난이도** — 스펙이 복잡해 파서마다 동작이 달라짐
4. **기본 설정의 위험성** — 안전한 옵션이 기본이 아닌 경우가 많음

---

## 대안 검토

| 용도         | 권장 대안                                    |
| ------------ | -------------------------------------------- |
| 설정 파일    | **TOML** — 명시적 타입, 단순한 스펙          |
| 데이터 교환  | **JSON** — 타입 강제 변환 없음               |
| 복잡한 설정  | **HCL** (Terraform), **Dhall** — 타입 안전성 |
| 간단한 키-값 | **.env** / **INI**                           |

---

_작성일: 2026-03-16_ with Sonnet 4.6
