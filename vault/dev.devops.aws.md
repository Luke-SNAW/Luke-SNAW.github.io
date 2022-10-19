---
id: 7mujc4bw6yz1nfbf03gmqc8
title: Aws
desc: ""
updated: 1666146598769
created: 1646005847772
---

## IAM

### IAM에 필요한 기본 권한

- iam:ChangePassword - 최초 로그인 후 암호변환 (필수 아닐 수 있음. 권한 없을 때 실패 로그로 권한 요청 → 권한 받고 실패 → 특수문자 넣어 성공했기 때문)
- **[IAM: IAM 사용자가 MFA 디바이스를 스스로 관리하도록 허용](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/reference_policies_examples_iam_mfa-selfmanage.html)**
- iam:GetLoginProfile, iam:UpdateLoginProfile - 계정 사용자가 콘솔 비밀번호 리셋을 스스로 할 수 있도록
