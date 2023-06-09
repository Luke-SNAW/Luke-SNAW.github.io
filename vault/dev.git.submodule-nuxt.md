---
id: 139jmtdtr0cvcvb4b4gkk0o
title: Submodule Nuxt
desc: ""
updated: 1686211413850
created: 1686211366348
---

## Quick Setup

### Submodule로 추가

report sub directory로 추가

```sh
git submodule add https://github.com/genoplan/report-module-2023.git report
```

### Package install

[peerDependencies](/package.json) 참고하여 설치

### nuxt config에 components, composables 추가

```js
//nuxt.config.ts
export default defineNuxtConfig({
  components: ["~/components", "~/report/components"],
  imports: {
    dirs: ["./report/composables"],
  },
})
```

### Tailwind setting

```js
// tailwind.config.js
module.exports = {
  content: ["./report/components/**/*.{js,vue,ts}"],
}
```

### build action

```yaml
# build-deploy.yml
- name: Check out code
  uses: actions/checkout@master
  with:
    submodules: true
    token: ${{ secrets.REPO_READ_WRITE }} # private repo 일 경우
```
