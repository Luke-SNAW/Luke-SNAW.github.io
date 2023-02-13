---
id: 6645fjtiqxtko03nuccgjj2
title: "What I struggled 🧗‍♂️/📣 brag In"
desc: ""
updated: 1676248652512
created: 1669264809793
---

## Week 7, 2023 - Windows Subsystem for Linux

밑의 국성원 유전자 검사 신고 작업. 데이터 만드시는 분들이 야근하고 토요일에도 작업하셔서 일요일에 유효성 검사랑 실제 데이터 등록 테스트를 함.

WSL 설치 후 pnpm i error. 하단 답글보니 이게 뭔가 싶다. 결국 windows 영향을 받는다는 거잖아. 날리고 windows용으로 세팅

### [Solution for WSL](https://stackoverflow.com/a/58414196)

I solved this by mounting C:/ with default permissions bound to my user instead of root. I followed the guide here: [https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements/](https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements/)

```shell
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata,uid=1000,gid=1000,umask=22,fmask=111
```

This mounts all files on the C drive as my user instead of root. Therefore sudo is not needed to run `npm i`

### Volta

windows 설치 후 실행이 안됨

> https://github.com/volta-cli/volta/issues/1392#issuecomment-1336254236

좀 찾아보니 환경변수 확인하라고 함. 됨. [공식 문서](https://docs.volta.sh/guide/getting-started) linux 설치에는 환경변수 등록하라고 해놓고 windows에는 그런거 안써있는데?

## Week 6, 2023 - 국생원 유전자 검사 신고 - Playwright script

실행이 빠르고 test code recording이 편한 playwright로…

## Week 5, 2023 - Cypress → Playwright → Cypress

Playwright의 Test code structuring 문제

### Playwright

playwright는 test 마다 독립적인걸 가정하여 parallel하게 실행하도록 [권장](https://playwright.dev/docs/test-parallel#serial-mode).

- **[[Question] Running projects in sequential order, files in parallel #19889](https://github.com/microsoft/playwright/issues/19889)**

문제는 하나의 story를 테스트 하는데 **step별로 나눌 수 없음**. (feature request는 있는데 낮은 우선순위로 1년 반 동안 진전없음)

- **[[Feature] It would be nice if test.step showed up in trace view actions #8682](https://github.com/microsoft/playwright/issues/8682)**
- **[[Feature] Show test steps `test.step` in the `list` report (and on assertion fails) #20532](https://github.com/microsoft/playwright/issues/20532)**

[어떤 글](https://timdeschryver.dev/blog/keep-your-playwright-tests-structured-with-steps)에는 test.step을 쓰라고 했는데, 써보니 step3에서 error가 나도 전체 story에서 error났다는 보고만 나온다. debug mode로 돌려도 같음. (interface가 달라보이긴 한데...)

test.describe.config serial로 test 나눠서 쓰면 가능하긴 한데, test하나 끝날 때마다 browser context가 reset 됨. (=page reset)

완전 deal breaker인데, playwright를 써야 하나?
global config로 serial하게 하면 될까? test.describe.config랑 차이 없을 거 같은데
test마다 my-test setting을 하도록 함? step의 시작단계 마다 context를 setting하라고?

문서도 너무 빈약 https://playwright.dev/docs/api/class-test#test-step

> test.step  
> Declares a test step.

### Cypress

찾아보니 cypress에서도 test code recording 기능이 있다. 시험 기능이지만. ([experimentalStudio](https://www.cypress.io/blog/2022/08/30/how-to-use-studio-in-cypress-10-7))

ver.10.0에서 삭제했다가 [feedback](https://github.com/cypress-io/cypress/discussions/21561)에서 부활시켜달라는 요청이 많아서 ver.10.7에서 부활. 현재 ver.12.5.1. 반년 정도 지났는데 아직도 experimental 단계라는게 좀 그렇지만, 내렸다가 feedback 받고 부활한거라 없어질거 같지는 않음. 해서 cypress로 계속 쓸 듯.

오랜만에 cypress 돌려보니 env 실행 자체가 너무 느리다. playwright 쓰다가 쓰니 역체감이 심함.

## Week 4, 2023 - AWS EC2 테스트 서버 볼륨 삭제됨

### 경과

아침 출근하니 테스트 서버 CPU 점유 경고가 뜸. 확인해보니 100%에서 계속 유지되어서 EC2 Instance를 reboot.  
몇 분 뒤에 변화가 없어서 suspend. 몇 분 뒤에 웹 사이트 접속 안되어 확인해보니 종료 됨. ??? log를 확인해보니 AutoScailing이 죽여버림.

![](assets/images/what-i-struggled-brag-in/week4-2023__test-server.webp)

더 확인해보니 자동 생성된 instance의 volumn이 계승되지 않고 새로 생성 됨. 이거까진 이해가 가는데 기존 volumn을 자동 삭제? 이런 방식이면 믿고 쓸 수가 있나? 나중에 알아보니 EC2 생성 시 기본으로 [root volumn이 종료 시 삭제 설정](https://aws.amazon.com/ko/premiumsupport/knowledge-center/deleteontermination-ebs/)된다. 🤨

### 해결

[[dev.devops.github-actions--s3--code-deploy]] [^week4-2023__test-server], [[dev.devops.github-actions--code-deploy--git-pull]]를 통해 복구.

[^week4-2023__test-server]: `week4-2023__test-server`: 작성해놓은 문서의 command text에 spacebar 대신 다른 보이지 않는 문자가 들어가서 copy&paste 했을 때 error 계속 발생했었음 🤨

## Week 3, 2023 - Nuxt generate 시, dynamic route에서 payload error

### 현상

next generate로 생성된 사이트에서 payload 생성 안하는 dynamic route path에서도 payload를 요구[^ssr-prerendering?]

[^ssr-prerendering?]: `ssr-prerendering?` - SSR을 통해 prerendering 할 수도 있지만, report의 경우는 개체 별 페이지를 모두 생성시키진 않을 예정이므로

### 해결

crawlLinks: true와 함께 nuxt build로 생성

```js
//nuxt.config.js
{
  nitro: {
    // 이 config 없이 nuxt generate하면 dynamic route까지 payload를 try. error 발생.
    prerender: {
      crawlLinks: true,
      routes: ['/', '/ko'],   // /ko는 @nuxtjs/i18n module의 한국어 지원을 위해
    },
  }
}
```

### 참고한 문서들

- https://nuxtjs.org/docs/concepts/nuxt-lifecycle/
- https://stackoverflow.com/questions/61485508/how-nuxt-generate-dynamic-routes
- https://nuxt.com/docs/api/configuration/nuxt-config/#generate
- https://github.com/nuxt/rfcs/issues/22
- https://nuxtjs.org/docs/features/data-fetching/#:~:text=this%20hook%20blocks%20route%20navigation%20until%20it%20is%20resolved%2C%20displaying%20a%20page%20error%20if%20it%20fails.

## Week 2, 2023 - Playwright CORS setting

### Allow Extension

결론은 실패. load는 됐지만 기본 off로 되어 있어 browser 처음 실행할 때 손으로 on 시켜야 함.

```shell
# Run find . -type d -iname "<EXTENSION ID HERE>"
```

```js
// playwright.config.js
use: {
   launchOptions: {  // https://playwright.dev/docs/api/class-testoptions#test-options-launch-options
      args: [  // https://playwright.dev/docs/chrome-extensions
         `--disable-extensions-except=~/Library/Application Support/Google/Chrome/Default/Extensions/lfhmikememgdcahcdlaciloancbhjino/0.3.5_0`,
      ],
   },
}
```

### Off web security

이쪽으로 해결[^chromium-only]

[^chromium-only]: `chromium-only` - chromium만 해결. 다른 browser도 해당 option을 찾아 넣든가, CORS 세팅을 부탁하든가 해야 함.

```js
// playwright.config.js
use: {
   launchOptions: {  // https://playwright.dev/docs/api/class-testoptions#test-options-launch-options
      args: ['--disable-web-security'],
   },
}
```

## Week 2, 2023 - Playwright 도입

cypress에 비해 다음 이점이 확연하다. (그리고 [[단점 | journal.what-i-struggled-brag-in#week-5-2023---playwright-test-code-structuring-draft]]이 드러나는데...)

1. 속도가 빠르고 (browser를 직접 띄우지 않고 테스트만 실행시킬 수 있음)
2. VS code와의 연결이 더욱 긴밀하다.
   1. browser에서의 입력을 test code로 생성해줌.
   2. vs code에서 selector에 cursor를 두면, browser에서 해당 element가 표시됨

## Week 2, 2023 - temp branch 운영

### 문제

배포 환경에서만 테스트 할 수 있는 내용이라면 지속적으로 수정·배포·테스트를 진행  
이 과정 중에 다른 개발자가 테스트 서버에 배포하면 내용이 서로 상실되거나 브랜치 conflict가 빈번하게 발생할 수 있으므로, 개발자끼리 테스트 브랜치, 서버를 쓰겠다고 알린 뒤에 독점적으로 사용 중
(fixup으로 쌓아가며 테스트할 수 있으나, 결국엔 commit을 정리한 후, 정리한 걸 다시 테스트해야 하는데, 이 때 conflict가 대량 발생할 수 있다.)

### 해결

temp branch 운영. husky를 이용하여 temp branch를 push하기 전에 origin/test branch를 merge

> https://stackoverflow.com/questions/6372334/git-commit-hooks-per-branch/6376054#6376054

### Trouble shooting

push할 때 다음 error가 발생하면 `chmod`로 해당 파일에 실행 권한을 줄 것

> hint: The '.husky/pre-push' hook was ignored because it's not set as executable.

test branch merge 후 remote에는 push됐는데, local에서는 push 안된 걸로 표시  
→ post push hook이 없어서 merge가 일어나면 손으로 fetch 입력해야 함. 아니면 fetch 선행 입력

```shell
git push;git fetch
```

## Week 52, 2022 - [Tailwind - Dynamic class names](https://tailwindcss.com/docs/content-configuration#dynamic-class-names)

```js
class = `bg-${ zero ? pageColor : baseColor}` // not work
class = zero ? `bg-${pageColor}` : `bg-${baseColor}` // not work
```

## Week 51, 2022 - SPA framework - S3 - CloudFront 배포 시 404 error 처리

없는 URI로 접근 시 403 error가 뜬다. [아마도 해당 url path를 cloudFront에서 인식하지 못해서 S3로 요청이 가고 public이 아니니 permission denied 에러](https://dexlee.tistory.com/189#:~:text=%ED%95%B4%EB%8B%B9%20url%20path%EB%A5%BC%20cloudFront%EC%97%90%EC%84%9C%20%EC%9D%B8%EC%8B%9D%ED%95%98%EC%A7%80%20%EB%AA%BB%ED%95%B4%EC%84%9C%20S3%EB%A1%9C%20%EC%9A%94%EC%B2%AD%EC%9D%B4%20%EA%B0%84%EB%8B%A4.%20public%EC%9D%B4%20%EC%95%84%EB%8B%88%EB%8B%88%20%EB%8B%B9%EC%97%B0%ED%9E%88%20permission%20denied%20%EC%97%90%EB%9F%AC%20%EB%B0%9C%EC%83%9D.)
![](assets/images/what-i-struggled-brag-in/s3-cloudfront-404-error.webp)

cloudfront에서 403 error를 SPA framework index.html로 처리하도록 해주면 framework에서 404 처리해 줌
![](assets/images/what-i-struggled-brag-in/s3-cloudfront-404-custom-setting.webp)

## Week 50, 2022 - tailwind css

새 nuxt3 project에 tailwind 도입.
그 동안 제작자 소개글에서 motivation과 결과가 모순되는 걸 봐서 꺼렸는데, code colocation으로 인한 DX, 속도 향상 때문에 써보기로 함.

## Week 49, 2022 - Nuxt3 UI Framework

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

## Week 48, 2022 - Refine package.json product section

```
pnpm install --prod --frozen-lockfile
```

product에 쓰지 않는 package 설치를 피하여 새 package 설치 시의 시간을 37 → 19초로 줄임.  
js resource size도 9mb 정도 줄음 (github cache 확인)

## Week 47, 2022 - nuxt3 generate false negative error

sentry setting test 때문에 일부러 error를 내고 배포했는데 계속 정상 동작함.  
github actions log 확인하니...
![](assets/images/what-i-struggled-brag-in/nuxt3-generate__github-actions.webp)  
generate시에

> WARN Using experimental payload extraction for full-static output. You can opt-out by setting experimental.payloadExtraction to false.

라고 뜨더니... 관련있나?

## Week 45, 2022 - TanStack Query 적용

Powerful asynchronous state management, server-state utilities and data fetching.  
cache on API request.  
report detail modal → page로 변환함에 따라 summary 화면과 전환이 잦고 그 때마다 API request를 함.  
stale time을 설정하여 정해진 시간 내에는 request 없이 cache data 활용하도록 수정

| <video width="320" height="240" controls><source src="/assets/movs/what-i-struggled-brag-in/tanstack-query__before.webm" type="video/webm"></video> | <video width="320" height="240" controls><source src="/assets/movs/what-i-struggled-brag-in/tanstack-query__after.webm" type="video/webm"></video> |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| TanStack Query 적용 이전. 리포트 요약↔상세 페이지 이동 시 마다 API request 발생                                                                     | TanStack Query 적용 이후. Cache를 활용하기 때문에 리포트 요약 페이지에서 추가 API request가 없어짐                                                 |

## Week 44, 2022 - [[Google app script about i18n|dev.tools.google.apps-script#script-of-sheet---i18n-json]]

## Week 39, 2022 - Package manager yarn → pnpm

배포 시간 -40s (package 설치 시간 감소) - 캐시활용 차이? 같은 script인데…

![](assets/images/genoplan/yarn.webp)

![](assets/images/genoplan/pnpm.webp)

local disk space 절약

---

한 달 188k transaction

## Week 29, 2022 - Webpack v3 → v5

vue3이 나온 시점에서 무조건 최신 plugin을 쓰면 호환이 안되므로 vue2에 맞는 버전 일일히 찾아 설치함.

## Week 15, 2022 - Cypress

![](assets/images/genoplan/cypress.webp)
