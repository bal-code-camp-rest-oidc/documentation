# Second Day, 22.09.2020

On that second day we focused on finishing the labs (https://github.com/andifalk/secure-oauth2-oidc-workshop).

## Lab 2

### PKCE Workflow

The PKCE addition is needed to prevent the authorization code interception attack. It adds a challenged key and method
to the authorization request. If the client requests for access token it adds the key to challenge. So the authz server
can compare the challenged key and the key to challenge (with challenge method).

The Authz Server publishes the supported methods under the key `code_challenge_methods_supported`
in [the open id-configuration](http://localhost:8080/auth/realms/workshop/.well-known/openid-configuration).

```
                                                  +-------------------+
                                                 |   Authz Server    |
       +--------+                                | +---------------+ |
       |        |--(A)- Authorization Request ---->|               | |
       |        |       + t(code_verifier), t_m  | | Authorization | |
       |        |                                | |    Endpoint   | |
       |        |<-(B)---- Authorization Code -----|               | |
       |        |                                | +---------------+ |
       | Client |                                |                   |
       |        |                                | +---------------+ |
       |        |--(C)-- Access Token Request ---->|               | |
       |        |          + code_verifier       | |    Token      | |
       |        |                                | |   Endpoint    | |
       |        |<-(D)------ Access Token ---------|               | |
       +--------+                                | +---------------+ |
                                                 +-------------------+
```

## Discussion Points
Why are we using stateful session for client?

## Nonce Parameter
Documentation of [auth parameters](https://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)

The nonce parameter value needs to include per-session state and be unguessable to attackers. One method to achieve
this for Web Server Clients is to store a cryptographically random value as an HttpOnly session cookie and use a
cryptographic hash of the value as the nonce parameter. In that case, the nonce in the returned ID Token is compared
to the hash of the session cookie to detect ID Token replay by third parties. A related method applicable to JavaScript
Clients is to store the cryptographically random value in HTML5 local storage and use a cryptographic hash of this value.

## Lab 3
In lab 3 we learned how we can access a resource server with a standalone client (in our case a spring batch). Here we
are using the [OAuth2 client credentials grant flow](https://tools.ietf.org/html/rfc6749#section-4.4) to get the token
you need to register the client in the keycloak. 

## Lab 4
In this lab we implemented a custom mapping and some unit and integration tests using Mockito as well as SpringBoot tests.

## Lab 5
In this lab we implemented OAuth2/OIDC tests using own self-signed JWT (instead of keycloak) tokens which makes testing much easier.
Using https://jwt.io helps to make the contents of a JWT token visible.

## Lab 6
In this lab we added an Angular client using our OAuth2/ OIDC infrastructure.