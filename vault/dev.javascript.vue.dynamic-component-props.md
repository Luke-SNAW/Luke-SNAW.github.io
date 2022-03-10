---
id: 1fp5c6sls5ohtbharazsymx
title: Dynamic Component Props
desc: ""
updated: 1646895517114
created: 1646895517114
---

```vue
<Faq class="mt48 mt56d" :list="FAQS" :open-title-key="faqTitleKey" />
```

```javascript
const FAQS = [
  {
    titleKey: "family-negative",
    component: FaqContents,
    componentProps: { type: "negative" },
  },
  {
    titleKey: "family-positive-autosomal",
    component: FaqContents,
    componentProps: { type: "positive-autosomal" },
  },
  {
    titleKey: "family-positive-xlinked",
    component: FaqContents,
    componentProps: { type: "positive-xlinked" },
  },
];
```

```vue
<!-- FAQ component -->
<div v-for="item in list">
  <component :is="item.component" v-bind="item.componentProps" />
</div>
```

```javascript
// FAQ component
export default {
  props: {
    type: {
      type: "negative" | "positive-autosomal" | "positive-xlinked",
      required: true,
    },
  },
};
```
