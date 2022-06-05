---
id: 0yxxudkuzdpqhapvplegwxz
title: API Security Best Practices - curity
desc: ""
updated: 1654402046852
created: 1654401998926
---

https://curity.io/resources/learn/api-security-best-practices/

# Always Use a Gateway

# Always Use a Central OAuth Server

# Only Use JSON Web Tokens Internally

- [Phantom Token Approach](https://curity.io/resources/learn/phantom-token-pattern/)
- [Split Token Approach](https://curity.io/resources/learn/split-token-pattern/)
- Both involve an API Gateway in the process of translating an opaque token into a JWT.

# Use Scopes for Coarse-Grained Access Control

# Use Claims for Fine-Grained Access Control at the API Level

# Trust No One

# Create or Reuse Libraries for JWT Validation

# Do Not Mix Authentication Methods

# Protect All APIs

# Issue JWTs for Internal Clients Inside Your Network

# Use JSON Web Key Sets for Key Distribution

# Always Audit

# Manage Claims Centrally

# Abuse Doesn't Have to Be a Breach
