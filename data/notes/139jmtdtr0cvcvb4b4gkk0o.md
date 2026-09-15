
## Quick Setup

### Submodule로 추가

report sub directory로 추가

```sh
git submodule add https://github.com/genoplan/report-module-2023.git report
```

#### Submodule remove

```sh
git submodule deinit -f $module_dir
rm -rf .git/modules/$module_dir
git rm -f $module_dir
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
