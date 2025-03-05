---
id: NXAefr1pIXFjCcemglCJM
title: Security
desc: ""
updated: 1741138396001
created: 1644825680750
---

## Collections

- [Risk-Based Authentication using Auth0 Actions and Have I Been Pwned APIs](https://javascript.plainenglish.io/risk-based-authentication-using-auth0-actions-and-have-i-been-pwned-apis-fd3cb65c040a)
- [SecurityZines](https://securityzines.com/) - graphical way of learning concepts of Application & Web Security.
- [JWT vs. Opaque Tokens](https://zitadel.com/blog/jwt-vs-opaque-tokens) - https://news.ycombinator.com/item?id=33018135
- [Chromium based browsers leak user local IP via WebRTC foundation attribute](https://niespodd.github.io/webrtc-local-ip-leak/)
  - https://news.ycombinator.com/item?id=33327678
    - This can be disabled in Brave by turning "WebRTC IP handling policy" to "Disable non-Proxied UDP" in "settings - > Privacy and Security".
    - WebRTC was already known to leak local IP. Which can be dangerous if you're behind a VPN.
- [PDF vulnerability](https://news.ycombinator.com/item?id=33732763)
  - [Dangerzone](https://github.com/freedomofpress/dangerzone) - Take potentially dangerous PDFs, office documents, or images and convert them to a safe PDF.
- [Password requirements: myths and madness](https://www.franzoni.eu/password-requirements-myths-madness/)
  - https://news.ycombinator.com/item?id=34098369
- [Web Hackers vs. The Auto Industry: Critical Vulnerabilities in Ferrari, BMW, Rolls Royce, Porsche, and More](https://samcurry.net/web-hackers-vs-the-auto-industry/)
- [RIP, Passwords. Here’s What’s Coming Next.](https://www.nytimes.com/wirecutter/blog/what-are-passkeys-and-how-they-can-replace-passwords/)
- [Oh-Auth - Abusing OAuth to take over millions of accounts](https://salt.security/blog/oh-auth-abusing-oauth-to-take-over-millions-of-accounts)
  > Not verifying access tokens as required by OAuth specifications allows an attacker to harvest credentials from a malicious site and hijack accounts on other trusted platforms.
- [Companies embracing SMS for account logins should be blamed for SIM-swap attacks](https://keydiscussions.com/2024/02/05/sim-swap-attacks-can-be-blamed-on-companies-embracing-sms-based-password-resets/)
- [Second Factor SMS: Worse Than Its Reputation](https://www.ccc.de/en/updates/2024/2fa-sms) - Attackers can intercept SMS one-time passwords through techniques like SIM swapping or exploiting SS7 network vulnerabilities.
- [Researchers: Weak Security Defaults Enabled Squarespace Domains Hijacks](https://krebsonsecurity.com/2024/07/researchers-weak-security-defaults-enabled-squarespace-domains-hijacks/) - "Wait, what if the user's email address isn't verified?"
- [Don’t Let Your Domain Name Become a “Sitting Duck”](https://krebsonsecurity.com/2024/07/dont-let-your-domain-name-become-a-sitting-duck/)
- [NIST will standardise prohibition of requirement of composing passwords from various character styles, and requirement for periodic password changes.](https://mastodon.social/@LukaszOlejnik/113193089731407165)
  - https://pages.nist.gov/800-63-4/sp800-63b.html#passwordver
- [ABC News hacks into popular robot vacuum, watches owner through camera](https://www.abc.net.au/news/2024-10-04/robot-vacuum-hacked-photos-camera-audio/104414020)
  - [Valetudo](https://github.com/Hypfer/Valetudo) is a cloud replacement for vacuum robots enabling local-only operation.
- [Attacking APIs using JSON Injection](https://danaepp.com/attacking-apis-using-json-injection)
  > This endpoint had no sanitization on the parameters throughout the processing of the JSON body. Moreover, the library Samsung relied on (json-c) was compiled with `JSON_TOKENER_STRICT=0`, which allows for defining strings with both single and double quotes.
  > You can [read a great writeup here](https://www.talosintelligence.com/vulnerability_reports/TALOS-2018-0556) from Cisco TALOS. This became [CVE-2018-3879](https://www.cvedetails.com/cve/CVE-2018-3879/), and when chained with [CVE-2018-3880](https://www.cvedetails.com/cve/CVE-2018-3880/), had a CVSS rating of 9.9.
  > JSON Injection → SQL Injection → Buffer Overflow → ROP = PWNED
- [Hundreds of code libraries posted to NPM try to install malware on dev machines](https://arstechnica.com/security/2024/11/javascript-developers-targeted-by-hundreds-of-malicious-code-libraries/)
  > The IP address returned by a package Phylum analyzed was: hxxp://193.233.201[.]21:3001.
  > While the method was likely intended to conceal the source of second-stage infections, it ironically had the effect of leaving a trail of previous addresses the attackers had used in the past.
  >
  > Attacks like this one rely on typosquatting, a term for the use of names that closely mimic those of legitimate packages but contain small differences, such as those that might occur if the package was inadvertently misspelled.
- [A phishing attack involving g.co, Google's URL shortener](https://gist.github.com/zachlatta/f86317493654b550c689dc6509973aa4)
- [Smuggling arbitrary data through an emoji](https://paulbutler.org/2025/smuggling-arbitrary-data-through-an-emoji/)
  - https://news.ycombinator.com/item?id=43023508, https://news.hada.io/topic?id=19199
  - Unicode 문자열을 수용하는 시스템에서 버퍼 오버플로우를 유발할 수 있음
  - LLM 출력 워터마킹에 이 기술을 사용하는 아이디어가 마음에 듦 - 99%의 복사 붙여넣기 생성기를 쉽게 잡아낼 수 있음

## [A comprehensive guide to the dangers of Regular Expressions in JavaScript](https://www.sonarsource.com/blog/vulnerable-regular-expressions-javascript/)

This article explains how certain regex patterns can cause exponential backtracking on long strings, leading to regular expression denial of service (ReDoS) vulnerabilities.  
Two real world examples caused major outages at Stack Overflow and CloudFlare due to unintentionally vulnerable regex use.

The article details how issues like excessive use of wildcards, quantifiers and overlapping patterns can cause catastrophic backtracking.  
It also offers techniques for testing regex safety and fixing vulnerable patterns, such as limiting matches, using string methods instead of regex, and refactoring nested groups.  
Overall, the article effectively raises awareness of the ReDoS threat within seemingly benign regex code.

## AI

- [Hacking Gemini's Memory with Prompt Injection and Delayed Tool Invocation](https://embracethered.com/blog/posts/2025/gemini-memory-persistence-prompt-injection/)
