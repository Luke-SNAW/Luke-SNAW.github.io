
> https://green.sapphi.red/blog/local-server-security-best-practices

## Attack Vectors

### [1. Overly Permissive CORS Settings​](https://green.sapphi.red/blog/local-server-security-best-practices#_1-overly-permissive-cors-settings)

Requests from external sites are usually blocked by the browser's SOP, either by preventing the request itself or blocking the reading of the response. However, this is not the case if the [`Access-Control-Allow-Origin` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Access-Control-Allow-Origin) is set to explicitly allow cross-origin requests. Utilizing resources from different "origins" this way is called [Cross-Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) (CORS). Many development servers were configured with `Access-Control-Allow-Origin: *`, which allows requests from all "origins."

Here are the specific attack steps:

1. An attacker serves a malicious site (e.g., http://malicious.example.com).
2. A user accesses a site that executes JavaScript served by the malicious site. This isn't limited to top-level navigation; it includes embedding via iframes or scripts on external sites.
3. The served JavaScript executes fetch('http://127.0.0.1:3000/main.js'), and the response content is sent to the attacker.
4. The attacker receives the contents of http://127.0.0.1:3000/main.js.

In the case of a development server, `main.js` is a transpiled file, but often the source code exists within that file or in `main.js.map`, allowing the original source code to be retrieved.

Related

- Vite: [`GHSA-vg6x-rcgg-rjx6` / `CVE-2025-24010`](https://github.com/vitejs/vite/security/advisories/GHSA-vg6x-rcgg-rjx6) (\[1\]: Permissive default CORS settings)
- parcel: [Fix PR](https://github.com/parcel-bundler/parcel/pull/10138)
- esbuild: [`GHSA-67mh-4wv8-2f99`](https://github.com/evanw/esbuild/security/advisories/GHSA-67mh-4wv8-2f99)
- Next.js: [`GHSA-3h52-269p-cp9r` / `CVE-2025-48068`](https://github.com/vercel/next.js/security/advisories/GHSA-3h52-269p-cp9r) (Allowed source maps with `Access-Control-Allow-Origin: *`, though not mentioned in the description)
- Nuxt: [`GHSA-2452-6xj8-jh47` / `CVE-2025-24360`](https://github.com/nuxt/nuxt/security/advisories/GHSA-2452-6xj8-jh47)

### [2. Using XSSI and Modifying the Prototype](https://green.sapphi.red/blog/local-server-security-best-practices#_2-using-xssi-and-modifying-the-prototype)

There are two types of scripts in the browser. One is the module script, which can use `import` and `export` statements and requires the `type=module` attribute when loaded via a `<script>` tag. The other is the classic script, which has been in use for a long time.

For historical reasons, the SOP does not apply when loading classic scripts via a `<script>` tag. This means that even without a CORS configuration, a script can be loaded from an external site. An attack that exploits this is called Cross-Site Script Inclusion (XSSI). To be clear, as mentioned earlier, fetching the script's content directly with `fetch` is blocked by SOP by default.

This becomes a problem for bundlers that output a bundle in classic scripts and in a format that allows the module list to be retrieved. For example, in Webpack, setting [`output.iife: false`](https://webpack.js.org/configuration/output/#outputiife) can expose the module list in a global variable like `window.webpackChunkSomething`.

...

Here are the specific attack steps:

1. An attacker serves a malicious site (e.g., `http://malicious.example.com`).
2. A user accesses the site. This includes top-level navigation as well as embedding via iframes.
3. The served JavaScript executes a script like the one shown above, and the result is sent to the attacker.
4. The attacker receives the contents of the module list.

Related

- webpack-dev-server: [`GHSA-4v9v-hfq4-rm2v` / `CVE-2025-30359`](https://github.com/webpack/webpack-dev-server/security/advisories/GHSA-4v9v-hfq4-rm2v)
- Next.js: [`GHSA-3h52-269p-cp9r` / `CVE-2025-48068`](https://github.com/vercel/next.js/security/advisories/GHSA-3h52-269p-cp9r) (One of the reasons why `allowedDevOrigins` is necessary)
- Nuxt: [`GHSA-4gf7-ff8x-hq99` / `CVE-2025-24361`](https://github.com/nuxt/nuxt/security/advisories/GHSA-4gf7-ff8x-hq99)

### [3. Using CSWSH​](https://green.sapphi.red/blog/local-server-security-best-practices#_3-using-cswsh)

Similar to classic scripts, WebSocket connections are not subject to SOP. Therefore, by default, connections from other sites are possible. An attack that exploits this is called Cross-Site WebSocket Hijacking (CSWSH).

Most bundlers don't send source code directly over WebSockets, so this vulnerability alone cannot retrieve useful information without being combined with other vulnerabilities. However, since Turbopack did send source code over WebSockets, this vulnerability alone made it possible to retrieve source code.

Here are the specific attack steps:

1. An attacker serves a malicious site (e.g., `http://malicious.example.com`).
2. A user accesses a site that executes JavaScript served from the malicious site. This includes top-level navigation as well as embedding via iframes or scripts on external sites.
3. The served JavaScript establishes a WebSocket connection.
4. The user edits a file, and the bundler sends the source code over the WebSocket.
5. The served JavaScript sends that source code to the attacker.
6. The attacker receives the source code.

Related

- Vite: [`GHSA-vg6x-rcgg-rjx6` / `CVE-2025-24010`](https://github.com/vitejs/vite/security/advisories/GHSA-vg6x-rcgg-rjx6)（\[2\]: Lack of validation on the Origin header for WebSocket connections）
- Vitest: [`GHSA-9crc-q9x8-hgqq` / `CVE-2025-24964`](https://github.com/vitest-dev/vitest/security/advisories/GHSA-9crc-q9x8-hgqq)
- parcel: [Fix PR](https://github.com/parcel-bundler/parcel/pull/10138)
- webpack-dev-server: [`GHSA-9jgg-88mc-972h` / `CVE-2025-30360`](https://github.com/webpack/webpack-dev-server/security/advisories/GHSA-9jgg-88mc-972h)
- Next.js: [`GHSA-3h52-269p-cp9r` / `CVE-2025-48068`](https://github.com/vercel/next.js/security/advisories/GHSA-3h52-269p-cp9r) (One of the reasons why `allowedDevOrigins` is necessary)

### [4. Using DNS Rebinding​](https://green.sapphi.red/blog/local-server-security-best-practices#_4-using-dns-rebinding)

One method for bypassing SOP is an attack known as DNS Rebinding. It works by changing the IP address a domain points to, allowing requests to be sent to a different IP address while being on the same "origin." If a server is vulnerable to this attack, it's possible to send requests from another site and receive responses, even if CORS is properly configured.

Here are the specific attack steps:

1. An attacker serves a malicious site (e.g., `http://malicious.example.com`) over HTTP.
2. A user accesses the site. This includes top-level navigation as well as embedding via iframes.
3. The attacker changes the domain's DNS record to point to `127.0.0.1` (or another private IP address).
4. The site's JavaScript sends a request with `fetch('http://malicious.example.com/main.js')`. This request is to the same "origin," but because the domain now resolves to `127.0.0.1`, it receives the same content as a request to `http://127.0.0.1/main.js`.
5. The site's JavaScript sends the result of the `fetch` to the attacker.
6. The attacker receives the contents of `main.js`.

Note that this attack does not work on HTTPS sites because the domain's certificate validation would fail. Therefore, today, this attack is mainly feasible against local servers.

Related

- Vite: [`GHSA-vg6x-rcgg-rjx6` / `CVE-2025-24010`](https://github.com/vitejs/vite/security/advisories/GHSA-vg6x-rcgg-rjx6)（\[3\]: Lack of validation on the Host header for HTTP requests）
- esbuild: [`GHSA-67mh-4wv8-2f99`](https://github.com/evanw/esbuild/security/advisories/GHSA-67mh-4wv8-2f99)
- parcel: [Fix PR](https://github.com/parcel-bundler/parcel/pull/10138)

## [Best Practices for Local Servers​](https://green.sapphi.red/blog/local-server-security-best-practices#best-practices-for-local-servers)

### [Properly Check the Request Origin​](https://green.sapphi.red/blog/local-server-security-best-practices#properly-check-the-request-origin)

Attack methods 1-3 all exploit insufficient checking of the request's origin.

For "1. Overly Permissive CORS Settings," it's crucial to recognize that an allowed "origin" can read the response. You should not set the `Access-Control-Allow-Origin` header casually; instead, you should properly configure it for trusted "origins" only.

For "2. Using XSSI and Prototype Pollution" and "3. Using CSWSH," it's important to be aware of the exceptions to SOP and perform appropriate checks.

For XSSI, you can use the [`Cross-Origin-Resource-Policy` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cross-Origin_Resource_Policy). Specifying this header can restrict the reading of responses from other "origins." However, be aware that the request itself will still reach the server. If operations with side effects like writing data are involved, you should check that the [`Sec-Fetch-Site` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Site) is not `cross-site` and reject the response before the side effect occurs.

For CSWSH, you can prevent it by validating the `Origin` header. A key point here is not to uniformly allow all IP addresses. While allowing all IP addresses is acceptable for "DNS Rebinding" for reasons explained later, for CSWSH, allowing all IPs would fail to prevent attacks from sites that can be served from an IP address ([`GHSA-9jgg-88mc-972h` / `CVE-2025-30360`](https://github.com/webpack/webpack-dev-server/security/advisories/GHSA-9jgg-88mc-972h)).

### [Properly Check the Request Target​](https://green.sapphi.red/blog/local-server-security-best-practices#properly-check-the-request-target)

"4. Using DNS Rebinding" exploits insufficient checking of the request's destination. Using HTTPS is ideal. However, this can be a burden for users of a development server, making it difficult to adopt. In that case, you should validate that the `Host` header belongs to your site. You may always allow a `Host` header that is an IP address. This is because DNS is not queried for IP address hosts, so DNS Rebinding cannot occur. If a middleware compatible with Node.js's [Connect](https://github.com/senchalabs/connect) is usable, you can use [`host-validation-middleware`](https://github.com/sapphi-red/host-validation-middleware), a library extracted from Vite that validates the `Host` header.

### [Bind to the Loopback Interface Only​](https://green.sapphi.red/blog/local-server-security-best-practices#bind-to-the-loopback-interface-only)

In Node.js's `server.listen`, if the `host` parameter is not specified, it accepts requests to all IP addresses that point to the machine. Therefore, unless blocked by a firewall, access from within the same network is possible. For example, a phone connected to the same Wi-Fi can access a server running on a PC by specifying the PC's Wi-Fi IP address (e.g., `192.168.0.5`). However, this also means that any device on that Wi-Fi can access the server. If not necessary, it's a good idea to specify a loopback interface like `127.0.0.1` or `::1` in the `host` parameter to prevent access from outside the machine itself. Since Vite v2.3, this has been the default, so no configuration is needed in Vite.
