---
id: rr1v0qgo9y5a4h5txghol3i
title: Event Delegation with Lokalised Anchor
desc: ""
updated: 1661841906093
created: 1661841830015
---

```vue
<template>
  <article @click="toPolicy">
    <a>개인 정보 처리 방침</a>을 참조
    <!-- a tag가 lokalise 내용에 포함 됨-->
  </article>
</template>

<script>
export default {
  methods: {
    toPolicy({ target }) {
      if (target.tagName.toLowerCase() != "a") return;
      this.$router.push("/policy/privacy");
    },
  },
};
</script>
```
