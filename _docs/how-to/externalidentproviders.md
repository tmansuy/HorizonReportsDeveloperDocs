---
layout: default
title: Using an Identity Provider (IdP) for SSO
nav_order: 15
parent: How To
---

Horizon Reports supports using an external identity provider for single sign-on (SSO) (e.g. Active Directory Federation Services or OpenID Connect). In addition, you can also enable support for third party identity providers via Google, Facebook, or Twitter social media accounts. Each of these authentication options can be configured by entering the appropriate information in the Configuration Settings section of the project.

# Active Directory Federation Services

To enable external authentication using Active Directory Federation Services, you need to specify the *ADFS Metadata address* and the *ADFS Realm*.

* *ADFS Metadata address*: A URL that points to the active directory instance to perform the authentication. For example, for the Horizon Reports domain: https://horizon-reports.local/FederationMetadata/2007-06/FederationMetadata.xml

* *ADFS Realm*: For the realm address, use the WS-Federation Passive protocol URL that was entered when configuring ADFS.

# OpenID Connect

To enable external authentication using OpenID Connect, you need to specify the *OpenID Authority*, the *OpenID ClientID* and the *OpenID ClientSecret*.

* *OpenID Authority*: A URL that points to the authentication server that supports the OpenID Connect protocol.

* *OpenID ClientID*: The ClientID value to send to the OpenID Connect authentication server.

* *OpenID ClientSecret*: The secret key value to send to the OpenID Connect authentication server.

# Facebook

To enable external authentication using Facebook, you need to specify the *Facebook AppID* and the *Facebook AppSecret*. Refer to the [developer documentation](https://developers.facebook.com/docs/) for details on creating an App that supports authentication.

# Google

To enable external authentication using Google, you need to specify the *Google ClientID* and the *Google ClientSecret*. To generate those values, navigate to [Integrating Google Sign-In into your web app](https://developers.google.com/identity/sign-in/web/sign-in#before_you_begin) and select CONFIGURE A PROJECT.

# Twitter

To enable external authentication using Twitter, you need to specify the *Twitter ConsumerKey* and the *Twitter ConsumerSecret*. To generate those values, navigate to [ https://apps.twitter.com/]( https://apps.twitter.com/) and create a new app for use with authentication.