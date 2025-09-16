# Guidelines for developing more secure web applications

## Security features

This category lists web platform features that you can implement in a web application to help mitigate or respond to various attacks.

### Use HTTPS

Ensure your web application uses [HTTPS](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS) (HTTP over [TLS](https://developer.mozilla.org/en-US/docs/Glossary/TLS)) for all its pages and other resources that it loads. Implementing HTTPS is crucial for securing data in transit. It protects against eavesdropping and man-in-the-middle attacks.

To support HTTPS a web application needs a TLS certificate. [Let's Encrypt](https://letsencrypt.org/) is a widely used nonprofit Certification Authority which issues free TLS certificates.

Not all TLS configurations are equally secure: if you need to configure your own server, consult a resource such as Mozilla's [TLS Recommended Configurations](https://wiki.mozilla.org/Security/Server_Side_TLS#Recommended_configurations).

Modern web hosting services support HTTPS for you, either by default or through a configuration setting. In this situation, the hosting service is likely to manage your certificate and configure the server on your behalf.

You should serve all pages over HTTPS, not just pages that you consider especially sensitive.

When a page loads resources (scripts, stylesheets, fonts, images, and so on), these resources should also be served over HTTPS. If a page is loaded over HTTPS and it attempts to load resources over HTTP, then the browser will either try to upgrade the load request to use HTTPS or will block the request: this is called [mixed content blocking](https://developer.mozilla.org/en-US/docs/Web/Security/Mixed_content).

If it's not possible for you to update your code to load resources from HTTPS URLs (for example, because your HTML has been archived) you can include a [content security policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) that contains the [`upgrade-insecure-requests`](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#upgrading_insecure_requests) directive, and the browser will automatically upgrade these requests to HTTPS.

To support clients which request pages over HTTP, you can listen for HTTP requests and use a [301 Moved Permanently](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/301) response to redirect to the HTTPS version. If you do this, then you should also send the [HTTP `Strict-Transport-Security`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security) (HSTS) response header: this informs clients that you wish them to use HTTPS, and will cause the browser to connect using HTTPS directly for any subsequent visits, even those made using HTTP URLs.

#### Learn more

- [Let's Encrypt](https://letsencrypt.org/)
- [TLS Recommended Configurations](https://wiki.mozilla.org/Security/Server_Side_TLS#Recommended_configurations) (Mozilla)
- [Transport Layer Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html) (OWASP)
- [HTTP Strict Transport Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html) (OWASP)
- [Strict-Transport-Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security) (MDN)

### Implement a content security policy (CSP)

A CSP helps mitigate [cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS) and other code injection attacks by specifying which resources a document is allowed to load. A CSP can also help control whether a page can be embedded in another page, thus protecting against [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking), and can help ensure that all resources are loaded over HTTPS.

- To mitigate against XSS, we recommend that you implement a [strict CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#strict_csp), which uses a [nonce](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#nonces) or a [hash](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#hashes) to indicate to the browser which scripts it expects to see in the document. However, any CSP that prevents uncontrolled execution of inline scipts is much better than none.

- To enforce the use of trusted types, set the [`require-trusted-types-for`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/require-trusted-types-for) directive. See the [Validate and sanitize user input](#validate-and-sanitize-user-input) guideline.

- To defend against [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking), set the [`frame-ancestors`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) directive.

- To help ensure that all resources are loaded over HTTPS, set the [`upgrade-insecure-requests`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/upgrade-insecure-requests) directive. See the [Use HTTPS](#use-https) guideline.

#### Learn more

- [Content Security Policy guide](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) (MDN)
- [Content Security Policy Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) (OWASP)
- [Strict CSP guide](https://web.dev/articles/strict-csp) (web.dev)

### Set the SameSite attribute on sensitive cookies

The [`SameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) cookie attribute is a defense in depth against a variety of attacks, including [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking), [CSRF](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF) and various [cross-site leaks](https://xsleaks.dev/). It takes one of three values: `Strict`, `Lax`, or `None`.

The strictest value is `Strict`, which prevents the cookie from being included in any cross-site requests: that is, any requests which originate from a different [site](https://developer.mozilla.org/en-US/docs/Glossary/Site) from the site that set the cookie.

However, this will prevent the cookie being included in some cross-site requests for which you might want it. For example, if the user is logged into your site, and the user then clicks a link to your site from a different site, you probably want to show the logged-in version of your page, and for this to happen the request must include the user's cookie.

The `Lax` value is intended to allow for this use case, but offers correspondingly weaker protection against cross-site attacks.

As a general guide, then, you should try to use `Strict` for some cookies and `Lax` for others:

- `Lax` for cookies that you will use to decide if a logged-in user should be shown a page
- `Strict` for cookies that you will use to authorize requests that change the server's state, such as transferring money or changing the user's settings.

Note that `Lax` is the default value in some but not all browsers, and in those browsers, the implementation of `Lax` when it is the default is more permissive than the normal implementation of `Lax`. This means that you should actively set `Lax`, and not rely on it being the default.

#### Learn more

- [`SameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) (MDN)
- [SameSite cookies explained](https://web.dev/articles/samesite-cookies-explained) (web.dev)
- [Bypassing SameSite cookie restrictions](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions) (PortSwigger)

### Use Fetch metadata to defend against cross-site attacks

Many attacks, including [CSRF](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF) and some [cross-site leaks](https://xsleaks.dev/), depend on an attacker's site making an HTTP request to the target site: that is, making a cross-site request.

Fetch metadata headers are a collection of HTTP request headers which provide information about the context of an HTTP request. Fetch metadata headers include:

- [`Sec-Fetch-Site`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Site): Whether the request is same-origin, same-site, or cross-site.
- [`Sec-Fetch-Mode`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Mode): The request's [`mode`](https://developer.mozilla.org/en-US/docs/Web/API/Request/mode).
- [`Sec-Fetch-User`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-User): Whether the request is a user-initiated navigation.
- [`Sec-Fetch-Dest`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Sec-Fetch-Dest): The request's [`destination`](https://developer.mozilla.org/en-US/docs/Web/API/Request/destination).

When handling a request, a server can examine these headers, and use them to reject certain cross-site requests, and so defend against the corresponding attacks.

To protect against CSRF attacks, you should understand where your site is implementing HTTP requests that change the server's state in a significant way (for example, transferring the user's money), and should consider using Fetch metadata headers to prevent these requests from being made cross-site.

To protect against certain cross-site leaks, you should decide whether you need other sites to be able to load your site's resources, and either block cross-site loads entirely or only allow them for allowlisted sites. This is called a _Resource Isolation Policy_.

#### Learn more

- [Defend against CSRF using Fetch metadata](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/CSRF#fetch_metadata) (MDN)
- [Protect your resources from web attacks with Fetch Metadata](https://web.dev/articles/fetch-metadata) (web.dev)
- [Isolation Policies](https://xsleaks.dev/docs/defenses/isolation-policies/) (xsleaks.dev)

### Implement monitoring and logging

Implement effective monitoring and logging to detect and respond to security incidents.

Monitoring and logging are essential for identifying suspicious activities and responding to incidents in a timely manner. This practice helps in forensic analysis and improving overall security posture.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Validate and sanitize user input

Input validation and sanitization are critical for preventing injection attacks, such as SQL injection and [cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS). Ensuring that user inputs conform to expected formats helps mitigate these risks.

To mitigate SQL injection attacks, use [prepared SQL statements with parameterized queries](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html). This ensures that the user input is treated as data rather than SQL commands.

To mitigate XSS attacks:

- When interpolating input into a page as text, use a reputable templating engine that performs input encoding, and understand the context in which you are interpolating input.
- When interpolating input as HTML, sanitize it using a reputable library such as [DOMPurify](https://github.com/cure53/DOMPurify). If you're rendering input in the client using DOM APIs like [`innerHTML`](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML), use the [Trusted Types API](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API) along with the [`require-trusted-types-for`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/require-trusted-types-for) CSP directive, to ensure that input is being passed through a sanitization function.

#### Learn more

- [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html) (OWASP)
- [Cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/XSS) (MDN)
- [Trusted Types guide](https://web.dev/articles/trusted-types) (web.dev)
- [Trusted Types API](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API) (MDN)

### Implement restrictions on framing

Controlling whether your site can be embedded in another site using an [`<iframe>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) can help protect against [clickjacking](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/Clickjacking) and certain [cross-site leak attacks](https://xsleaks.dev/).

Implement framing protection using the [`frame-ancestors`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy/frame-ancestors) CSP directive and the [`X-Frame-Options`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-Frame-Options) HTTP response header. If you need your site to be embeddable by specific sites, you can list them in `frame-ancestors`: restrict the configuration as much as possible, to reduce your risk.

The `frame-ancestors` directive offers more fine-grained control than `X-Frame-Options`, allowing you to list sites that are allowed to embed your site. However, [`frame-ancestors` is not supported in obsolete browsers, notably Internet Explorer](https://caniuse.com/mdn-http_headers_content-security-policy_frame-ancestors). When both methods are included, browsers that support `frame-ancestors` will ignore `X-Frame-Options`, so it is best to include both methods.

#### Learn more

- [Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html) (OWASP)
- [Framing Protections](https://xsleaks.dev/docs/defenses/opt-in/xfo/) (XS-Leaks Wiki)

### Limit the use of third-party scripts and resources

Use _Subresource Integrity_ to ensure that third-party resources, like external scripts, haven't been tampered with. This adds an extra layer of protection against third-party script-based attacks.

- [MDN Link](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

### Validate and sanitize all server-side requests

Servers that make network requests on behalf of clients are potentially vulnerable to [Server-Side Request Forgery (SSRF)](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/SSRF) attacks.

To mitigate this:

- Implement URL validation:
  - Ensure that the server can only make requests to the URLs you expect.
  - If possible, ensure that the server can only make HTTPS requests (and especially not other schemes such as `file:`).
  - Ensure that URL redirects can't be used as a mechanism to evade URL validation.
- Restrict the public-facing server's network access as far as possible: especially, restrict the server's access to any internal networks.
- Log and monitor requests that the server makes.

#### Learn more

- [Server-Side Request Forgery Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) (OWASP)
- [SSRF](https://developer.mozilla.org/en-US/docs/Web/Security/Attacks/SSRF) (MDN)

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
