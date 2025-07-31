---
layout: default
title: Using an Identity Provider (IdP) for SSO
nav_order: 15
parent: How To
---

Horizon Reports supports using an external identity provider for single sign-on (SSO) (e.g. Active Directory Federation Services or OpenID Connect). In addition, you can also enable support for third party identity providers via Google, Facebook, or Twitter social media accounts. Each of these authentication options can be configured by entering the appropriate information in the Configuration Settings section of the project.


> <span class="glyphicon glyphicon-info-sign" aria-hidden="true"></span> After changing any of these settings, you'll need to restart the application before they take effect. If you find that you're unable to login after a setting change, launch Horizon Reports locally with HRWeb.exe and pass clearauthsettings=true as a command line argument.


# Active Directory Federation Services

To enable external authentication using Active Directory Federation Services, you need to specify the *ADFS Metadata address* and the *ADFS Realm*.

* *ADFS Metadata address*: A URL that points to the active directory instance to perform the authentication. For example, for the Horizon Reports domain: https://horizon-reports.local/FederationMetadata/2007-06/FederationMetadata.xml

* *ADFS Realm*: For the realm address, use the WS-Federation Passive protocol URL that was entered when configuring ADFS.

# OpenID Connect

To enable external authentication using OpenID Connect, you need to specify the *OpenID Authority*, the *OpenID ClientID* and the *OpenID ClientSecret*.

* *OpenID Authority*: A URL that points to the authentication server that supports the OpenID Connect protocol.

* *OpenID ClientID*: The ClientID value to send to the OpenID Connect authentication server.

* *OpenID ClientSecret*: The secret key value to send to the OpenID Connect authentication server.

## Automatically assign roles on user creation

The first time a user logs in with external authentication, a local Horizon Reports user account is created. During this process, you can have the Identity Provider instruct Horizon Reports to assign roles when the user is created. To do this, attach a comma-separated list of role names (for existing roles) to the ID Token the IdP server returns during authentication.

## Tenant Support With OIDC

If you have tenants enabled for a project, you can still use external authentication. In this case, during the connection/authorization process, the Identity Provider must tell Horizon Reports what tenant the current user belongs to. To do this, attach a tenant claim (for an existing tenant) to the ID Token the IdP server returns during authentication. If you have an existing external authentication system that already uses a claim named *tenant*, you can use *reporting_tenant* instead. If there's no tenant attached, or the tenant that's attached doesn't exist, the login attempt will be rejected.

# Facebook

To enable external authentication using Facebook, you need to specify the *Facebook AppID* and the *Facebook AppSecret*. Refer to the [developer documentation](https://developers.facebook.com/docs/) for details on creating an App that supports authentication.

# Google

To enable external authentication using Google, you need to specify the *Google ClientID* and the *Google ClientSecret*. To generate those values, navigate to [Integrating Google Sign-In into your web app](https://developers.google.com/identity/sign-in/web/sign-in#before_you_begin) and select CONFIGURE A PROJECT.

# Twitter

To enable external authentication using Twitter, you need to specify the *Twitter ConsumerKey* and the *Twitter ConsumerSecret*. To generate those values, navigate to [ https://apps.twitter.com/]( https://apps.twitter.com/) and create a new app for use with authentication.