# setup octa

```less
Octa endpoints:
Security: API
    default
        api://default
        https://dev-74235182.okta.com/oauth2/default

    Issuer
        Okta URL https://dev-74235182.okta.com/oauth2/default
    Metadata URI
        https://dev-74235182.okta.com/oauth2/default/.well-known/oauth-authorization-server
    Audience
        api://default
```

[octa endpoints](https://dev-74235182.okta.com/oauth2/default/.well-known/oauth-authorization-server)

```less
Applications -> Applications
+Create App Integration

    OIDC - OpenID Connect
        Web Application

Grant type:
    Authorization Code
    Refresh Token

Sign-in redirect URIs:
    http://localhost:8080/authorization-code/callback

Sign-out redirect URIs:
    http://localhost:8080

Assignments -> Controlled access
    Limit access to selected groups (Skip group assignment for now)
```