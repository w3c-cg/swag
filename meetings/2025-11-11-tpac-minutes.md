# SWAG TPAC 2025 Session

11 November 2025

Chaired: Florian Scholz and Dan Appelquist
Scribe: Will

Present: 18

Signed-up:
 Rakina Amni,   Daniel Appelquist,   Will Bamberg,  Giovanni Cerrato,   Serena Chen,   Michael Ficarra,  Chris Fredrickson,   Hiroshige Hayashizaki,  Dominique Hazaël-Massieux,   Johann Hofmann,   Brian Kardell,  Emily Lauber,   Justin Ridgewell,   Daniel Rubery,   Florian Scholz,  Tzviya Siegman,   Kouhei Ueno,   Anna Weine

https://www.w3.org/events/meetings/ca0be7c4-0d4a-4d67-b815-05accd660bec/

## Minutes

Dan: origin is: there's a gap between the security community and web developers. Tools are not being used especially by the long tail of web devs.

Florian: ran a survey to get an idea of the extent to which devs have problems with security. Launched SWAG CG. Presented at TPAC, made a plan to start writing. Now have some funding from the Sovereign Tech Agency (STA) to work on web platform security docs

Florian: we now have a section on MDN documenting common web sec attacks.

Florian: we've now moved on to document web authentication, cover the main authentication methods & the current reality for web devs. New tech (e.g. passkeys) is not already explained: when to use what and what is good practice.

Florian: we are funded by the STA until August 2026, and have plans to document threat models, keep contributing to SWAG guidelines, and privacy.

Dan: we also want to talk about the Cyber Resilience Act: general idea is: if you are developing a website, you don't need to care about the CRA. But this isn't always clear, e.g. a web app that's part of a system including embedded devices or libraries that might be used in such systems. We need to explore and explain this. - ref https://github.com/ossf/wg-globalcyberpolicy

Florian: that's the context for this discussion. We need the perspectives of the security experts in this room (and outside it). We want to know what we are missing. We are also running another survey soon to see how we are doing.

Will: we're looking for reviews and feedback from subject matter experts.

Mike Samuel: how should people volunteer?

Florian: join SWAG. We meet up weekly and often talk about docs we have in draft.

Florian: one question we got is, how are we different to OWASP? We are very hands on and try to be very practical. We are trying to look at it from the perspective of someone who's a web dev but not a security expert.

Vadim from MDN: one thing is to write docs and another is to make sure developers know about it.

Dan: use whatever channels we have. W3C's marketing channels, OpenSSF but that tends to be software security professionals. Part of the idea of using MDN is that this is where devs are anyway.

Florian: integrate links to our security docs from other docs, e.g. forms -> CSRF.

Estelle: standard "security considerations" for reference pages, linking to security docs. web devs need to know that they should be thinking about security.

Brian: we like to say "web developer" as if it is uniform and it isn't. For security you have to think about it from a few different personas. CSS, HTML, JS, web server setup. Need to tell people what they need to know.

Florian: need to give the right information to the right person. There is also some gatekeeping with security, web devs might feel it's not their problem/responsibility/are of expertise. We're somewhat trying to break these barriers.

Dan: trusted types cuts across boundaries. web developer needs to care about this but security expert might not because they are thinking of server setup. People who go through compsci might not be learning about security, or at least not the fundamental concepts.

Brian: [talking about different roles... different types of education that these roles have]
    
Will: one thing I want to do is to talk about : if you're doing X then you need to worry about a b and c... Etc... We do have that plan. But right now we're doing the foundation... E.g. "if you're dealing with user input then you need to think about XSS."

Brian: many things (layers) there too - like are you going to use an ad server... 

Camille: from google chrome security will you look at support for security policies in frameworks. e.g. a framework that does/doesn't support CSP.

Dan: SWAG has a separate "guidelines for FW devs". It's hard for MDN to document frameworks.

Estelle: we don't generally document FW on MDN, but if we document security on MDN, FW developers will understand how to integrate security features into their work.

Will: talking about frameworks on MDN is problematic because frameworks have their own docs, but we need to be pragmatic about it. In the XSS guide we do talk about frameworks and then point to their docs... I think we should be pragmatic ... if it's a helpful thing to do.

Aaron: The idea of compat is not necessarily binary... it's really like a spectrum... some frameworks do the bare minimum... some offer a fully packaged solution. some nuance and some subjectivity. Wanted to +1 to making sure we have docs published in this umbrella... and the ask to framework developers...

Florian: attacks stay more constant than defenses.

Dan" Q. for webappsec: there was a presentation about adoption of something (maybe CSP). Is there a feeling in this group about adoption of features that SWAG could help with. NB added by Dan later: I think this was actually the presentation I was talking about: [2023-09-14-TPAC-minutes.md](https://github.com/w3c/webappsec/blob/main/meetings/2023/2023-09-14-TPAC-minutes.md#deprecations-and-new-defaults)

Mike: Chromium tracks adoption at a not very granular level. Have been more focused on working with entities where users spend a lot of time (google properties) and making sure they have what they need. Would be great to reach a broader audience, and help ensure people get to know about new stuff.

Florian, in Docs CG we have a similar issue with web components: giant orgs can understand them, smaller ones can't.

Artur: we all care about sec features being used. with Web almanac, even the most popoular ones were low. Most websites don't have these protections. But most sites don't necessarily need these protections. So maybe we can redefine success: if they are available to people who need them, maybe that is good enough. And maybe frameworks will fill the gap for the rest. 

Florian: with prototype pollution, say, we need to understand what level of lockdown is actually practical for most people. 

Artur: we always say, wouldn't it be nice to have a header like "give me security" that turns on protections.

Camille: the platform often can't do much because compat is important. Depending on how much you are handling sensitive data, you might put more effort into this.

Will: we hope that the survey will help us understand more why people are or aren't using security features: because the don't know about them/don't understand them/can't deploy them/don't need them.

Brian: web almanac is not representative because it only looks at home pages.

Florian: there is research going on about adoption.

Mike: considering making changes to spec requirements. Would MDN writers like to see webappsec file issues or PRs on MDN when security specs change?

Florian: same issue came up with docs CG. So, yes.

Mike: one example is script-src-hash., a fairly small addition to the spec. How would we make this available to the right people?

Vadim: MDN wants more involvement from vendors, so yes.

Will: timing is tricky because we won't update the docs until something is shipping, and at that point the spec author will have moved onto something else.

Florian: MDN writers are not that deeply integrated into the WGs, can we be more involved? Especially while we are funded to do this work it is a good opportunity.

Carlos: it's currently an origin trial, how could we document it now?

Mike: WHATWG impose a req that the spec editor files a bug. This doesn't work that well because of timing. Can we look more into ways to collaborate?
