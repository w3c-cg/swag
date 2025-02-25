CSRF guide# SWAG CG Minutes Doc - Mon 24 February 2025

Present: Dan, Simone, Lola, Will, AAron

## [CSRF guide review](https://pr38151.content.dev.mdn.mozit.cloud/en-US/docs/Web/Security/Attacks/CSRF#defense_summary_checklist)

Will: I wrote a page on CSRF for MDN... which had an editorial review and approval... But hasn't had a technical review from a security expert... 

https://github.com/mdn/content/pull/38151

... wanted to add a guideline about CSRF ... which motivated this .. that's the next thing. 

*Dan to send to OpenSSF folks for feedback*

*Will to draft a guideline about CSRF*-

Aaron: not that many technologies that deal with server-side HTTP headers... on NPM... 

## [Fetch Metadata Request headers](https://github.com/w3c-cg/swag/issues/13)

- has multiple browser implementations but is not a standard - can we try to standardise it? Simone: yes.

## Web App Sec notes

Permissions API update is incoming - will be moving to CR

https://www.linkedin.com/pulse/from-operation-aurora-apt29-web-browsers-killchain-simone-onofri-m063f/

Subresource integrity - for dynamic content - also coming soon

## Practical/accessible guide to threat modelling

(cf https://owasp.org/www-community/Threat_Modeling_Process which to me is not very accessible)

Simone: we are looking for editors... in SING... still thinking ...  General idea is to use the framework of "trust...?"  Challenge is - we see all the threat modeling framework guidelines are for .. systems .. not for specific tiny browser APIs...

Will: thinking about a guide on MDN for threat modeling for Web Applications.. the OWASP doc .. is not accessible.  Reads like "aimed at security professionals" - if you're a web developer looking for guidance... we need something more practical.  
* "if you're incorporating input into your pages, you need to think about XSS" 
* "if you have a form that chanegs state on the server then you need to care about CSRF" 
* "If you're using third party libraries then you need to think about SRI and supply chain attacks".

Simone: agree .. we could try to get an example which could cover 80% of the needs of the developer... Think about your application, think about threats... In theory, the approach of risk management. ISO 27001... Improbable that a web developer can do this .. so we need to lead by examples.

*need tracking issue*

## Planned "attacks" docs for MDN:

Will: working my way through docs on MDN... going to have one on CSRF soon... going to work through these things as we have time... 

Cross-site scripting (done)
Clickjacking (done)
CSRF (in review)

Cross-site leaks (CORP, COOP, COEP)
Supply-chain attacks
Man in the middle
SSRF
...more?

Lola: what resources are you using to inform what you write about this?

Will: OWASP a lot... a super good resource... foundation ... and I can build more accessible guides. For cross-site leaks, web.dev ... a lot of that is kind of "bloggy" - not reference docs.. I found portswigger has super good documentation... lots of good examples.. That kind of thing. Also people in this group!

## Libraries

Aaron: Will be working on more material similar to what's there...
