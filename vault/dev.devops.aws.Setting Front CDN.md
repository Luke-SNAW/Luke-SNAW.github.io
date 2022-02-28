---
id: e27crz1ovxiph9ohvbjedy6
title: Setting Front CDN
desc: ""
updated: 1646030899268
created: 1646021156163
---

# S3 버킷 생성

## 권한 탭

- 객체 소유권→ ACL 활성화됨. 객체 라이터

<details>
  <summary>버킷 정책</summary>

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": [
        "s3:PutObject",
        "s3:PutObjectAcl",
        "s3:GetObject",
        "s3:GetObjectAcl",
        "s3:ListBucket",
        "s3:AbortMultipartUpload"
      ],
      "Resource": ["arn:aws:s3:::YOUR_BUCKET", "arn:aws:s3:::YOUR_BUCKET/*"],
      "Principal": {
        "AWS": "arn:aws:iam::YOUR_ACCOUNT_NUMBER:user/YOUR_USERNAME"
      },
      "Effect": "Allow"
    }
  ]
}
```

</details>

## 속성 탭

정적 웹 호스팅 편집

- 정적 웹 사이트 호스팅: 활성화
- 호스팅 유형: 정적 웹 사이트 호스팅
- 인덱스 문서: index.html

# CloudFront 배포 생성

- origin domain: S3> 속성 탭> 정적 웹 사이트 호스팅> 버킷 웹 사이트 엔드포인트
- SSL Certicicate → Custom SSL → ACM에 만들어져 있는 SSL
- CNAME: domain name
- default root object: index.html

# Route53

## CNAME 생성

- 레코드 이름: site name
- 값: CloudFront의 URL
