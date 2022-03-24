---
id: 4g275ke7i8296gvpkb1n1fc
title: Lightsail
desc: ""
updated: 1648599734035
created: 1648599678702
---

# 인증서

## 설치

> https://aws.amazon.com/ko/premiumsupport/knowledge-center/linux-lightsail-ssl-bitnami/  
> https://docs.bitnami.com/aws/faq/administration/generate-configure-certificate-letsencrypt/

```bash
sudo /opt/bitnami/bncert-tool
```

## bncert-tool 또는 Lego 도구를 사용하여 설치한 Let's Encrypt 인증서 갱신하기

> https://aws.amazon.com/ko/premiumsupport/knowledge-center/lightsail-bitnami-renew-ssl-certificate/

```bash
sudo /opt/bitnami/ctlscript.sh stop
sudo /opt/bitnami/letsencrypt/lego --tls --email="EMAIL-ADDRESS" --domains="DOMAIN" --path="/opt/bitnami/letsencrypt" renew --days 90
sudo /opt/bitnami/ctlscript.sh start
```
