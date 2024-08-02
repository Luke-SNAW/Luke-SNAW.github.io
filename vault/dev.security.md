---
id: NXAefr1pIXFjCcemglCJM
title: Security
desc: ""
updated: 1722558805037
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

## [A comprehensive guide to the dangers of Regular Expressions in JavaScript](https://www.sonarsource.com/blog/vulnerable-regular-expressions-javascript/)

This article explains how certain regex patterns can cause exponential backtracking on long strings, leading to regular expression denial of service (ReDoS) vulnerabilities.  
Two real world examples caused major outages at Stack Overflow and CloudFlare due to unintentionally vulnerable regex use.

The article details how issues like excessive use of wildcards, quantifiers and overlapping patterns can cause catastrophic backtracking.  
It also offers techniques for testing regex safety and fixing vulnerable patterns, such as limiting matches, using string methods instead of regex, and refactoring nested groups.  
Overall, the article effectively raises awareness of the ReDoS threat within seemingly benign regex code.
