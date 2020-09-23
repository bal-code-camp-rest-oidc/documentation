# Adding Identity Providers
0. Lookup credentials in Github:<br/>
![](./img/identity-provider/01-github-client.png)
0. Create new identity provider in Keycloak in your realm and set credentials:<br/>
![](./img/identity-provider/02-keycloak-identity-provider.png)
0. Assign a default, hard coded role within your identity provider in keycloak:<br/>
![](./img/identity-provider/03-keycloak-identity-provider-default-role-mapper.png)
0. Finally ensure that a default group will be set in Keycloak for new users:<br/>
![](./img/identity-provider/04-keycloak-identity-provider-default-group.png)
