---
id: 34ncx4gmwijqk4o1ds4egrx
title: 5 Software Security Goals All CTOs Should Prioritize
desc: ""
updated: 1673394583744
created: 1673394429346
---

> https://thenewstack.io/5-software-security-goals-all-ctos-should-prioritize/

Mitigations such as asking a third-party company to run penetration tests can help. This will identify vulnerabilities from the [OWASP Top Ten](https://owasp.org/www-project-top-ten/), such as weak backend endpoints exposed to the internet. Typically, though, penetration testing will only find a subset of issues. It is instead recommended to [defend in depth](https://thenewstack.io/container-defense-depth/), where software teams follow best practices for protecting against threats.

Correctly implementing security can also provide significant business benefits. A design with a good separation of concerns will perform well, keep the application security code simple and ensure that security behavior is easy to extend. It will also provide the best capabilities in areas like user [authentication](https://thenewstack.io/what-do-authentication-and-authorization-mean-in-zero-trust/) and connecting to business partners.

## **1. Applications Use Modern Security Standards**

These days the most powerful security option for modern applications is to use the [OAuth family of specifications](https://www.rfc-editor.org/rfc/rfc6749). These security standards map to company use cases. For each standard, the threats and mitigations have also been carefully vetted by many experts.

OAuth is used to secure mobile, web and API components. It is lightweight and scales well to large software platforms. It is also widely used to protect high-worth data by using stronger security profiles, such as those defined by the [Financial-grade API (FAPI)](https://openid.net/wg/fapi/) working group.

Your applications should then outsource the complex security to an identity and access management (IAM) system. This provides you with powerful options for [authenticating](https://thenewstack.io/how-do-authentication-and-authorization-differ/) users, protecting data using tokens and interoperating with business partners.

![](https://cdn.thenewstack.io/media/2022/12/3b482f0d-image1-e1671565511269.png)

The standards also provide blueprints for your engineers to follow to find more weaknesses early on. This includes using “scopes” and “claims” to verify early on that there is no [broken object-level authorization](https://owasp.org/www-project-api-security/), which is OWASP’s top API vulnerability.

Companies then need to choose an IAM solution. This is an important decision since you need to ensure the right business outcomes. A company might start with some technical investigations. Ultimately though, the decision-maker in selecting a product is usually the chief technology officer (CTO) or the head of architecture.

Yet there are subtleties to understanding the important requirements and making the most informed choice. I’ll therefore highlight other key behaviors a CTO should look for when planning a company’s next-generation security architecture.

## **2. A Secure Token Design That Protects APIs**

Ultimately, OAuth is about protecting data. Developers understand that an application redirects to the IAM system when a user needs to authenticate. Afterward, the app calls APIs with tokens. However, not all realize that the data used in tokens requires a careful design.

![](https://cdn.thenewstack.io/media/2022/12/279162c4-image4-e1671565550880.png)

The IAM system will store its own user account data, which becomes the source of truth for [personally identifiable information (PII)](https://curity.io/resources/learn/privacy-and-gdpr/). The IAM system can help you to manage other regulatory aspects, such as accepting terms or user privacy prompts. A zero trust architecture (ZTA) should be used to protect against both external and internal threats. This requires only simple code in APIs to verify a JWT access token on every request and apply business rules. For a summary of the behavior, see the “[Implementing Zero Trust APIs](https://curity.io/resources/learn/implementing-zero-trust-apis/)” article.

The IAM system must write secure values into tokens as “claims” that your APIs will later trust and use for authorization. Examples might be a user ID, email, tenant ID, role or subscription level. If some values are stored in the business data, the IAM system must be able to retrieve them. Meanwhile, internet clients should receive only confidential reference tokens.

![](https://cdn.thenewstack.io/media/2022/12/95ba7a64-image3-e1671565535582.png)

## **3. Users Authenticate in Many Ways, with a Single Identity**

An IAM system will enable your applications to run a simple [code flow](https://curity.io/resources/learn/oauth-code-flow/), after which you can configure many ways to authenticate users. One possible solution might use Azure Active Directory as the first factor of a multifactor authentication (MFA) flow. Supporting passwordless logins via WebAuthn, passkeys and wallets is also becoming essential for businesses.

Robust authentication will also require a data integrity design. Your business data will often have its own user concept, with business user IDs stored against business resources. But the system should avoid duplicating users in the identity or business data when they use different authentication methods. This is achieved with the following data picture type, called [account linking](https://curity.io/resources/learn/account-linking-recipes/). It requires high extensibility in the IAM system to handle all of your current and future authentication use cases.

![](https://cdn.thenewstack.io/media/2022/12/378ae237-image2-e1671565523150.png)

## **4. Engineering Teams Follow Security Best Practices**

OAuth is a complex framework and applying it is highly architectural. There is also a greater separation of concerns than in older architectures, with more components and endpoints. Some use cases, such as [web security](https://curity.io/product/token-service/oauth-for-web), are tricky to get right. Unfortunately, it is common to make expensive mistakes, which can delay time to market or affect future productivity. Since most architects and developers are not security experts, they need access to [detailed IAM online resources](https://curity.io/resources/).

Done well, OAuth only ever requires simple application code. Yet if architects follow suboptimal designs, or if the IAM system does not have the extensibility features needed, it is common to need to code complex workarounds at the application layer. This code then becomes challenging to manage and extend over time.

## **5. DevOps Teams Operate Production Systems Securely and Reliably**

Using an IAM system from a SaaS provider is sometimes seen as a safe choice, where the external party guarantees the high availability of the IAM system. Yet requirements from DevOps and InfoSec teams usually go beyond this. DevOps teams will need modern [logging and monitoring](https://curity.io/resources/logging-monitoring/) features, and InfoSec will need [auditing](https://curity.io/docs/idsvr/latest/system-admin-guide/audit-logging/index.html) of IAM events. Your IAM provider should also provide a support package with timely access to real product experts.

In production, the DevOps team will operate APIs, the API gateway and the IAM system, which are summarized in the [IAM primer](https://curity.io/resources/learn/iam-primer/). These components interact frequently, so it is most efficient if they are hosted next to each other inside your backend cluster. A cloud native approach works best and also enables teams to restrict endpoints exposed to the internet.

## **Conclusion**

Securing modern apps is possible via the OAuth framework, which provides state-of-the-art features for authenticating users and protecting data. Before committing to an IAM product, involve your technical staff in evaluations and ensure that you can achieve the following outcomes:

1. Applications that use modern security standards.
2. A secure token design that protects APIs.
3. Users can authenticate in many ways using a single identity.
4. Engineering teams follow security best practices.
5. DevOps operates production systems securely and reliably.

At Curity, we provide an [IAM product](https://curity.io/product/) and are passionate about remaining up-to-date with the ever-growing list of [OAuth security standards](https://curity.io/product/conformance/). We also ensure that our product is easily extensible to meet any use case.

We recognize that OAuth implementations are challenging for organizations and take time away from focusing on your own intricate business objectives. So in addition to an IAM product, we provide concrete designs to reduce uncertainty and accelerate end-to-end solutions.

The Curity approach involves a separation of concerns that externalizes your applications’ security plumbing. We also put significant effort into people-focused resources that support developers and DevOps along their journeys.
