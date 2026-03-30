---
id: lnueycdcbsdexl901il5npx
title: Privacy
desc: ""
updated: 1774850304647
created: 1646006125980
---

- [Google Fonts and GDPR](https://gomakethings.com/google-fonts-and-gdpr/): [A German court ruled that serving custom web fonts from Google Fonts violates GDPR](https://www.theregister.com/2022/01/31/website_fine_google_fonts_gdpr/), because it shares a visitors IP address with Google without their permission or consent.

---

## [ChatGPT won't let you type until Cloudflare reads your React state](https://www.buchodi.com/chatgpt-wont-let-you-type-until-cloudflare-reads-your-react-state-i-decrypted-the-program-that-does-it/)

The program collects 55 properties. No variation across 377 samples. All 55, every time, organized into three layers:

### Layer 1: Browser Fingerprint

**WebGL** (8 properties): `UNMASKED_VENDOR_WEBGL`, `UNMASKED_RENDERER_WEBGL`, `WEBGL_debug_renderer_info`, `getExtension`, `getParameter`, `getContext`, `canvas`, `webgl`

**Screen** (8): `colorDepth`, `pixelDepth`, `width`, `height`, `availWidth`, `availHeight`, `availLeft`, `availTop`

**Hardware** (5): `hardwareConcurrency`, `deviceMemory`, `maxTouchPoints`, `platform`, `vendor`

**Font measurement** (4): `fontFamily`, `fontSize`, `getBoundingClientRect`, `innerText`. Creates a hidden div, sets a font, measures rendered text dimensions, removes the element.

**DOM probing** (8): `createElement`, `appendChild`, `removeChild`, `div`, `style`, `position`, `visibility`, `ariaHidden`

**Storage** (5): `storage`, `quota`, `estimate`, `setItem`, `usage`. Also writes the fingerprint to `localStorage` under key `6f376b6560133c2c` for persistence across page loads.

### Layer 2: Cloudflare Network

**Edge headers** (5): `cfIpCity`, `cfIpLatitude`, `cfIpLongitude`, `cfConnectingIp`, `userRegion`

These are injected server-side by Cloudflare's edge. They exist only if the request passed through Cloudflare's network. A bot making direct requests to the origin server or running behind a non-Cloudflare proxy will produce missing or inconsistent values.

### Layer 3: Application State

**React internals** (3): `__reactRouterContext`, `loaderData`, `clientBootstrap`

This is the part that matters. `__reactRouterContext` is an internal data structure that React Router v6+ attaches to the DOM. `loaderData` contains the route loader results. `clientBootstrap` is specific to ChatGPT's SSR hydration.

These properties only exist if the ChatGPT React application has fully rendered and hydrated. A headless browser that loads the HTML but doesn't execute the JavaScript bundle won't have them. A bot framework that stubs out browser APIs but doesn't actually run React won't have them.

This is bot detection at the application layer, not the browser layer.
