# Security Guidelines for Framework & Library Developers

Similarly to our [Security guidelines for web application developers](./security_guidelines.md), we want the authors of frameworks and libraries that will be used as dependencies to be as careful as possible to not introduce potential vulnerabilities (or code that can be chained into a vulnerability when combined with user code).

We want to be more careful about the security standards in code here, due to the fact that their reach is not limited to just the single application being authored but potentially to thousands of applications across the ecosystem that use these as dependencies or less-visible transitive dependencies.

## Security Features

### Ensure compatibility for users to allow them to enforce a strict Content Security Policy (CSP)

A [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) helps mitigate cross-site scripting (XSS) and other code injection attacks by specifying which sources of content are trusted. For the best protection against many variants of XSS, we recommend an approach known as a [strict CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP#strict_csp), which uses a nonce or hash to restrict the scripts that can load.

This means that the code introduced to applications through your dependency cannot rely on features blocked by a strict CSP, such as:

- Inline event handlers
- `javascript:` URLs
- `eval()` calls

which must be refactored, as suggested in [this guide](https://web.dev/articles/strict-csp#refactor).

### Limit the use of potentially unsafe DOM APIs to minimize injection risk and ensure compatibility with Trusted Types

Using [unsafe DOM APIs](https://www.w3.org/TR/trusted-types/#dom-xss-injection-sinks) that can turn untrusted user strings into HTML markup executing on the page may lead to injection vulnerabilities, such as XSS.

Furthermore, if the user of your dependency wants to enforce [Trusted Types](https://web.dev/articles/trusted-types) as a defense against XSS, they will run into incompatibilities with using the [Trusted Types API](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API), since the [Trusted Types policies](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API#trusted_type_policies) have to be invoked at the site of assignment into the [injection sinks](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API#injection_sinks), which will be in the dependency's code rather than the application's code.

The recommendation is to

1. Refactor away any unnecessary calls to these unsafe DOM APIs if possible
2. Create your dependency's Trusted Types policy and clearly document the policy name, as in [this example](https://angular.dev/best-practices/security#enforcing-trusted-types).

### Publish your library with provenance using trusted builders

[Software attestations](https://slsa.dev/attestation-model) help protect against supply chain attacks. Since [NPM supports package provenance](https://github.blog/security/supply-chain-security/introducing-npm-package-provenance/), you can use [trusted builders](https://slsa.dev/blog/2023/05/bringing-improved-supply-chain-security-to-the-nodejs-ecosystem) to let your customers know that the package that they are importing has been built using the code in the repository using trusted builders.

## Security Practices

The following security practices apply just as they do for [our guidelines for web application developers](./security_guidelines.md).

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

- ### Use package managers such as NPM to automatically manage dependencies and enable updates

Package managers streamline the process of managing libraries and dependencies, ensuring that you can easily update to the latest versions, which often include important security patches.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Monitor known vulnerabilities in your web app's direct & indirect dependencies

Regularly checking for vulnerabilities in both direct and transitive dependencies helps you stay informed about potential security risks and take action to mitigate them. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Keep dependencies up to date

Keeping dependencies (i.e., libraries, polyfills, frameworks, etc.) up to date minimizes the risk of exploitation through known vulnerabilities. Regular updates should be part of your development lifecycle.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)

### Enforce a code review policy

Implementing a code review process helps catch potential security issues before they are merged into the main codebase, creating a culture of security awareness among developers.

- [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
