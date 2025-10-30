# Explainer: Third-Party Cookie Allowlist Header

This proposal is an early design sketch to describe the problem below and solicit feedback on the proposed solution.
It has not been approved to ship in Chrome.

* [Discussion](https://github.com/explainers-by-googlers/third-party-cookie-allowlist-header/issues)

## Introduction

Websites may want to limit third-party origins from storing/reading cookies in certain circumstances including, but not limited to, pursuing compliance with local data protection and privacy laws.
If a website has limited control of third parties, it must currently trust representations made by them as to their compliance.
This can cause issues where third parties are layered (such as, an advertising service that has content served by another party) or compromised (such as when an imported script abuses access to perform disallowed actions).
Although third-party cookies are not the only storage vector for such cases, they are a key mechanism that many sites wish to make representations to their users or regulators about.

## Goals

* Allow the top-level site to provide an allowlist of origins which can access third-party cookies.
* Allow child frames to further restrict the list of origins which can access third-party cookies.
* When this allowlist is provided, deny access to third-party cookies to all other origins.
* Require consent of child-frames where specific lists (instead of none or all) will be enforced.


## Non-goals

* Override controls to allow access to third-party cookies where access would otherwise be denied.
* Change behaviors related to third-party cookies where the allowlist is not provided.
* Provide a mechanism to change the allowlist during the document’s lifecycle.
* Allow child-frames to escape parental restrictions through lack of participation.

## Use cases

### Website with cookie-related notice

A website has a notice that provides transparency about the third parties it works with for various purposes and it wants to limit the use of third-party cookies by any third-party not listed.
A website has a notice that asks for permission related to third-party cookies used by that website’s advertisers. If the user denies the use of third-party cookies, the website wants a way to prevent a given origin from accessing or setting them via a browser control. 

### Website with sensitive content

A website with sensitive content wants to prevent its users from being tracked by third-party resources it has to fetch/embed to function.
Third-party cookies are a key tracking vector, and controls related to them would improve user privacy (even if it does not guarantee it).
