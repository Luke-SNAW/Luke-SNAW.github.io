---
id: pphqbd7v12fdv5ztfuv2dx7
title: Webpack
desc: ""
updated: 1663046463895
created: 1663046408488
---

# Webpack4, next.js - Cordova App lazy loading

```bash
yarn add webpack-assets-manifest
```

```js
// next.config.js
const WebpackAssetsManifest = require("webpack-assets-manifest");

module.exports = {
  webpack: (config, { buildId, dev, isServer, defaultLoaders, webpack }) => {
    // Note: we provide webpack above so you should not `require` it
    config.plugins.push(
      new WebpackAssetsManifest({
        sortManifest(a, b) {
          if (a[0] == "m") return -1;
          if (b[0] == "m") return 1;
          return b.localeCompare(a);
        },
      })
    );
    return config;
  },
};
```
