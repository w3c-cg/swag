# Guidelines for developing more secure web applications

## Security features

This category lists web platform features that you can implement in a web application to help mitigate or respond to various attacks.

### Use HTTPS

Ensure your web application is designed to use encryption (HTTPS) by default for all network operations and ensure that the processes are in place to renew HTTPS certificates.

Implementing HTTPS is crucial for securing data in transit. It protects against eavesdropping and man-in-the-middle attacks. Regularly renewing certificates ensures that your encryption remains valid and trusted.

### Implement a content security policy (CSP)

A CSP helps mitigate [cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS) and other code injection attacks by specifying which resources a document is allowed to load. A CSP can also help control whether a page can be embedded in another page, thus protecting against [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking), and can help ensure that all resources are loaded over HTTPS.

- To mitigate against XSS, we recommend that you implement a [strict CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#strict_csp), which uses a [nonce](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#nonces) or a [hash](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#hashes) to indicate to the browser which scripts it expects to see in the document. However, any CSP that prevents uncontrolled execution of inline scipts is much better than none.

- To enforce the use of trusted types, set the [`require-trusted-types-for`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/require-trusted-types-for) directive. See the [Validate and sanitize user input](#validate-and-sanitize-user-input) guideline.

- To defend against [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking), set the [`frame-ancestors`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) directive.

- To help ensure that all resources are loaded over HTTPS, set the [`upgrade-insecure-requests`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/upgrade-insecure-requests) directive. See the [Use HTTPS](#use-https) guideline.

#### See also

- [Content Security Policy guide](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) (MDN)
- [Content Security Policy Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) (OWASP)
- [Strict CSP guide](https://web.dev/articles/strict-csp) (web.dev)

### Implement monitoring and logging

Implement effective monitoring and logging to detect and respond to security incidents.

Monitoring and logging are essential for identifying suspicious activities and responding to incidents in a timely manner. This practice helps in forensic analysis and improving overall security posture.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Validate and sanitize user input

Input validation and sanitization are critical for preventing injection attacks, such as SQL injection and [cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS). Ensuring that user inputs conform to expected formats helps mitigate these risks.

To mitigate SQL injection attacks, use [prepared SQL statements with parameterized queries](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html). This ensures that the user input is treated as data rather than SQL commands.

To mitigate XSS attacks:

- When interpolating input into a page as text, use a reputable templating engine that performs input encoding, and understand the context in which you are interpolating input.
- When interpolating input as HTML, sanitize it using a reputable library such as [DOMPurify](https://github.com/cure53/DOMPurify). If you're rendering input in the client using DOM APIs like [`innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML), use the [Trusted Types API](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API) to ensure that input is being passed through a sanitization function.

#### See also

- [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html) (OWASP)
- [Cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS) (MDN)
- [Trusted Types guide](https://web.dev/articles/trusted-types) (web.dev)
- [Trusted Types API](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API) (MDN)

### Limit the use of third-party scripts and resources

Use _Subresource Integrity_ to ensure that third-party resources, like external scripts, haven't been tampered with. This adds an extra layer of protection against third-party script-based attacks.

- [MDN Link](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

### Validate and sanitize all server-side requests

Ensuring that all incoming requests are validated and sanitized helps protect against unauthorized access and various types of attacks, such as server-side request forgery (SSRF).

- [OWASP SSRF Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)

## Security practices

This category lists practices you can follow, which help reduce the risk of introducing security vulnerabilities into your web application, or help you respond to vulnerabilities.

### Evaluate the security metrics of open source libraries

When selecting open source libraries, frameworks, build tools, or similar, take into account open source security best practices.

This helps ensure that the libraries you use are actively maintained and have a good security track record, reducing potential vulnerabilities in your application. Consider the following [Scorecard](https://securityscorecards.dev) metrics: _tbd_

### Require multi-factor authentication for project developers

Ensure all developers working on the project are using multi-factor authentication (MFA) to access the source repository.

Multi-factor authentication adds an additional layer of security by requiring more than one form of verification, reducing the risk of unauthorized access to your codebase.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Have a documented security policy

Document (in a `SECURITY.md` file) your security policy, including how you want people to notify you of security issues. A clear security policy fosters transparency and encourages responsible disclosure of vulnerabilities, allowing you to address issues promptly and maintain user trust.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Perform a threat modeling exercise for your web application

Threat modeling helps identify potential security threats and vulnerabilities in your application architecture, enabling you to proactively address risks before they can be exploited.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

- [OWASP guide to threat modeling](https://owasp.org/www-community/Threat_Modeling)

### Use package managers such as NPM to automatically manage dependencies and enable updates

Package managers streamline the process of managing libraries and dependencies, ensuring that you can easily update to the latest versions, which often include important security patches.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Monitor known vulnerabilities in your web app's direct & indirect dependencies

Regularly checking for vulnerabilities in both direct and transitive dependencies helps you stay informed about potential security risks and take action to mitigate them. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Keep dependencies up to date

Keeping dependencies (i.e., libraries, polyfills, frameworks, etc.) up to date minimizes the risk of exploitation through known vulnerabilities. Regular updates should be part of your development lifecycle.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Do not push secrets to a repository

Storing sensitive information (such as encrypted tokens or passwords) in version control can lead to accidental exposure. Use environment variables or secret management tools to handle sensitive data securely.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Enforce a code review policy

Implementing a code review process helps catch potential security issues before they are merged into the main codebase, creating a culture of security awareness among developers.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Lock down your server configuration

Ensure that configuration files for your web server are not publicly accessible.
