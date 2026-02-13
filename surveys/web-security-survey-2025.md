# SWAG Web Security survey 2025

The W3C Security Application Guidelines Community Group (SWAG CG) develops and publishes recommendations to help web developers secure their applications.

We wanted to understand whether web developers are using the features that we recommend, so in in 2025/2026 the W3C Security Application Guidelines Community Group (SWAG CG) ran a survey that asked web developers to tell us which features they used.

We asked for respondents through social media channels belonging to the W3C and individuals connected with SWAG CG. We had 108 responses in total.

## Responses

The questions we asked fall into two groups:

- A series of yes/no questions, asking whether developers used any of a number of features.
- A question asking which of a number of HTTP headers the respondent uses.

### Web security features

We asked web developers:

- Do you implement any mechanism to control whether third-party sites can embed your site as an iframe?
- When you set cookies that contain a user's login credentials (such as a session ID), do you set the SameSite attribute to "Lax" or "Strict", to control whether the cookie is included in cross-site requests?
- When you set cookies that contain sensitive user information (such as a session ID), do you set the Secure attribute to ensure they are only sent over an encrypted (HTTPS) connection?
- When you set cookies, do you use the HttpOnly attribute to prevent them from being accessed by client-side JavaScript?
- Do you use Fetch metadata to control whether certain cross-site requests are allowed?
- Do you use CSRF tokens in forms on your site?
- Do you use a Content-Security-Policy header on your site?
- Do you set the "integrity" attribute on scripts you load from a third-party site such as a CDN?
- Do you enforce the use of Trusted Types when passing input into JavaScript injection sinks such as innerHTML?

We've summarised the results in the following table:

![Bar chart showing the percentages of respondents using specific web security features.](charts/2025-survey-features.svg)

We see reasonable adoption of most features. Adoption of security-related cookie attributes is high, and adoption of CSP is higher than we expected at about 75%.

The least-used feature we asked about was trusted types, which saw only a little more than 25% adoption: perhaps this is not surprising as it has only recently gained cross-browser support.

The only other feature to be used by less than 50% of respondents was fetch metadata. Fetch metadata is an ergonomic and very useful API, and has been supported in most browsers for several years. However, until recently, documentation of it in both OWASP and MDN has been lacking: so we might speculate that lack of adoption results from a lack of awareness. Both sites now recommend fetch metadata as part of a defense against attacks like CSRF and cross-site leaks, so we might expect to see increased adoption in future.

### HTTP headers

We asked web developers which of the following HTTP headers they use:

- Http Strict Transport Security (HSTS)
- Referrer-Policy
- X-Content-Type-Options
- Content-Disposition
- Cross-Origin-Embedder-Policy (COEP)
- Cross-Origin-Opener-Policy (COOP)
- Cross-Origin-Resource-Policy (CORP)
- Permissions-Policy

We can summarise the results as follows:

![Bar chart showing the percentages of respondents using specific HTTP headers.](charts/2025-survey-headers.svg)

## Respondent characteristics

## Future work
