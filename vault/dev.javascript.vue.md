---
id: p6jdsvhol2ebyzilnb5u3ot
title: Vue
desc: ""
updated: 1646816079337
created: 1646815969488
---

# [How to Use nextTick() in Vue](https://dmitripavlutin.com/vue-next-tick/)

If you don't supply the callback argument to Vue.nextTick() or this.$nextTick(): then the functions would return a promise that's being resolved when DOM is updated.  
Using this with an async/await syntax makes the code more readable than the callbacks approach.

```javascript
await this.$nextTick();
console.log(this.show, this.$refs.content);
```
