---
id: utfpb5303hi2tjwtucpx4i9
title: font
desc: ""
updated: 1646130388803
created: 1646130321486
---

```javascript
export function injectStyles(rule, id) {
  $(`#${id}`).remove();
  const div = $("<div />", {
    html: `&shy;<style>${rule}</style>`,
  })
    .attr("id", id)
    .css("display", "none")
    .appendTo("body");
}
```

```javascript
import { injectStyles, getRemoteUrl } from "@/utils";

injectStyles(
  ` @font-face { font-family: 'Noto Sans'; font-weight: 700; src: local('Noto Sans Bold'), local('Noto Sans Bold'), url('${getRemoteUrl(
    "/static/fonts/NotoSans-Bold.woff"
  )}') format('woff'); }`
);
```