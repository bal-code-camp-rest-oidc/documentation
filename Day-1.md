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

We where able to secure our backend-app via the public Github client.

### OAuth 2.0

### Glossary

[JWK](https://tools.ietf.org/html/rfc7517)