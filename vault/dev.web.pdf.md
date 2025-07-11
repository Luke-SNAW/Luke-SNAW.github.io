---
id: zwm4anrm660qx8djckh2ne5
title: PDF
desc: ""
updated: 1752191925216
created: 1733811446364
---

## Page footer 자동으로 생성

지원 되지 않는 듯. 수동으로 테이블 사이즈 조절해서 loop 돌려야..
(Puppeteer에 footer template이 있는 거 같은데... 시도는 안해봄)

> [I believe the correct answer is that HTML 5 and CSS3 have no support for printing page header and footers in print media.](https://stackoverflow.com/a/7197225)

## [How to deal with page breaks when printing a large HTML table](https://stackoverflow.com/a/1763683/26960115)

## PDF 암호화

Puppeteer에선 pdf 암호화를 지원하지 않기 때문에 외부 library를 사용해야 함

> https://github.com/puppeteer/puppeteer/issues/6120

https://github.com/Sparticuz/node-qpdf2

> https://stackoverflow.com/a/77189654

## chromium launch options

참고

> https://github.com/alixaxel/chrome-aws-lambda/blob/1395ee60ad1625d08306a4aad8b7b851b73a9a83/source/index.js#L84-L122

```js
 /**
   * Returns a list of recommended additional Chromium flags.
   */
  static get args() {
    const result = [
      '--autoplay-policy=user-gesture-required',
      '--disable-background-networking',
      '--disable-background-timer-throttling',
      '--disable-backgrounding-occluded-windows',
      '--disable-breakpad',
      '--disable-client-side-phishing-detection',
      '--disable-component-update',
      '--disable-default-apps',
      '--disable-dev-shm-usage',
      '--disable-domain-reliability',
      '--disable-extensions',
      '--disable-features=AudioServiceOutOfProcess',
      '--disable-hang-monitor',
      '--disable-ipc-flooding-protection',
      '--disable-notifications',
      '--disable-offer-store-unmasked-wallet-cards',
      '--disable-popup-blocking',
      '--disable-print-preview',
      '--disable-prompt-on-repost',
      '--disable-renderer-backgrounding',
      '--disable-setuid-sandbox',
      '--disable-speech-api',
      '--disable-sync',
      '--disk-cache-size=33554432',
      '--hide-scrollbars',
      '--ignore-gpu-blacklist',
      '--metrics-recording-only',
      '--mute-audio',
      '--no-default-browser-check',
      '--no-first-run',
      '--no-pings',
      '--no-sandbox',
      '--no-zygote',
      '--password-store=basic',
      '--use-gl=swiftshader',
      '--use-mock-keychain',
    ];

    if (this.headless === true) {
      result.push('--single-process');
    } else {
      result.push('--start-maximized');
    }

    return result;
  }
```
