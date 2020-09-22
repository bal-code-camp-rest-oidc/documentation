# Second day

## Lab 2

### PCME workflow

The PCME addition is needed to prevent the authorization code interception attack. It adds a challenged key and method to the authorization request. If the client requests for access token it adds the key to challenge. So the authz server can compare the challenged key and the key to challenge (with challenge method).

The Authz Server publishes the supported methods under the key `code_challenge_methods_supported` in [the open id-configuration](http://localhost:8080/auth/realms/workshop/.well-known/openid-configuration).
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


## Discussion points

Why are we using statefull session for client?