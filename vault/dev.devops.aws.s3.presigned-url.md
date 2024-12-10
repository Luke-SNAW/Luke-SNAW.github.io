---
id: jc12ch4ruj1eak2p8fj2m7h
title: Presigned URL
desc: ""
updated: 1733814627238
created: 1733811121555
---

```xml
<Error>
<Code>AccessDenied</Code>
<Message>User: arn:aws:sts::996526550038:assumed-role/~~ is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::~~" because no identity-based policy allows the s3:ListBucket action</Message>
<RequestId>BJWVV83DHW3WVJQ3</RequestId>
<HostId>fefjjk63uF4LvbzOjuyuvG6AghObYjY4v2pXv0sOIVPHAlkJXvmON2Fc4JqVlcrtrgRKhsnVHY4v4XKvMzFKckS/m5nRfAdY</HostId>
</Error>
```

-> Lambda role에 permission 추가

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::~~"
    }
  ]
}
```

presigned URL 다운로드 시 fetch 없이 [file-saver](https://github.com/eligrey/FileSaver.js)의 saveAs쓰면 HEAD로 요청해서 403 에러 발생. CORS에 HEAD 열어줘도 error

> https://github.com/eligrey/FileSaver.js/issues/557#issuecomment-573417689

## S3 setting

### Block all public access on

### Bucket policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "public-read",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::~~/*"
    }
  ]
}
```

### CORS

```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["HEAD", "GET", "POST"],
    "AllowedOrigins": ["http://localhost:3000"],
    "ExposeHeaders": []
  }
]
```
