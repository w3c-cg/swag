# Security Regulatory Guidance for Web Developers and Library Developers

## Purpose of this Document
This document provides actionable guidance for web developers and developers of web libraries or frameworks on how to understand and comply with emerging software security regulations and policy guidance. It focuses on topics such as vulnerability handling, secure defaults, supply chain security, and secure software lifecycle practices. It specifically excludes privacy-related topics, so this is not about privacy regulation such as GDPR.

Note that *this guide is not legal advice*; it’s just an overview to help you understand how regulatory and policy topics might apply to you. If you are looking for advice on your specific situation, please consult your own legal counsel or other detailed regulatory guidance documents.

## Scope and Audience

This guidance is for web developers producing web sites or software for deployment on the web or as packaged apps (e.g., PWAs, Electron) as well as developers of libraries, frameworks, or tools consumed by the web development ecosystem.

## Understanding the Security Regulatory Landscape

### European Union – Cyber Resilience Act (CRA)

Summary: The European CRA applies to manufacturers of "products with digital elements" (PDEs), including software that is placed on the EU market.

#### Relevance to Web Developers:

* The CRA is likely not directly applicable to general web sites or web apps deployed directly from a server.  The CRA excludes web sites that do not support a product's digital functionality.
* The CRA may apply if your web site or web app is integral to the function of a digital product - for example, if your web app is instrumental in controlling an IOT device.
* The CRA may apply if your web site or web app is integrated into a packaged application - for example, if your web app is converted into an Electron (or similar) app and put on the market as a desktop application, or of the web pages are built to execute within a web view that is displayed within a native app, then it would be considered a product under the CRA.
* The CRA most likely applies to your libraries, frameworks and tools that you sell or make available as part of a paid service to be used in other web sites. In this case your product is not the website which is not regualted by CRA but the software component placed on the market standalone as consumeable software product.
* Open source library developers, if they expect that their libraries may be used by those developing PDEs, should clearly state how to send vulnerability reports, and prepare to receive and respond to those security vulnerability reports. An OSS project does not have to have a "steward" under the CRA, but OSS developers of widely-used or important programs may want to identify and establish a steward for it.
* Open source library developers should have a a published security policy and should consider open our security guidelines for library and framework developers. This is because the CRA directs downstream users (particularly those classed as "manufacturers" of PDEs) to perform due dilligence on any open source component that they incorporate into their products.
* The OpenSSF have produced a [Brief Guide for Open Source Software (OSS) Developers](https://best.openssf.org/CRA-Brief-Guide-for-OSS-Developers) when it comes to understanding the  CRA.

### United States – CISA Secure by Design, US Executive Orders and Other Guidance

tba

### UK Software Security Code of Practice

tba

