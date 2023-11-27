---
id: p6jdsvhol2ebyzilnb5u3ot
title: Vue
desc: ""
updated: 1701070568025
created: 1646815969488
---

## Collections

- [Note: The main difference is that the watchEffect starts instantly while the watch() runs lazily](<https://www.syncfusion.com/blogs/post/vue-composition-api-vs-react-hooks.aspx#:~:text=Note%3A%20The%20main%20difference%20is%20that%20the%20watchEffect%20starts%20instantly%20while%20the%20watch()%20runs%20lazily>)
- [Top 7 tips/features in Vue 3](https://medium.com/@felixdavid12/top-7-tips-features-in-vue-3-7119cee4a918) 3. Reactive CSS
- [How to Destructure Props in Vue (Composition API)](https://dmitripavlutin.com/props-destructure-vue-composition/)
- [The new Wikipedia appearance that took the whole village](https://medium.com/@dlyall/the-new-wikipedia-appearance-that-took-a-whole-village-52637b34a00f)
  - [Vue.js has been selected as Wikimedia Foundation's future JavaScript framework](https://lists.wikimedia.org/hyperkitty/list/wikitech-l@lists.wikimedia.org/thread/SOZREBYR36PUNFZXMIUBVAIOQI4N7PDU/)
  - [RFC: Adopt a modern JavaScript framework for use with MediaWiki](https://phabricator.wikimedia.org/T241180) and [EvanYou comment](https://phabricator.wikimedia.org/T241180#:~:text=Project%20lead%20of%20Vue.js%20here.)
- [What to Expect from Vue in 2023 and How it Differs from React](https://thenewstack.io/vue-2023/)
- [Why I’m sticking with Vue in 2023](https://medium.com/@lindblomdev/why-im-sticking-with-vue-in-2023-d67bce7bc2f4)
  - Script setup + composition API produce clean code
  - Performance is good
  - Best tooling I have used
- [[Core Team RFC] New SFC macro: defineModel](https://github.com/vuejs/rfcs/discussions/503)
- [useFetch triggers a request on the client side in nested components (using resolveComponent) #20476](https://github.com/nuxt/nuxt/issues/20476)
- [Vue - scoped style leak](https://github.com/vuejs/vue-loader/issues/957#issuecomment-329947476)

## nextTick

### [How to Use nextTick() in Vue](https://dmitripavlutin.com/vue-next-tick/)

If you don't supply the callback argument to Vue.nextTick() or this.$nextTick(): then the functions would return a promise that's being resolved when DOM is updated.  
Using this with an async/await syntax makes the code more readable than the callbacks approach.

```javascript
await this.$nextTick()
console.log(this.show, this.$refs.content)
```

### [How to wait for a browser re-render? Vue.nextTick doesn't seem to cover it, and setTimeout(..., 0) is not good enough.](https://github.com/vuejs/vue/issues/9200)

#### await this.$nextTick()

리포트 데이터를 테이블로 그리는 탭을 띄우고 바로 인쇄를 호출 했을 때, 테이블 내용이 모두 렌더링 되지 않은 상태에서 인쇄 상태로 전환됨.  
해서 DOM에 해당 데이터가 업데이트 됐는지 [cockatiel](https://github.com/connor4312/cockatiel)를 통해 polling으로 확인 후 nextTick으로 인쇄 시도 했는데 역시 렌더링이 완료 안된 상태로 진행 됨. DOM 적용과 rendering 시간차가 꽤 되는 듯

```javascript
this.$nextTick(window.print) // no rendering completed
```

위 code와 동일한 걸로 보이는 vue issue link에 나온 다음 code로는 잘 됨.

```javascript
await this.$nextTick()
window.print() // rendering completed
```

#### double `requestAnimationFrame`

다음 2 링크도 흥미로움.  
setTimeout 0은 안되고 25가 되는 이유.

- https://github.com/vuejs/vue/issues/9200#issuecomment-468503909
- https://github.com/vuejs/vue/issues/9200#issuecomment-468512304

## filter

### declare

```javascript
Vue.filter("USD", (value) => {
  if (typeof value !== "number") throw "value must be number"

  const formatter = new Intl.NumberFormat("en-IN", {
    style: "currency",
    currency: "USD",
    minimumFractionDigits: 2,
  })
  return formatter.format(value)
})
```

### use in template

```html
{{ price | USD}}
```

### use in javascript

```javascript
this.$options.filter.USD(this.price)
```
