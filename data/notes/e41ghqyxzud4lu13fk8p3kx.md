
**브루트포스 공격 성공 확률에 대한 산업 표준**

일반적으로 인증 시스템에서 브루트포스 공격의 **성공 확률을 0.1% 미만 (즉, 0.001 이하)**으로 유지하는 것이 산업에서 "안전"하다고 간주됩니다. 이는 **NIST SP 800-63B 가이드라인**과 **OWASP 권장사항**에서 유도되는 수준으로, 온라인 공격에서 로그인 시도 횟수를 제한(rate limiting)하여 달성합니다.[^1][^2]

**주요 기준과 이유**:

- **NIST 지침**: 온라인 브루트포스 공격을 막기 위해 시도 횟수를 제한하라고 명시. 예를 들어, 분당 100회 시도로 제한하면 10자리 문자열(예: 62^10 ≈ 8.4조 조합)에서 성공 확률이 100/8.4조 ≈ **10^{-12} 수준(0.0000000001%)**으로 떨어짐. 짧은 문자열(예: 16자리 문화상품권 코드)이라도 rate limit으로 **1% 미만 확률**을 목표로 함.[^1][^2]
- **OWASP 및 업계 실무**: 브루트포스 성공률을 **1% 이하**로 억제하는 rate limiting/CAPTCHA/MFA를 권장. Microsoft 분석에 따르면 MFA가 99.9% 공격을 막지만, 단일 문자열 인증(Mullvad 계정 코드나 상품권처럼)은 rate limit 없인 취약. 성공률 **0.01~0.1%**조차 고위험으로 봄.[^4][^8]
- **위험 허용 수준(risk tolerance)**: 산업별 차이 있음.
  - **금융/고민감 산업**: **0.01% 미만** (엄격한 규제 준수).[^11][^12]
  - **문화상품권 등 저가/대량 발행 서비스**: **1% 이하** 허용되기도 함. 무한 시도 방지를 위해 계정 잠금이나 지연을 두지만, "특정 확률 이하"는 **0.1~1%**로 운영(사용자 편의성 trade-off). 그러나 이는 보안상 권장되지 않음.[^3][^6]
- **실제 취약점**: 제공된 사례처럼 rate limit 미비 시 성공률 80% 이상(웹 앱 공격 중 브루트포스 비중). 분산 봇넷 공격에도 **분당 수천 회** 제한으로 확률을 0.001%대로 낮춤.[^7][^10]

**mullvad/문화상품권 사례**: 이런 단일 문자열 인증은 편의성을 위해 설계됐으나, 브루트포스로 뚫리기 쉽습니다. 안전 기준은 **0.1% 미만**이지만, 실제 운영에서 1%까지 허용되는 경우가 있어 보안 논란. 더 나은 대안은 CAPTCHA나 시간 지연 추가.[^5][^9]

이 수치는 조직의 **위험 허용도(risk tolerance)**에 따라 조정되며, 절대적이지 않습니다. 정확한 %는 위협 모델(공격자 컴퓨팅 파워)에 따라 다름.[^3][^6]

[^1]: [NIST Special Publication 800-63B](https://pages.nist.gov/800-63-4/sp800-63b.html) (22%)

[^2]: [Strength of Passwords](https://pages.nist.gov/800-63-4/sp800-63b/passwords/) (14%)

[^3]: [Creating Cyber Risk Tolerance Statements: Turn Strategy ...](https://www.fairinstitute.org/blog/creating-cyber-risk-tolerance-statements) (13%)

[^4]: [Authentication - OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) (11%)

[^5]: [Lab: Broken brute-force protection, multiple credentials per request](https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request) (9%)

[^6]: [Balancing Identity Management and Risk Tolerance](https://www.sysdig.com/blog/balancing-identity-management-and-risk-tolerance) (8%)

[^7]: [What is a Brute Force Attack?](https://www.upguard.com/blog/brute-force-attack) (7%)

[^8]: [Blocking Brute Force Attacks](https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks) (6%)

[^9]: [CWE-308: Use of Single-factor Authentication (4.19.1)](https://cwe.mitre.org/data/definitions/308.html) (4%)

[^10]: [Why Rate Limiting Fails for ATO Defense | Memcyco](https://www.memcyco.com/brute-force-attack-prevention/) (3%)

[^11]: [Selecting the Perfect Authentication Method for Your Business](https://blog.pulsarsecurity.com/selecting-the-perfect-authentication-method-for-your-business) (2%)

[^12]: [Mastering MFA Requirements: Compliance, Risks, and Best Practices](https://www.rsa.com/resources/blog/multi-factor-authentication/mastering-mfa-requirements-compliance-risks-and-best-practices/) (1%)
