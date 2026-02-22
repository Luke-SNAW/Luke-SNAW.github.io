
## [The Difference Between Web Sockets, Web Workers, and Service Workers](https://css-tricks.com/the-difference-between-web-sockets-web-workers-and-service-workers/)

### Web Socket

Establishes an open and persistent two-way connection between the browser and server to send and receive messages over a single connection triggered by events.

### Web Worker

Allows scripts to run in the background in separate threads to prevent scripts from blocking one another on the main thread.

### Service Worker

A type of Web Worker that creates a background service that acts middleware for handling network requests between the browser and server, even in offline situations.

## [The difference between Service Workers, Web Workers and WebSockets](https://aarontgrogg.com/blog/2015/07/20/the-difference-between-service-workers-web-workers-and-websockets/)

TL;DR

### WebSocket

Creates an open connection between a client and a server, allowing persistent two-way communication over a single connection. Ideal for any situation where you currently use long-polling such as chat apps, online games, or sports tickers. Can directly interact with the DOM. Communication is handled through the WebSocket’s `send` method.

### Web Worker

Mimics multithreading, allowing intensive scripts to be run in the background so they do not block other scripts from running. Ideal for keeping your UI responsive while also performing processor-intensive functions. Cannot directly interact with the DOM. Communication must go through the Web Worker’s `postMessage` method.

### Service Worker

Background service that handles network requests. Ideal for dealing with offline situations and background syncs or push notifications. Cannot directly interact with the DOM. Communication must go through the Service Worker’s `postMessage` method.
