# Single Sign-On (OIDC)

> This feature is available in v0.5+

# Intro

Warpgate can use arbitrary OpenID Connect (OIDC) providers to authenticate users based on their verified emails.

OIDC providers include, but are not limited to:

* Google Accounts
* Sign in with Apple
* GitLab
* Microsoft Azure
* Okta

# Configuration

## External host setting (before v0.12)

To use SSO, Warpgate needs to know what its external hostname is. It'll try its best to figure it out based on the client's request, but it's better if you set it explicitly via the top-level `external_host` config option:

```diff
+ external_host: warpgate.acme.inc
```

> `external_host` can include a port as well

Starting with v0.12, Warpgate uses the `Host` header to determine the external host.

## SSO Providers

### Obtaining app credentials from a provider

You'll need to register your Warpgate instance as an "app" (terminology varies per provider) at the provider and obtain a _Client ID_ and a _Client secret_. You'll need to provide a _Redirect URL_ which - which will be verified by the SSO provider.

The _redirect URL_ for Warpgate is `https://<warpgate-external-host>/@warpgate/api/sso/return`.

Okta provides excellent guides on registering an app with various providers:

* [Google](https://developer.okta.com/docs/guides/social-login/google/main/#create-an-app-at-the-identity-provider)
* [Apple](https://developer.okta.com/docs/guides/social-login/apple/main/#create-an-app-at-the-identity-provider)
* [GitLab](https://developer.okta.com/docs/guides/social-login/gitlab/main/#create-an-app-at-the-identity-provider)
* [Microsoft Azure](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)

### Adding credentials to the config file

With a _Client ID_ and a _Client Secret_ in hand, you can add these to the Warpgate config file:

#### Google

```diff
external_host: warpgate.acme.inc:8888

+ sso_providers:
+ - name: google
+   label: Google login
+   provider:
+     type: google
+     client_id: 1234...
+     client_secret: ABC...
```

#### Microsoft Azure

```diff
external_host: warpgate.acme.inc:8888

+ sso_providers:
+ - name: azure
+   provider:
+     type: azure
+     client_id: 123...
+     client_secret: ABC...
+     tenant: XYZ...
```


#### Apple (⚠️ v0.6.6+)

```diff
external_host: warpgate.acme.inc:8888

+ sso_providers:
+ - name: apple
+   label: Apple ID
+   provider:
+     type: apple
+     team_id: ABC...  # your Apple Team ID
+     client_id: com.warpgate.test  # your Service ID (not the App ID!)
+     key_id: ABC...  # the ID of the key you've created
+     client_secret: ABC...  # Base64 encoded contents of the .p8 private key file you've got from Apple

```

#### Custom


```diff
external_host: warpgate.acme.inc:8888

+ sso_providers:
+ - name: custom
+   label: ACME SSO
+   provider:
+     type: custom
+     client_id: 123...
+     client_secret: ABC...
+     issuer_url: https://sso.acme.inc,
+     scopes: ["email"],
```

### Requiring SSO for a user

Users are linked to their SSO accounts based on their email. If the SSO provider advertises email verification status, Warpgate will require the email to be verified.

To link a user to SSO, click `Add SSO` in the credentials section, and then (optionally) set SSO as the only accepted credential type for HTTP connections.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/190000970-70a63709-7cf3-41a9-a445-ef18b21690d0.png">

Here, we've also set SSO to be the only allowed login credential for HTTP auth, and have set SSH to use out-of-band web authentication. 

> `In-browser auth` (OOB web authentication) means that Warpgate will send a login link to the SSH client and will wait for the user to authenticate themselves in a browser. The auth requirements will be the same as set for the `http` protocol. 

```
❯ ssh cwilde:tnt@warpgate.acme.inc -p 2222   
----------------------------------------------------------------
Warpgate authentication: please open https://warpgate.acme.inc:8888/@warpgate#/login/31282192-ad29-4fa7-bdc2-5b481d531e58 in your browser
----------------------------------------------------------------

(cwilde:tnt@warpgate.acme.inc) Press Enter when done: 
```

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/183523588-1d77bd16-dbc0-4b6a-95bf-16a1a64d0aca.png">

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/183523841-5814116c-8574-45fa-9d04-094c28d5cf0b.png">

## Setting roles via SSO (⚠️ v0.10+)

With `custom` type OIDC providers, Warpgate can also sync the user's role memberships when they log in.

For that, your provider must set a `warpgate_roles` OIDC claim (a JSON array of role names) either in the ID Token or the UserInfo response. By default, Warpgate will use these names as-is and completely overwrite the user's memberships.

You can also set `role_mappings` in the provider's configuration to explicitly map claim values to role names. In this case, only the roles mentioned here will be synced SSO, and the memberships in other roles won't be affected. For example:

```yaml
- name: oidc-custom
  label: Custom SSO
  provider:
    type: custom
    client_id: ...
    client_secret: ...
    issuer_url: ...
    scopes: []
    role_mappings:
      'QA group': 'qa'
      Admins: 'warpgate:admin'
```