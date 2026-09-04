
## Conditionally add properties💡 in the object from [11 Useful Modern JavaScript Tips](https://medium.com/dhiwise/11-useful-modern-javascript-tips-9736962ed2cd)

```javascript
const isValid = false
const age = 18

const person = {
  name: "Krina",
  ...(isValid && { isActive: true }),
  ...(age >= 18 || (isValid && { card: 0 })),
}
```

## [58 JavaScript Tips and Tricks for Web Developers](https://blog.bitsrc.io/common-js-development-skills-5053f0a74ced)

## Loop array

```js
const array = ["a", "b", "c"]

for (let item of array) {
  console.log(item)
}
```

## Copy text to clipboard

```js
const copyTextarea = document.querySelector("#urlToShare")
copyTextarea.focus()
copyTextarea.select()

try {
  document.execCommand("copy")
  alert(this.$t("URL이 복사되었습니다. 원하는 곳에 붙여넣기 하세요."))
} catch (err) {
  alert(this.$t("복사가 실패했습니다. 직접 복사하세요."))
}
```

## Throttling requests

```js
let cRequest = 0

export const preventDOSsuspiciousAction = () => {
  cRequest++
  return new Promise((resolve) => {
    setTimeout(() => {
      cRequest = 0
      resolve()
    }, cRequest * 300)
  })
}
//
window.promisePost = async (URL, prms, noToast = false, loadingFor) => {
  showBusyIndicator(loadingFor)
  await preventDOSsuspiciousAction()

  return new Promise((resolve, reject) => {
    $.post(URL, prms)
      .done((rsp) => {
        if (rsp.success) {
          resolve(rsp)
          return
        }
        if (!noToast) vueObj.$toast.open(rsp.message)
        reject(rsp)
      })
      .fail(reject)
      .always(() => {
        hideBusyIndicator(loadingFor)
      })
  })
}
```

## [Deep copy in JavaScript](https://web.dev/baseline-features/#deep-copy-in-javascript)

```js
const original = { id: 0, prop: { name: "Tom" } }
/* Old hack */
const deepCopy = JSON.parse(JSON.stringify(original))
/* New way */
const deepCopy = structuredClone(original)
```
