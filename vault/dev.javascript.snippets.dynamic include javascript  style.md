---
id: sl745tz6bq8rs101g780c0h
title: "Dynamic Include JavaScript, Style"
desc: ""
updated: 1664154214939
created: 1646130423880
---

```javascript
export function includeJsOnce({ id, src }) {
  if (document.querySelector(`#${id}`)) return false;

  const script = document.createElement("script");
  script.id = id;
  script.type = "text/javascript";
  script.src = src;
  document.body.appendChild(script);
  return true;
}
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
