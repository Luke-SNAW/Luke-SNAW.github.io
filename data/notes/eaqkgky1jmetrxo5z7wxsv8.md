
## [Upcoming security changes to Google's OAuth 2.0 authorization endpoint in embedded webviews](https://developers.googleblog.com/2021/06/upcoming-security-changes-to-googles-oauth-2.0-authorization-endpoint.html)

The Google Identity team is continually working to improve Google Account security and create a safer and more secure experience for our users. As part of that work, we recently introduced a new [secure browser policy](https://developers.google.com/identity/protocols/oauth2/policies#browsers) prohibiting Google OAuth requests in embedded browser libraries commonly referred to as embedded webviews. All embedded webviews will be blocked starting on **September 30, 2021**.

Embedded webview libraries are problematic because they allow a nefarious developer to intercept and alter communications between Google and its users by acting as a "[man in the middle](https://wikipedia.org/wiki/Man-in-the-middle_attack)." An application embedding a webview can modify or intercept network requests, insert custom scripts that can potentially record every keystroke entered in a login form, access session cookies, or alter the content of the webpage. These libraries also allow the removal of key elements of a browser that hold user trust, such as the guarantee that the response originates from Google's servers, display of the website domain, and the ability to inspect the security of a connection. Additionally the [OAuth 2.0 for Native Apps](https://datatracker.ietf.org/doc/html/rfc8252#section-8.12) guidelines from IETF require that native apps must not use embedded user-agents such as webviews to perform authorization requests.

Embedded webviews not only affect account security, they could affect usability of your application. The sandboxed storage environment of an embedded webview disconnects a user from the single sign-on features they expect from Google. A full-featured web browser supports multiple tools to help a logged-out user quickly sign-in to their account including password managers and [Web Authentication](https://developer.mozilla.org/en-US/docs/Web/API/Web_Authentication_API) libraries. Google's users also expect multiple-step login processes, including [two-step verification](https://www.google.com/landing/2step/) and [child account authorizations](https://support.google.com/families/answer/9204736), to function seamlessly when a login flow involves multiple devices, when switching to another app on the device, or when communicating with peripherals such as a security key.

### [Instructions for impacted developers](https://developers.googleblog.com/2021/06/upcoming-security-changes-to-googles-oauth-2.0-authorization-endpoint.html#instructions)

Developers must register an appropriate OAuth client for each platform (Desktop, Android, iOS, etc.) on which your app will run, in compliance with [Google's OAuth 2.0 Policies](https://developers.google.com/identity/protocols/oauth2/policies#register). You can verify the OAuth client ID used by your installed application is the most appropriate choice for your platform by visiting the Google API Console's [Credentials page](https://console.developers.google.com/apis/credentials). A "Web application" client type in use by an Android application is an example of mismatched use. Reference our [OAuth 2.0 for Mobile & Desktop Apps](https://developers.google.com/identity/protocols/oauth2/native-app) guide to properly integrate the appropriate client for your app's platform.

---

## [Action Advised] Take action to continue using Google's OAuth authorization endpoint

Google Developers logo

Hello Google Developer,

We're writing to let you know that we detected the use of an embedded webview in requests to Google's OAuth 2.0 authorization endpoint in the past 120 days associated with one or more of your OAuth client IDs listed in this email.

Any affected authorization endpoint requests will be blocked with a `disallowed_useragent` error starting **July 24, 2023.** Affected requests to our authorization endpoint will display a [user-facing warning message](https://developers.googleblog.com/2021/06/upcoming-security-changes-to-googles-oauth-2.0-authorization-endpoint.html#warning-message) starting in May until **July 24, 2023**.

### What do you need to know?

Embedded webview libraries are highly customizable, which can expose Google's login and account authorization pages to potential "man-in-the-middle" attacks. [Google's OAuth 2.0 "Use secure browsers" policy](https://developers.google.com/identity/protocols/oauth2/policies#browsers) helps us protect users from these and other types of attacks.

Examples of affected embedded webview libraries include android.webkit.WebView on Android and WKWebView on iOS or macOS.
