---
id: if56gxwtype30agcqmyhn5m
title: Silly
desc: ""
updated: 1648079633811
created: 1648079618234
---

# [Why does JavaScript’s parseInt(0.0000005) print “5”?](https://javascript.plainenglish.io/why-is-javascripts-parseint-0-0000005-5-eb9e2432f1b0)

```javascript
String(0.000005); // => '0.000005'
String(0.0000005); // => '5e-7' pay attention here
parseInt("5e-7"); // 5
```
