---
id: 6ap7amibzjhel2cuq17yxwx
title: 리소스 우선순위 - preload, preconnect, prefetch
desc: ""
updated: 1689748559408
created: 1689748255799
---

> https://beomy.github.io/tech/browser/preload-preconnect-prefetch/

## preload[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#preload)

현재 페이지에서 사용될 것이 확실한 리소스들을 `preload`해야 합니다. `preload`는 브라우저에게 현재 페이지에서 필요한 리소스를 빠르게 가져오게 합니다.

```html
<link rel="preload" as="script" href="super-important.js" />
<link rel="preload" as="style" href="critical.css" />
```

`preload`는 위의 코드와 같이 `<link rel="preload" as="...">`와 같이 사용합니다.

### 주의 사항[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A3%BC%EC%9D%98-%EC%82%AC%ED%95%AD)

`preload`를 사용할 때 주의해야 할 몇 가지 사항을 살펴보도록 하겠습니다.

#### `as` 속성 사용[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#as-%EC%86%8D%EC%84%B1-%EC%82%AC%EC%9A%A9)

`as` 속성을 사용하여 리소스의 유형을 브라우저에 알려줘야 합니다. 올바른 유형이 설정되어 있지 않다면 브라우저는 해당 리소스를 사용하지 않습니다.

#### 중복 리소스 참조[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A4%91%EB%B3%B5-%EB%A6%AC%EC%86%8C%EC%8A%A4-%EC%B0%B8%EC%A1%B0)

`preload`는 브라우저가 반드시 리소스를 가져오게 만듭니다. 리소스를 중복 참조하면 중복된 개수만큼 리소스를 가져오기 때문에 리소스를 중복해서 참조하지 않도록 해야 합니다.

#### 반드시 사용되는 리소스에만 사용[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EB%B0%98%EB%93%9C%EC%8B%9C-%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94-%EB%A6%AC%EC%86%8C%EC%8A%A4%EC%97%90%EB%A7%8C-%EC%82%AC%EC%9A%A9)

`preload`는 현재 페이지에서 반드시 사용되는 리소스에만 사용되어야 합니다.

`<link rel="preload" as="...">`를 이용하여 리소스를 가져왔지만 현재 페이지에서 3초 내로 사용되지 않는 리소스는 브라우저에서 경고가 출력 됩니다. 필요하지 않는 것을 가져오지 하지 않도록 주의해야 합니다.

### 사용 사례[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%82%AC%EC%9A%A9-%EC%82%AC%EB%A1%80)

이번에는 `preload`를 사용하기 좋은 리소스를 살펴보도록 하겠습니다.

#### 폰트[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%ED%8F%B0%ED%8A%B8)

사용자가 사이트의 폰트를 기다리는 시간을 감소시키고, 시스템 폰트와 선언된 포트의 충돌을 해결할 수 있습니다.

```html
<link
  rel="preload"
  as="font"
  crossorigin="crossorigin"
  type="font/woff2"
  href="myfont.woff2"
/>
```

위의 코드와 같이 폰트를 `preload`해서 브라우저에게 폰트가 즉시 필요하다는 것을 알려줄 수 있습니다.

#### Critical Rendering Path의 CSS와 JavaScript[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#critical-rendering-path%EC%9D%98-css%EC%99%80-javascript)

