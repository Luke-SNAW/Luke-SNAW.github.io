---
id: 6645fjtiqxtko03nuccgjj2
title: "What I struggled 🧗‍♂️/📣 brag In"
desc: ""
updated: 1672126471971
created: 1669264809793
---

## Week 52, 2022

### [Tailwind - Dynamic class names](https://tailwindcss.com/docs/content-configuration#dynamic-class-names)

```js
class = `bg-${ zero ? pageColor : baseColor}` // not work
class = zero ? `bg-${pageColor}` : `bg-${baseColor}` // not work
```

## Week 51, 2022

### SPA framework - S3 - CloudFront 배포 시 404 error 처리

없는 URI로 접근 시 403 error가 뜬다. [아마도 해당 url path를 cloudFront에서 인식하지 못해서 S3로 요청이 가고 public이 아니니 permission denied 에러](https://dexlee.tistory.com/189#:~:text=%ED%95%B4%EB%8B%B9%20url%20path%EB%A5%BC%20cloudFront%EC%97%90%EC%84%9C%20%EC%9D%B8%EC%8B%9D%ED%95%98%EC%A7%80%20%EB%AA%BB%ED%95%B4%EC%84%9C%20S3%EB%A1%9C%20%EC%9A%94%EC%B2%AD%EC%9D%B4%20%EA%B0%84%EB%8B%A4.%20public%EC%9D%B4%20%EC%95%84%EB%8B%88%EB%8B%88%20%EB%8B%B9%EC%97%B0%ED%9E%88%20permission%20denied%20%EC%97%90%EB%9F%AC%20%EB%B0%9C%EC%83%9D.)
![](assets/images/what-i-struggle-in/s3-cloudfront-404-error.webp)

cloudfront에서 403 error를 SPA framework index.html로 처리하도록 해주면 framework에서 404 처리해 줌
![](assets/images/what-i-struggle-in/s3-cloudfront-404-custom-setting.webp)

## Week 50, 2022

### tailwind css

새 nuxt3 project에 tailwind 도입.
그 동안 제작자 소개글에서 motivation과 결과가 모순되는 걸 봐서 꺼렸는데, code colocation으로 인한 DX, 속도 향상 때문에 써보기로 함.

## Week 49, 2022

### Nuxt3 UI Framework

.com에 쓰인 buefy UI framework는 .co.kr에 쓰이는 프로젝트 지원X (major version)

**Candidates**

1. [naiveui](https://www.naiveui.com/en-US/light/components/avatar) - 이슈 등록 글이 중국어가 더 많음
   - sketch kit free
   - Naive UI Snippets - vs code
2. [antdv](https://antdv.com/components/overview) - figma kit 구매함 - 버그 답변이 죄다 중국어
3. [primevue](https://www.primefaces.org/primevue/autocomplete) ✅
   - figma$250? - deprecated - [https://www.figma.com/community/file/890589747170608208](https://www.figma.com/community/file/890589747170608208)
   - vuelidate
   - radar chart
4. [vuetifyjs](https://next.vuetifyjs.com/en/components/all/)
   - [https://store.vuetifyjs.com/products/vuetify-ui-kit-figma](https://store.vuetifyjs.com/products/vuetify-ui-kit-figma) free
5. [https://element-plus.org/en-US/component/button.html](https://element-plus.org/en-US/component/button.html)
   - [figma template](https://www.figma.com/community/file/1021254029764378306) - free, non en
6. [ui-elements](https://vuestic.dev/ko/ui-elements/alert)
   - no figma or sketch
7. [inkline](https://www.inkline.io/docs/forms/checkbox)
   - storybook, no figma or sketch

## Week 48, 2022

### Refine package.json product section

```
pnpm install --prod --frozen-lockfile
```

product에 쓰지 않는 package 설치를 피하여 새 package 설치 시의 시간을 37 → 19초로 줄임.  
js resource size도 9mb 정도 줄음 (github cache 확인)

## Week 47, 2022

### nuxt3 generate false negative error

sentry setting test 때문에 일부러 error를 내고 배포했는데 계속 정상 동작함.  
github actions log 확인하니...
![](assets/images/what-i-struggle-in/nuxt3-generate__github-actions.webp)  
generate시에

> WARN Using experimental payload extraction for full-static output. You can opt-out by setting experimental.payloadExtraction to false.

라고 뜨더니... 관련있나?

## Week 44, 2022

### [[Google app script about i18n|dev.tools.google.apps-script#script-of-sheet---i18n-json]]
