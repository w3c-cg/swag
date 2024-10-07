# Guidelines for Developing More Secure Web Applications

## A Draft Document from the W3C SWAG Community Group

1. Ensure your web application is designed to use encryption (https) by default for all network operations and ensure that the processes are in place to renew https certificates.
2. Employ a content security policy (CSP), employing the following CSP best practices: [tbd]
3. When selecting open source libraries, frameworks, build tools or similar, take into account open source security best practices - e.g. consider the following Scorecard metrics: [tbd]
4. Ensure all developers working on the project are using multi-factor authentication to access the soruce repository. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
5. Use package managers such as NPM to automatically manage dependencies and enable updates. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
6. Monitor known vulnerabilities in your web app's direct & indirect dependencies. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
7. Keep dependencies (i.e. libraries, polifills, frameworks, etc...) reasonably up to date. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
8. Do not push secrets (such as encrypted tokens or passwords) to a repository. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
9. Enfore a policy in your repo to review bfore accepting changes. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
10. Have a documented security policy including how you want people to notify you of security issues in your application (in a `SECURITY.md` file). [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
11. Perform a threat modeling excercie for your web application. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software) [OWASP guidelines link needed]
12. Implemented effective monitoring and logging to detect and respond to security incidents. [openssf concise guide](https://best.openssf.org/Concise-Guide-for-Developing-More-Secure-Software)
13. Prevent injection attacks by validating and santizing user inputs.
14. [Something about security configuration on the server side.]
15. Validate and sanitize all server-side requests to [prevent unauthorized access](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html).
