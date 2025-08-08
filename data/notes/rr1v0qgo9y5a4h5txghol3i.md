
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
