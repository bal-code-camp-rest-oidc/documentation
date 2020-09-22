# First steps

## Intro Labs

### Auth-Code Demo

We could setup local Keycloak based on docker.
The demo showed us the https://tools.ietf.org/html/rfc7517, how the user goes through the different stages from client to the auth-provider, getting a authentication-token, back to the client, requesting the access-token, where we were able to call our backend-system.
```
     +----------+
     | Resource |
     |   Owner  |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier      +---------------+
     |         -+----(A)-- & Redirection URI ---->|               |
     |  User-   |                                 | Authorization |
     |  Agent  -+----(B)-- User authenticates --->|     Server    |
     |          |                                 |               |
     |         -+----(C)-- Authorization Code ---<|               |
     +-|----|---+                                 +---------------+
       |    |                                         ^      v
      (A)  (C)                                        |      |
       |    |                                         |      |
       ^    v                                         |      |
     +---------+                                      |      |
     |         |>---(D)-- Authorization Code ---------'      |
     |  Client |          & Redirection URI                  |
     |         |                                             |
     |         |<---(E)----- Access Token -------------------'
     +---------+       (w/ Optional Refresh Token)
```

### Github Client

In this exercise, we could authenticate by our Github-Account.
We created in the github-account of our organization a new OAuth-App.
Then we placed the gererated client-id and client-secret in to to
application.yaml.
Then, we tried to enhance the list of available Authentication-Providers with
the gitlab account.

## Lab 1

### Implement an OAuth2/OIDC resource server

Spring Security maps these scopes to the Spring Security authorities _SCOPE_library_admin_, _SCOPE_email_ and _SCOPE_profile_ by default.  
@PreAuthorize("hasRole('LIBRARY_ADMIN') || hasAuthority('SCOPE_library_admin')")
Discussion about @PreAuthorize vs @Secured or @RolesAllowed as described at [Baeldung](https://www.baeldung.com/spring-security-method-security)

### Glossary

[JWK](https://tools.ietf.org/html/rfc7517)