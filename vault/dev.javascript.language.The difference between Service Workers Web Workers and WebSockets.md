---
id: mr8u5j3k25bxu8bsymkaapw
title: The difference between Service Workers Web Workers and WebSockets
desc: ""
updated: 1649036822831
created: 1649036786160
---

https://aarontgrogg.com/blog/2015/07/20/the-difference-between-service-workers-web-workers-and-websockets/

TL;DR

# Service Worker

Background service that handles network requests. Ideal for dealing with offline situations and background syncs or push notifications. Cannot directly interact with the DOM. Communication must go through the Service Worker’s `postMessage` method.

# Web Worker

Mimics multithreading, allowing intensive scripts to be run in the background so they do not block other scripts from running. Ideal for keeping your UI responsive while also performing processor-intensive functions. Cannot directly interact with the DOM. Communication must go through the Web Worker’s `postMessage` method.

# WebSocket

Creates an open connection between a client and a server, allowing persistent two-way communication over a single connection. Ideal for any situation where you currently use long-polling such as chat apps, online games, or sports tickers. Can directly interact with the DOM. Communication is handled through the WebSocket’s `send` method.
