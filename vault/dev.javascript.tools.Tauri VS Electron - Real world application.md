---
id: 8w8tob5febntlegn5raac8k
title: Tauri VS Electron - Real world application
desc: ""
updated: 1661212837183
created: 1661212149237
---

> https://www.levminer.com/blog/tauri-vs-electron

## 1. Bundle

We have a clear winner here: Tauri

The Tauri app installer is around ~2,5MB (!!!), while the Electron app installer is around ~85MB.

One major advantage that Tauri has: The app is compiled to a binary, which means you have to be an expert at reverse engineering to be able to de-compile the app. With Electron you can unpack the app with a simple [NPM command](https://medium.com/how-to-electron/how-to-get-source-code-of-any-electron-application-cbb5c7726c37).

And if your user has the correct runtime for the webview used by Tauri you can just send them a single executable, they don't have to install anything.

## 2. Startup time

This is not a scientific test but running the apps and timing the startup yields a clear winner:

- Tauri: ~ 2 seconds
- Electron: ~ 4 seconds

## 3. Performance

This is not a scientific test again, just a rough comparison. These tests are from my PC: i5-4570 CPU, 16GB RAM, GTX 1660 and Windows 11

Honestly I expected more from Tauri, sure it uses less RAM, but not by much. Let's take a look at what's up on the Linux side.

Tauri ![Tauri](https://cdn.levminer.com/blog/tauri-vs-electron/tauri-linux.png)

Electron ![Electron](https://cdn.levminer.com/blog/tauri-vs-electron/electron-linux.png)

Wow, thats a big win for Tauri!

## 4. App backend

Now here comes one of the disadvantages of Tauri (or its biggest advantage, I guess it depends on you). In your Electron app you write your app backend in JavaScript, because Electron uses the Node.js runtime. Tauri on the other hand is written in Rust. Now if you know Rust your probably happy, but if you have to learn Rust from scratch (like me) you are going to face some issues.

You have to rewrite your app's backend in Rust, so I think the winner in Electron here. For now. Alternative bindings for your backend are on Tauri's roadmap, like Python, C++, or Deno. Personally I'm excited for the Deno integration so I can write my app backend in JavaScript/TypeScript again.

## 5. Rendering your app

Electron uses Chromium under the hood so your user sees the same on Windows, Linux and macOS. Tauri on the other hand uses the system webview: Edge Webview2 (Chromium) on Windows, WebKitGTK on Linux and WebKit on macOS. Now here comes the bad part, if you are a web developer you know that Safari (Based on WebKit) is always behind a step from every web browser. Just check out [Can I Use](https://caniuse.com/). There is always a bug that you are not seeing from Chrome, only your dear Safari users. The same issues exists in Tauri, and you can't do anything against it, you have include polyfills. The winner has to be Electron here.

One issue I had while developing Tauri is that my CSS bundle didn't include `-webkit` prefixes, so my app's CSS was very buggy.

## 6. Security

Tauri is very secure by default, on the other hand I can't say the same about Electron. Tauri has many [security](https://tauri.app/about/security) features built-in by default. You can even explicitly enable or disable certain APIs. With Electron you have full access to Node APIs, so a hacker could easily exploit the very powerful Node APIs. This not the case with Tauri, you have to explicitly expose the Rust functions.

## 7. Auto update

> ![Auto update comic](https://imgs.xkcd.com/comics/update.png) xkcd.com

Shipping an app without auto update in 2022 is a no go. If your user has to manually download every update I don't think they are going to be happy. Both Electron and Tauri has a built-in auto updater, but the Tauri one is so much simpler. In Electron I think most people use [electron-updater](https://www.npmjs.com/package/electron-updater). In Tauri you can use the [built in](https://tauri.app/v1/guides/distribution/updater) one, the one downside is you have to maintain your own [update server](https://github.com/KilleenCode/tauri-update-cloudflare). Electron updater pulls the binaries form GitHub releases, which is way more convenient.

## 8. Developer experience

In Tauri you get the whole package just by installing the Tauri CLI: Hot reload, building your app for all platforms, generating app icons. Electron gives you nothing, just the framework itself. You have setup hot reloading, bundling your app etc... Tauri takes care of everything for you. And here comes the best: Tauri is compatible with every web framework on earth. It just expects a localhost url or a folder where all your bundled code lives.

## Summary

Electron is being replaced? Yes, Tauri is way better, but it still misses a lot. In a couple of years I'm sure the Tauri team will catch app to Electron. The things I'm excited for: Deno as the backend, better auto update and iOS/Android support.

---

> https://news.ycombinator.com/item?id=32550267

---

"With Electron you have full access to Node APIs, so a hacker could easily exploit the very powerful Node APIs."

This is not true, `nodeIntegration` has been disabled by default years ago in Electron 5.0 [^1]. The default in Electron 20 will be a sandboxed renderer process that can't even read files from disk [^2]. Security in Electron is great if you follow their security guidelines [^3].

[^1] https://www.electronjs.org/docs/latest/breaking-changes#planned-breaking-api-changes-50

[^2] https://www.electronjs.org/docs/latest/breaking-changes#planned-breaking-api-changes-200)

[^3] https://www.electronjs.org/docs/latest/tutorial/security)

---

A missing point of comparison is that Electron also has far more desktop APIs available. Electron also has support for some advanced primitives like BrowserViews which enable some very sophisticated use cases.

---

As I see it, the difference between the Tauri approach and Electron becomes visible when you have multiple apps running.  
Each Electron app will load its own browser back-end in RAM, while all tauri apps will share the same runtime on disk and in RAM.

This makes for quite a big difference as the number of running apps grows.

---

Tauri is more like Ionic or Cordova than Electron. You get a mostly web based developer experience, but without the browser matrix simplification so you're still at the whim of the system WebView capabilities for the view layer.  
The good news is the built in webviews have come a long way since webcompat is much better across browsers, but it's still extra things to worry about and can produce problems on old MacOS or Windows pre-11.

See also:

https://tauri.app/v1/guides/architecture/process-model

https://tauri.app/v1/api/js/

---

Using Tauri for my most recent project, I have to say the Development experience was phenomenal.  
Only downside that the article rightly points out us the knowledge of Rust, which was new to me.

Also Tauri has Android & iOS targets on its roadmap too.

---

I've evaluated both Tauri and Flutter + flutter_rust_bridge.  
I immediately felt really productive in Tauri/Svelte/rust. It just kind of clicked with me (completely new to Svelte, but been doing SPAs and JS desktop apps for some time as well as being in the rust scene for years). It was like the ease of electron, but with a better build framework for bundling rust. Really a good setup, easy to get into, easy and fast to build in.

I think Flutter is a really great UI framework. The way it's set up really makes sense and makes it fairly easy to structure the UI. That said, I really do not like Dart at all. I found it difficult to learn a new language and a new UI framework at the same time, and found myself pining for HTML/javascript again. flutter_rust_bridge obviously alleviated this a bit because it made it possible to move most of the logic into rust. I am honestly also worried about Flutter being a Google project. They tend to abandon projects quite a bit. I do like the promises of Flutter and didn't actually have any material issues with it. I think I might give it another go on the next app I build and see if I can get over the Dart hump.

---

One thing I don't see mentioned is the horror of shipping for Windows. You'll need Windows to have the Edge runtime, which means you have to bundle it or install it as an add-on. People will complain about this, especially IT people, because Edge runtime runs some kind of stupid background service all the time for no clear reason. It's also brittle since you will have to constantly keep your installer up to date with new releases of the Edge runtime or use a fragile MS URL that could stop working at any time and that won't work behind some firewalls.  
TL;DR: trying to use the native web view on Windows is horrible because there is no native web view and MS can't bundle software for their own platform.

Of course I suppose shipping any software for Windows is horrible...

> Tauri has options to take care of that.  
> Microsoft's WebView2 has three distribution options: the "evergreen bootstrapper," the "evengreen standalone installer," and "fixed version" (where you embed a browser version in your installer).  
> https://developer.microsoft.com/en-us/microsoft-edge/webview2/  
> Tauri supports all three of those mechanisms. If you choose to embed the browser directly in your installer, it adds 100MB+ to your installer size, but it's guaranteed to work anywhere. (They even support Windows 7.)  
> https://tauri.app/v1/guides/building/windows#webview2-installation-options