페이지 성능을 측정할 때 중요한 개념 중, Critical Rendering Path가 있습니다([\[Browser\] Critical Rendering Path 최적화](https://beomy.github.io/tech/browser/critical-rendering-path) 참고). Critical Rendering Path란 초기 렌더링 전에 반드시 로드되어야 할 리소스를 말합니다.

```html
<link rel="preload" as="script" href="super-important.js" />
<link rel="preload" as="style" href="critical.css" />
```

위의 코드와 같이 초기 렌더링에 반드시 필요한 리소스를 `preload`해서 렌더링 속도를 높일 수 있습니다.

## preconnect[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#preconnect)

현재 페이지에서 외부 도메인의 리소스를 참고하는 것을 브라우저에게 알려 미리 외부 도메인과 연결을 설정할 수 있게 합니다.

`preconnect`를 사용하면 브라우저가 사이트에 필요한 연결을 미리 예상할 수 있게 됩니다. 브라우저는 필요한 소켓을 미리 설정할 수 있기 때문에 DNS, TCP, TLS 왕복에 필요한 시간을 절약할 수 있게 됩니다.

```html
<link rel="preconnect" href="https://example.com" />
```

위의 코드와 같이 `preconnect`를 사용할 수 있습니다.

### 주의사항[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD)

`preconnect`는 외부 도메인과 연결을 구축하기 때문에 많은 CPU 시간을 차지할 수 있습니다. 보안 연결의 경우 더 많은 시간을 차지할 수 있습니다. 10초 이내로 브라우저가 닫힌다면, 이전의 모든 연결 작업은 낭비되는 것이기 때문에 브라우저가 빨리 닫힐 수 있는 페이지에서는 `preconnect`를 사용하지 않는 것이 좋습니다.

### 사례[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%82%AC%EB%A1%80)

이번에는 `preconnect`를 사용하기 좋은 예를 살펴보도록 하겠습니다.

#### 정확한 경로를 알 수 없을 때[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A0%95%ED%99%95%ED%95%9C-%EA%B2%BD%EB%A1%9C%EB%A5%BC-%EC%95%8C-%EC%88%98-%EC%97%86%EC%9D%84-%EB%95%8C)

주어진 CDN으로 부터 리소스를 가져와야 한다는 것은 알지만 정확한 경로를 모르는 상황이 발생할 수 있습니다. 예를 들면 브라우저 별로 가져와야 하는 JQuery 등의 리소스 버전이 다를 때 가져와야 할 CDN 주소는 알지만 정확한 경로는 알지 못하는 상황을 이야기할 수 있습니다.

이러한 경우 브라우저는 리소스를 가져오지는 않지만 서버에 미리 연결하여 연결에 필요한 시간을 절약할 수 있습니다. 브라우저는 파일이 필요하기 전에는 리소스를 가져오지 않지만 적어도 연결은 먼저 처리해서 리소스를 요청하고 가져오는 여러 번의 왕복을 기다리지 않아도 됩니다.

#### 미디어 스트리밍[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EB%AF%B8%EB%94%94%EC%96%B4-%EC%8A%A4%ED%8A%B8%EB%A6%AC%EB%B0%8D)

스크립트가 로드되고 스트리밍 데이터를 처리할 준비가 될 때까지 스트리밍을 기다리고 싶을 수 있습니다. `preconnect`는 미리 연결을 하기 때문에 리소스를 가져올 준비가 되면 연결을 설정하는 것이 아니라 미리 연결된 설정에 따라 리소스를 가져와 연결을 설정하는 대기 시간을 줄 일 수 있습니다.

## prefetch[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#prefetch)

미래에 사용될 것이라고 예상되는 리소스들을 `prefetch`해야 합니다. 브라우저는 미래에 사용될 리소스들을 가져와 캐시에 저장합니다.

`prefetch`는 사용자가 다음에 할 행동을 미리 준비하는데 적합한 기능입니다. 예를 들어, 결과 목록에서 첫 번째 제품 상세 페이지를 가져오거나 콘텐츠의 다음 페이지를 가져오는 것을 이야기할 수 있습니다.

```html
<link rel="prefetch" href="page-2.html" />
```

위의 코드와 같이 `prefetch`를 사용할 수 있습니다.

### 주의사항[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD-1)

`prefetch`를 사용할 때 기억해야 할 몇 가지 내용들을 살펴보도록 하겠습니다.

#### 재귀적으로 동작하지 않는다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%9E%AC%EA%B7%80%EC%A0%81%EC%9C%BC%EB%A1%9C-%EB%8F%99%EC%9E%91%ED%95%98%EC%A7%80-%EC%95%8A%EB%8A%94%EB%8B%A4)

`prefetch`는 재귀적으로 동작하지 않습니다.

```html
<link rel="prefetch" href="page-2.html" />
```

위의 코드와 같이 `prefetch`를 사용한다면, `page-2.html`이라는 HTML 리소스를 가져올 수 있지만 `page-2.html`에서 사용되는 CSS 등의 리소스들은 가져오지 않습니다.

#### Override 목적으로 사용하지 않는다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#override-%EB%AA%A9%EC%A0%81%EC%9C%BC%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EB%8A%94%EB%8B%A4)

`prefetch`는 Override, 즉 재정의 할 목적으로 사용되면 안 됩니다.

```html
<html>
  <head>
    <link rel="prefetch" href="optional.css" />
    <link rel="stylesheet" href="optional.css" />
  </head>
  <body>
    Hello!
  </body>
</html>
```

위의 코드와 같이 `prefetch`를 사용할 경우, `<link rel="prefetch" href="optional.css">`의 바로 뒤따라오는 `<link rel="stylesheet" href="optional.css">`의 우선순위를 낮출 것이라고 생각할 수 있지만 그렇지 않습니다.

실제로는 한 번은 가장 높은 우선순위로, 나머지 한 번은 가장 낮은 우선순위로 스타일을 2번 가져오게 됩니다. 렌더 차단하는 CSS를 기다려야 할 뿐만 아니라, 파일을 두 번 다운로드해야 하는 낭비가 발생하기 때문에 동일한 리소스를 여러 번 가져와야 하는 경우는 피하는 것이 좋습니다.

## Vue.JS의 Lazy load[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#vuejs%EC%9D%98-lazy-load)

Single Page Application(SPA)의 고질적인 문제는 소스코드가 하나로 뭉쳐져서 사용자가 처음 웹사이트에 접속했을 때 큰 파일을 다운로드하고 파싱을 하느라 초기 렌더링이 느려진다는 점입니다. 이 문제를 해결하기 위해 vue-route는 현재 라우터에서 필요한 파일만 받을 수 있도록 하는 코드 분할(Code Splitting) 기능을 제공합니다. ([\[vue-router\] Lazy Loading Routes](https://beomy.tistory.com/80) 참고)

### prefetch 기능[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#prefetch-%EA%B8%B0%EB%8A%A5)

vue-cli3 부터 `prefetch`가 기본 기능으로 추가되었습니다. 비동기 컴포넌트 정의된 컴포넌트를 `prefetch`로 가져오도록 기본 기능으로 제공합니다.

코드 분할을 통해 만들어진 chunk 파일들이 위의 그림과 같이 HTML의 `head`에 `<link href="..." ref="prefetch">`와 같이 추가됩니다.

#### prefetch 기능 제거[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#prefetch-%EA%B8%B0%EB%8A%A5-%EC%A0%9C%EA%B1%B0)

`prefetch` 기능을 제거 방법을 이야기하도록 하겠습니다.

```js
// vue.config.js
module.exports = {
  ...
  chainWebpack: (config) => {
    ...
    config.plugins.delete('prefetch')
    ...
  },
  ...
}
```

`vue.config.js` 파일의 `chainWebpack` 밑에 `config.plugins.delete('prefetch')`를 선언하면 `prefetch` 기능이 제거됩니다.

#### 특정 컴포넌트에 prefetch 적용하기[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%ED%8A%B9%EC%A0%95-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%97%90-prefetch-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)

```js
import(/* webpackPrefetch: true */ "./views/About.vue")
```

특정 컴포넌트에 `prefetch`를 적용하고 싶다면 위의 코드와 같이 비동기 컴포넌트를 정의할 때, `/* webpackPrefetch: true */` 주석을 추가하면 됩니다.

### 주의사항[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%A3%BC%EC%9D%98%EC%82%AC%ED%95%AD-2)

`prefetch`는 미래에 사용될 수 있는 리소스를 미리 캐시 해 두기 때문에, 매우 유용한 기능입니다. 하지만 vue-cli3에서 이 기능을 사용할 때 몇 가지를 주의해야 합니다.

#### 비동기 컴포넌트로 정의되었다면 모두 prefetch 된다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A1%9C-%EC%A0%95%EC%9D%98%EB%90%98%EC%97%88%EB%8B%A4%EB%A9%B4-%EB%AA%A8%EB%91%90-prefetch-%EB%90%9C%EB%8B%A4)

vue-cli3에서 제공하는 `prefetch` 기능은 생각보다 똑똑하지 않은 것 같습니다.

위 그림의 `global.result-table`은 초기 렌더링에 필요한 컴포넌트입니다. 하지만 `prefetch`로 리소스가 가장 낮은 우선순위로 가져오게 되어 초기 렌더링 속도를 떨어트릴 수 있습니다.

#### Request 요청 수가 증가한다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#request-%EC%9A%94%EC%B2%AD-%EC%88%98%EA%B0%80-%EC%A6%9D%EA%B0%80%ED%95%9C%EB%8B%A4)

vue-cli3에서 제공하는 `prefetch` 기능은 비동기 컴포넌트로 정의된 모든 리소스를 `prefetch`로 가져오는 것으로 보입니다. 그래서 당장 사용하지 않더라고 캐시에 담아두게 됩니다. 비동기 컴포넌트로 정의된 모든 리소스를 다운로드하게 되기 때문에 Request 요청 수가 많아지게 됩니다.

vue-cli3의 prefetch 사용 시 105개를 Request 요청합니다.

vue-cli3의 prefetch 제거 시 총 47개의 Request를 요청하였습니다. `prefetch` 기능을 제거하였다면 라우터가 이동될 때마다 해당 라우터에서 필요한 리소스를 `head`에 `link` 태그로 추가됩니다. 즉 미리 리소스를 가져오는 것이 아니라 필요할 때 그때그때 리소스를 가져오게 됩니다. 한번 가져온 리소스는 다시 요청하지는 않습니다.

#### Load 타임스탬프 살펴보기[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#load-%ED%83%80%EC%9E%84%EC%8A%A4%ED%83%AC%ED%94%84-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0)

`prefetch`를 사용하는 가장 큰 이유는 당연히 렌더링 시간을 줄이기 위해서입니다. 이번에는 브라우저가 첫 렌더링을 완료하는 시간이 어떻게 다른지 살펴보도록 하겠습니다. Fast 3G, webpack-dev-serve로 테스트하였습니다.

위의 그림은 `prefetch` 기능을 사용할 때 크롬 개발자 도구에서 Network 탭입니다. 파란 글씨의 `DOMContentLoaded`와 빨간 글씨의 `Load` 타임스탬프를 주목합시다. (두 타임스탬프의 자세한 내용은 [\[Browser\] Critical Rendering Path 최적화](https://beomy.github.io/tech/browser/critical-rendering-path/#%ED%83%80%EC%9E%84%EC%8A%A4%ED%83%AC%ED%94%84)를 참고 바랍니다.) `DOMContentLoaded` 타임스탬프는 렌더 트리를 생성할 수 있는 시점을 나타냅니다. 위의 그림을 보면 4분 후에야 렌더 트리를 그릴 수 있게 됩니다.

`prefetch` 기능을 제거한 후 렌더링 하는데 걸리는 시간은 `DOMContentLoaded` 타임스탬프를 보면 2.8분 후에 렌더 트리를 그릴 수 있는 것을 볼 수 있습니다.

### 고찰[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EA%B3%A0%EC%B0%B0)

`prefetch`를 사용하면 리소스를 미리 캐시 해 두기 때문에 성능이 향상될 것이라고 예상이 됩니다. 하지만 vue-cli3에서 제공하는 `prefetch` 기능을 사용하면 오히려 첫 렌더링 성능이 저하되는 것으로 확인됩니다. 이런 원인은 2가지로 볼 수 있습니다.

#### 1\. 현재 페이지에서 반드시 필요한 리소스가 가장 낮은 우선순위로 받게 됩니다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#1-%ED%98%84%EC%9E%AC-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%97%90%EC%84%9C-%EB%B0%98%EB%93%9C%EC%8B%9C-%ED%95%84%EC%9A%94%ED%95%9C-%EB%A6%AC%EC%86%8C%EC%8A%A4%EA%B0%80-%EA%B0%80%EC%9E%A5-%EB%82%AE%EC%9D%80-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84%EB%A1%9C-%EB%B0%9B%EA%B2%8C-%EB%90%A9%EB%8B%88%EB%8B%A4)

꼭 필요한 리소스가 가장 낮은 우선순위로 리소스를 받게 되면, 당연히 렌더링 완료되는 시간도 늦어지게 됩니다.

#### 2\. 비동기 컴포넌트로 정의된 모든 리소스를 다운로드하게 되어, 다운로드해야 할 리소스 개수가 증가하게 됩니다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#2-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A1%9C-%EC%A0%95%EC%9D%98%EB%90%9C-%EB%AA%A8%EB%93%A0-%EB%A6%AC%EC%86%8C%EC%8A%A4%EB%A5%BC-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%98%EA%B2%8C-%EB%90%98%EC%96%B4-%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C%ED%95%B4%EC%95%BC-%ED%95%A0-%EB%A6%AC%EC%86%8C%EC%8A%A4-%EA%B0%9C%EC%88%98%EA%B0%80-%EC%A6%9D%EA%B0%80%ED%95%98%EA%B2%8C-%EB%90%A9%EB%8B%88%EB%8B%A4)

1번 이슈와 2번 이슈가 콜라보 되면서 렌더링 완료 시간도 더욱 느려집니다. 다운로드해야 하는 리소스 개수가 많아지고, 그중에서 꼭 필요한 리소스가 가장 마지막에 받아진다면 가장 마지막 리소스가 받아진 이후에야 렌더링이 완료되게 됩니다.

#### 필요한 파일만 `prefetch` 하는 것이 좋습니다.[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%ED%95%84%EC%9A%94%ED%95%9C-%ED%8C%8C%EC%9D%BC%EB%A7%8C-prefetch-%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B4-%EC%A2%8B%EC%8A%B5%EB%8B%88%EB%8B%A4)

vue-cli3가 기본으로 제공하는 `prefetch` 기능을 사용하면 모든 비동기 컴포넌트를 다운로드해 캐시 하기 때문에 이후의 사용자 행동에 대한 반응은 빨라질 수 있습니다. 초기 렌더링 속도를 향상시키느냐, 초기 렌더링 후의 업데이트 속도를 향상시키느냐 사이의 절충안을 찾아야 할 것 같습니다.

필요한 컴포넌트 혹은 리소스에만 `prefetch`하여 사용하여 둘 사이의 절충안을 찾는 것이 좋을 것 같습니다.

## 요약[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%9A%94%EC%95%BD)

1. 현재 페이지에서 반드시 사용되는 리소스는 `preload` 합니다.
2. 외부 도메인의 리소스는 `preconnect` 합니다.
3. 미래에 사용되는 리소스는 `prefetch` 합니다.
4. vue-cli3에서는 `prefetch`가 기본으로 제공합니다.
5. vue-cli3를 사용한다면 필요한 리소스에만 `prefetch`하는 것이 좋습니다.

##### 참고[](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/#%EC%B0%B8%EA%B3%A0)

- [https://developers.google.com/web/fundamentals/performance/resource-prioritization?hl=ko](https://developers.google.com/web/fundamentals/performance/resource-prioritization?hl=ko)
- [https://medium.com/@koh.yesl/preload-prefetch-and-priorities-in-chrome-15d77326f646](https://medium.com/@koh.yesl/preload-prefetch-and-priorities-in-chrome-15d77326f646)
- [https://medium.com/@jeongwooahn/vue-js-lazy-load-적용하기2-3f1a2f4a4ee8](https://medium.com/@jeongwooahn/vue-js-lazy-load-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B02-3f1a2f4a4ee8)
- [https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content](https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content)
- [https://css-tricks.com/prefetching-preloading-prebrowsing/](https://css-tricks.com/prefetching-preloading-prebrowsing/)
- [https://www.keycdn.com/blog/resource-hints](https://www.keycdn.com/blog/resource-hints)
- [https://medium.com/@pakss328/resource-hint-8fb4e56ee042](https://medium.com/@pakss328/resource-hint-8fb4e56ee042)
- [https://caniuse.com/#search=preload](https://caniuse.com/#search=preload)
- [https://caniuse.com/#search=prefetch](https://caniuse.com/#search=prefetch)
- [https://caniuse.com/#search=preconnect](https://caniuse.com/#search=preconnect)
