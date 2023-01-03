---
id: 4g275ke7i8296gvpkb1n1fc
title: Lightsail + Bitnami
desc: ""
updated: 1672718123542
created: 1648599678702
---

# 인증서

## 설치

> https://aws.amazon.com/ko/premiumsupport/knowledge-center/linux-lightsail-ssl-bitnami/  
> https://docs.bitnami.com/aws/faq/administration/generate-configure-certificate-letsencrypt/

```shell
sudo /opt/bitnami/bncert-tool
```

## bncert-tool 또는 Lego 도구를 사용하여 설치한 Let's Encrypt 인증서 갱신하기

> https://aws.amazon.com/ko/premiumsupport/knowledge-center/lightsail-bitnami-renew-ssl-certificate/

```shell
sudo /opt/bitnami/ctlscript.sh stop
sudo /opt/bitnami/letsencrypt/lego --tls --email="EMAIL-ADDRESS" --domains="DOMAIN" --path="/opt/bitnami/letsencrypt" renew --days 90
sudo /opt/bitnami/ctlscript.sh start
```

## [Let's Encrypt - Expiration Emails](https://letsencrypt.org/docs/expiration-emails/)

However, you can change the email address on your account, which effectively re-subscribes you. Many common email services treat `yourname+1@example.com` the same as `yourname@example.com`. So if you update your email address to `yourname+1@example.com`, you can start getting expiry mail again. With Certbot, use:

```shell
certbot update_account --email yourname+1@example.com
```

## 새 email 등록

```shell
sudo /opt/bitnami/letsencrypt/lego --tls --email="new+1@genoplan.com" --domains="DOMAIN" --path="/opt/bitnami/letsencrypt" --http run
```

### 등록 과정 중에 apache가 이미 실행 중이라 Error 발생하면

443 port를 써서 인증 시도했지만 이미 사용 중이라 실패 했다는 메시지 떴음

```shell
sudo /opt/bitnami/ctlscript.sh stop apache
# 등록 후
sudo /opt/bitnami/ctlscript.sh start apache
```
