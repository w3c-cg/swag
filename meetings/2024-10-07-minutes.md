# SWAG Minutes - Mon 7 October 2024

Present: Dan, Oliver Dunk, Randall, Will, Simone, Okiki, Estelle, Aaron

## Intros

Oliver: Developer Relations Engineer working on Chrome Extensions as part of the Google Chrome team. Interested in general web security and also Chrome Extension security.

Dan: [opens issue 5](https://github.com/w3c-cg/swag/issues/5) on extensions

Will: also interested in extensions security...

Simone: on extensions ... at TPAC we worked on extensions and also manifest extensions... kind of a threat we need to think about...

Estelle: arguing we should have security concerns for all pages in the docs...

## Outcomes of TPAC

Minutes: https://www.w3.org/2024/09/25-mdn-security-minutes.html

Will: haven't cleaned up minutes yet... like estelle mentioned, the idea of having security considerations sections for non security features on MDN... Everyone thinks its a good idea... A bunch of talk about how it's possible to "find developers where they are" ... find ways to to be in their workflow...

Will: I could write something up about it... like for a blog post...

## New CSP guide on MDN

-> https://github.com/mdn/content/pull/36157

(this is just an announcement/request for reviewers)

Will: there is an open PR - I would appreciate some review comments.  Got some from Aaron already - appreciated.

## Document attacks on MDN?

- attacks are rather chaotically documented on MDN at present
- Should we have dedicated/organized pages on attacks? Which ones?
- XSS, clickjacking, Spectre/Meltdown, CSRF, MITM, ...?

Will: sort of documentation for attacks but . need more... also wasn't able to get a good understanding of e.g. spectre/meltdown out of MDN. That seems like a project.  

## Security Considerations for non-Security APIs in MDN

Dan: we could start collecting non-security related specs which should have security considerations sections - 

*will to open issue*

## First Draft Security Guidelines Doc

https://github.com/w3c-cg/swag/blob/main/docs/security_guidelines.md

Oliver: breaking it down by "type of web application"...  felt like it's jumping between types... Also jumping between things like server and front end code...

Dan: may think about about types... i think we could categorize between "front end code" and server config stuff...

Simone: thinking also about the awesome format that we can use for the lists https://github.com/topics/awesome

## Threat Modeling

Simone: we're going to start the Threat Modeling CG .. two models for now: one for digital credentials and Tom from WICG Digital Credentials started a model for AI attacks... I'm still working with him on that... 

Simone: In general, we can consider different type of threats, such as the one related to human rights... 

Simone: We received also a request from the threat model for the web, for SING. As we have different threat types, we have also different "level" such as the levels defined here https://arxiv.org/abs/2408.03578, e.g., they have - business level or environment level threats... useful for scoping.  We can think about things like credit cards... 

Simone: we could start creating a threats list by ourselves... 

Simone: for generic threat model this exists: https://www.threatmodelingmanifesto.org/

Dan: for our document we can refer to this... 

## OpenSSF SOSS Community Day

Dan: presents [slides given at SOSS Community day](https://docs.google.com/presentation/d/18iOsWdh_LG_gqUdSW7XfE5UOoB6_Zfi_B2XDDurPRUc/edit?usp=drive_link) 

## Outputs from WebAppSec at TPAC

Simone: Aaron's point - to make the web developers adopt CSP... integrtaing CSP into frameworks... this could be a collection point to knock on doors and push this point (with framework developers)

Aaron: depending on the framework there will be different levels of difficulty... Wordpress will be difficult. This is a good conversation to start.

Aaron: [to open issue]

Will: we tried opening up a CSP using netlify instructions and it completely failed... we think the netflify instructions might be in error...

Aaron: we might be able to help.



