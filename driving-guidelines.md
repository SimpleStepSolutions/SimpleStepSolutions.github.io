---
layout: page
title: Driving Guidelines
comments: false
---
## Shift-left security

* By architecting applications with "security" in mind from the outset (i.e. earlier in the development process), organizations save over 50% on security related issues after launch. 
* We build applications around a standalone OpenID Connect Identity Provider (e.g. Okta, Auth0, Keycloak, etc.). This helps standardize Identity and Access Management, keeps user details separate from the application(s), and allows new applications to be built along-side the old with relative ease. ([more reasons](https://jumpcloud.com/resources/why-it-should-always-start-with-the-identity-provider/)?)

## Best-practice security
* We outshine the average developer with respect to security and Identity and Access Management as we engage with other security leaders on standards and best practice
* We use the authorization code flow for all user authentication. This way we follow best practice and never collect user credentials in the application itself. 
* We avoid using OAuth2 public clients (those that cannot keep a secret secure) if confidential clients are reasonably possible. If we use public clients, we must take extra precautions to protect tokens and use PKCE.

## Open-source community participation
* We use and contribute to open source technologies; specializing in

    | <img style="height:40px;box-shadow:none" src="assets/images/spring.svg"/> | | Java, Spring Boot, Spring Security, JPA |
    | <img style="height:40px;box-shadow:none" src="assets/images/reactjs.svg"/> | | React/Redux | 
    | <img style="height:40px;box-shadow:none" src="assets/images/postgresql.svg"/> | | PostgreSQL | 
    | <img style="height:40px;box-shadow:none" src="assets/images/oauth.svg"/> | | OpenID Connect/OAuth2 | 
    | <img style="height:40px;box-shadow:none" src="assets/images/docker.svg"/> | | Docker | 
    | <img style="height:20px;box-shadow:none" src="assets/images/logo-jhipster.svg"/> | | JHipster| 
    | <img style="height:40px;box-shadow:none" src="assets/images/kubernetes.svg"/> | | Kubernetes, GKE, etc. | 
    | <img style="height:40px;box-shadow:none" src="assets/images/jenkinsx2.svg"/> | | CI/CD (including Jenkins X)| 

<div id="accelerate"></div>
## Evidence-based approach to accelerating software delivery performance

> **"high IT performance correlates with strong business performance"** ~ <a target="_blank" href="https://www.amazon.ca/gp/product/1942788339/ref=as_li_tl?ie=UTF8&camp=15121&creative=330641&creativeASIN=1942788339&linkCode=as2&tag=simplestep-20&linkId=c5ea844cf2723322ce55b863411b91c3">Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations</a><img src="//ir-ca.amazon-adsystem.com/e/ir?t=simplestep-20&l=am2&o=15&a=1942788339" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />

* We follow an evidence-based approach to software delivery performance that has been shown to correlate to strong business performance regardless of organizational size or industry. Research shows that there are certain capabilities that drive improvements in software delivery performance – so we help organizations accelerate their business by focusing on these categories of capabilities:
    * **Continuous Delivery**
    <a align="right" target="_blank"  href="https://www.amazon.ca/gp/product/1942788339/ref=as_li_tl?ie=UTF8&camp=15121&creative=330641&creativeASIN=1942788339&linkCode=as2&tag=simplestep-20&linkId=6a06d8e9aed4924d8cd7ba3f7fc1f15c"><img align="right" border="0" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&MarketPlace=CA&ASIN=1942788339&ServiceVersion=20070822&ID=AsinImage&WS=1&Format=_SL160_&tag=simplestep-20" ></a><img align="right" src="//ir-ca.amazon-adsystem.com/e/ir?t=simplestep-20&l=am2&o=15&a=1942788339" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
    * **Architecture**
    * **Product and process**
    * **Lean management and monitoring**
    * **Cultural**
* We use GitOps so that what is deployed (code and infrastructure) are declarative and version controlled.
* We do Continuous Integration and Continuous Deployment; deploying and releasing even the first commit if all tests pass






