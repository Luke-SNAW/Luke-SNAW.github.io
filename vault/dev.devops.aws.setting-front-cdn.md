---
id: e27crz1ovxiph9ohvbjedy6
title: Setting Front CDN
desc: ""
updated: 1666317771349
created: 1646021156163
---

## S3 버킷 생성

### 권한 탭

- 객체 소유권→ ACL 활성화됨. 객체 라이터
- 퍼블릭 액세스 차단(버킷 설정) - 모두 비활성

<details>
  <summary>버킷 정책</summary>

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Resource": ["arn:aws:s3:::YOUR_BUCKET"],
      "Principal": {
        "AWS": "arn:aws:iam::YOUR_ACCOUNT_NUMBER:user/YOUR_USERNAME"
      },
      "Effect": "Allow"
    },
    {
      "Action": [
        "s3:PutObject",
        "s3:PutObjectAcl",
        "s3:GetObject",
        "s3:GetObjectAcl",
        "s3:AbortMultipartUpload"
      ],
      "Resource": ["arn:aws:s3:::YOUR_BUCKET/*"],
      "Principal": {
        "AWS": "arn:aws:iam::YOUR_ACCOUNT_NUMBER:user/YOUR_USERNAME"
      },
      "Effect": "Allow"
    }
  ]
}
```

</details>

### 속성 탭

정적 웹 호스팅 편집

- 정적 웹 사이트 호스팅: 활성화
- 호스팅 유형: 정적 웹 사이트 호스팅
- 인덱스 문서: index.html

## CloudFront 배포 생성

- origin domain: S3> 속성 탭> 정적 웹 사이트 호스팅> 버킷 웹 사이트 엔드포인트
- SSL Certicicate → Custom SSL → ACM에 만들어져 있는 SSL
- CNAME: domain name
- default root object: index.html

## Route53

### CNAME 생성

- 레코드 이름: site name
- 값: CloudFront의 URL

## Cache

> https://medium.com/wantedjobs/cloudfront-cloudfront-functions-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-next-js-%EB%B2%88%EB%93%A4%ED%8C%8C%EC%9D%BC-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%84%9C%EB%B9%99%ED%95%98%EA%B8%B0-9ccc0541e406

### CloudFront Functions

```js
function handler(event) {
  var response = event.response;
  var headers = response.headers;

  // CORS header
  if (!headers["access-control-allow-origin"]) {
    headers["access-control-allow-origin"] = { value: "*" };
    console.log("Access-Control-Allow-Origin was missing, adding it now.");
  }
  // cache-control
  headers["cache-control"] = { value: "public,max-age=31536000,immutable;" };
  return response;
}
```

함수연결 - 뷰어 응답
