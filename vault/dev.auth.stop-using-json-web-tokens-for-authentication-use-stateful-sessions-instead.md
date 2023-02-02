---
id: 58ft2xcm0mjwn8eljaxgh82
title: Stop Using JSON Web Tokens For Authentication. Use Stateful Sessions Instead.
desc: ""
updated: 1675211453008
created: 1650632420814
---

https://betterprogramming.pub/stop-using-json-web-tokens-for-authentication-use-stateful-sessions-instead-c0a803931a5d

I'm tired of seeing the same tutorials pop up every couple of weeks.

- "JWTokens are the recommended auth method because of scalability."
- "JWTokens are easier to use."
- "JWTokens are stateless, so you don't use memory on the server."

I am sure their intentions are good, but they share an un-secure way of authenticating and authorizing users, at least for web applications.

However, please don't feel bad; I used JWT (incorrectly) when starting I was starting out because I didn't know any better.

## The Way JWT is usually implemented (in tutorials)

With that out of the way, let's go through the flow to authenticate users with JWT.

- **The user enters their username and password —** When the user clicks the sign-in button, a request is sent to the server to verify the user's credential with the database.
- **The server successfully authenticates the user** — The server now creates and signs a JWT using a secret password and returns it in the response.

Tutorials usually set the expiration to about one week to 30 days.

- **The Client Receives the JWT in the response** — The developer (in a client like chrome) receives it, applies some logic, and then stores it, usually in Local Storage.
- **The Client uses info stored in the Token to render conditionally** — Usually, tutorials use fields like a user's email, username, and boolean fields like `isAdmin`**.**
- **The Client Adds the Token as a header for every request** — If the Token exists in Local Storage, the user's session is active.

The server can now check the user's identity by decrypting the signed Token on every request.

The Token will be valid until it expires.

## Everything that's Wrong With Using JWT this way.

...

## Providing Scalability

I can't close this article without mentioning that scalability can become an issue with server-side sessions.

...
