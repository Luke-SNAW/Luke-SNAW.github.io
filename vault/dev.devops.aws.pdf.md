---
id: isfc3gvb4x5nq2ebm8324ef
title: Pdf
desc: ""
updated: 1752200920002
created: 1752197925254
---

## User

### Permissions policies

#### lambda\_\_pdf-generator

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "lambda:UpdateFunctionCode",
      "Resource": [
        "arn:aws:lambda:*:function:pdf-generator__test",
        "arn:aws:lambda:*:function:pdf-generator"
      ]
    }
  ]
}
```

#### S3\_\_pdf-resources

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::pdf-resources",
        "arn:aws:s3:::pdf-resources--test"
      ]
    },
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:DeleteObject"],
      "Resource": [
        "arn:aws:s3:::pdf-resources/*",
        "arn:aws:s3:::pdf-resources--test/*"
      ]
    }
  ]
}
```

## Roles

### pdf-generator-role-\*

#### list-Bucket-for-presigned-URL

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::*"
    }
  ]
}
```

#### save_PDF

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:PutObjectAcl"],
      "Resource": "arn:aws:s3:::*/*"
    }
  ]
}
```
