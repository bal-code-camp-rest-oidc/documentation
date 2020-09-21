# Adminstrating Keycloak

## Creating New Client
0. Goto http://localhost:8080/ and use "Administration Console"
0. Login using credentials "admin/admin"
0. Click on "Clients" and press "Create": add all parameters as specified below (use "library-client" as template)<br/>
![](./img/new-client/01-clients.png)
0. Set further configuration parameters as shown below.<br/>
![](./img/new-client/02-create-client.png)
![](./img/new-client/03-client-configuration.png)
0. Provide all "Client Scopes"<br/>
![](./img/new-client/04-client-scopes.png)
0. Modify "Library Account Roles" as follows<br/>
![](./img/new-client/05-service-account-roles.png)
0. Copy your client secret for later use in postman<br/>
![](./img/new-client/06-client-secrets.png)
0. Execute post man with following settings<br/>
![](./img/new-client/07-postman-request.png)<br/>
Explanation for the [state parameter](https://auth0.com/docs/protocols/state-parameters#csrf-attacks).
0. login as user "bwayne/wayne"<br/>
![](./img/new-client/08-login.png)
0. Et voila - here is you first own client access.<br/>
![](./img/new-client/09-token-response.png)
