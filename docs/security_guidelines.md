# Guidelines for developing more secure web applications

## Security features

This category lists web platform features that you can implement in a web application to help mitigate or respond to various attacks.

1. **Ensure your web application is designed to use encryption (HTTPS) by default for all network operations and ensure that the processes are in place to renew HTTPS certificates.**

   - Implementing HTTPS is crucial for securing data in transit. It protects against eavesdropping and man-in-the-middle attacks. Regularly renewing certificates ensures that your encryption remains valid and trusted.

2. **Employ a content security policy (CSP)**

   - A CSP helps mitigate cross-site scripting (XSS) and other code injection attacks by specifying which sources of content are trusted. Consistency between development and production environments reduces the risk of misconfigurations. It is recommended to use the same CSP in development and production to reduce complexity. [MDN Link](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) [OWASP Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)

3. **Implement effective monitoring and logging to detect and respond to security incidents.**

   - Monitoring and logging are essential for identifying suspicious activities and responding to incidents in a timely manner. This practice helps in forensic analysis and improving overall security posture. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

4. **Prevent injection attacks by validating and sanitizing user inputs.**

   - Input validation and sanitization are critical for preventing injection attacks, such as SQL injection and XSS. Ensuring that user inputs conform to expected formats helps mitigate these risks.

5. **Limit the use of third-party scripts and resources.**

   - Use _Subresource Integrity_ to ensure that third-party resources, like external scripts, haven't been tampered with. This adds an extra layer of protection against third-party script-based attacks. [MDN Link](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

6. **Validate and sanitize all server-side requests to prevent unauthorized access.**

   - Ensuring that all incoming requests are validated and sanitized helps protect against unauthorized access and various types of attacks, such as server-side request forgery (SSRF). [OWASP SSRF Cheatsheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html)

## Security practices

This category lists practices you can follow, which help reduce the risk of introducing security vulnerabilities into your web application, or help you respond to vulnerabilities.

1. **When selecting open source libraries, frameworks, build tools, or similar, take into account open source security best practices**

   - Evaluating open source components based on security metrics helps ensure that the libraries you use are actively maintained and have a good security track record, reducing potential vulnerabilities in your application. Consider the following [Scorecard](https://securityscorecards.dev) metrics: _tbd_

2. **Ensure all developers working on the project are using multi-factor authentication to access the source repository.**

   - Multi-factor authentication (MFA) adds an additional layer of security by requiring more than one form of verification, reducing the risk of unauthorized access to your codebase. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

3. **Have a documented security policy.**

   - Document (in a `SECURITY.md` file) your security policy, including how you want people to notify you of security issues. A clear security policy fosters transparency and encourages responsible disclosure of vulnerabilities, allowing you to address issues promptly and maintain user trust. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

4. **Perform a threat modeling exercise for your web application.**

   - Threat modeling helps identify potential security threats and vulnerabilities in your application architecture, enabling you to proactively address risks before they can be exploited. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software) [OWASP guide to threat modeling](https://owasp.org/www-community/Threat_Modeling)

5. **Use package managers such as NPM to automatically manage dependencies and enable updates.**

   - Package managers streamline the process of managing libraries and dependencies, ensuring that you can easily update to the latest versions, which often include important security patches. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

6. **Monitor known vulnerabilities in your web app's direct & indirect dependencies.**

   - Regularly checking for vulnerabilities in both direct and transitive dependencies helps you stay informed about potential security risks and take action to mitigate them. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

7. **Keep dependencies (i.e., libraries, polyfills, frameworks, etc.) reasonably up to date.**

   - Keeping dependencies up to date minimizes the risk of exploitation through known vulnerabilities. Regular updates should be part of your development lifecycle. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

8. **Do not push secrets (such as encrypted tokens or passwords) to a repository.**

   - Storing sensitive information in version control can lead to accidental exposure. Use environment variables or secret management tools to handle sensitive data securely. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

9. **Enforce a policy in your repository to review before accepting changes.**

   - Implementing a code review process helps catch potential security issues before they are merged into the main codebase, creating a culture of security awareness among developers. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

10. **Lock down your server coniguration**

    - Ensure that configuration files (e.g., web server, application) are not publicly accessible.
