
> https://kevincox.ca/2024/08/24/cors/

## Summary by Universal Summarizer of Kagi

- CORS (Cross-Origin Resource Sharing) and the same-origin policy are often conflated, as they work together to manage cross-origin resource access.
- CORS was developed as a workaround for security vulnerabilities but is fundamentally flawed, as it does not adequately prevent cross-site request forgery (XSRF) attacks.
- Implicit credentials in web browsers can lead to security risks, allowing malicious sites to make unauthorized requests using a user's credentials (e.g., cookies).
- The default CORS policy allows requests but prevents reading results, which does not fully protect against certain types of attacks, such as unauthorized fund transfers.
- The recommended approach to secure applications is to ignore implicit credentials for cross-origin requests and only allow explicit credentials through controlled exceptions.
- Utilizing explicit credentials, such as API tokens or OAuth tokens in the Authorization header, can effectively mitigate XSRF risks and support multi-account functionality.
- Setting the SameSite attribute on cookies to 'Lax' or 'Strict' can help prevent cookies from being sent with cross-origin requests, enhancing security.
- A simple CORS policy allowing anonymous requests can protect against unauthorized access while still permitting necessary functionality.
- Developers should be cautious about creating overly specific CORS policies, as they may inadvertently introduce new vulnerabilities or hinder legitimate use cases.
- The web's security model is hindered by legacy decisions, but there are ongoing efforts by browser developers to enhance user privacy and security, albeit in an uncoordinated manner.
