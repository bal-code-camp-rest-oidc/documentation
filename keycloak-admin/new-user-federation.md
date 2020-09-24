# Add User Federation

## Requirements

The docker compose file ```oidc-application-client/docker-compose-setup/docker-compose.yml``` starts up all you need:
- OIDC: Keycloak
- DBMS: mysql
- LDAP-Server: ApacheDS

## Create User Federation
As a first step you create your new user federation:
![](./img/user-federation/01-keycloak-new-user-federation.png)

The following parameters are important to be set, as we use ApacheDS (and the default values within the applied image):
- Connection URL = ```ldap://apacheds:10389"``` (be aware that you need to use the service name as described in docker-compose)
- User DN = ```ou=users,ou=system```
- Bind DN = ```uid=admin, ou=system```
- Bind Credential = ```secret```

## Add Group Mapper
To ensure that your users are assigned to the appropriate groups you have to add a group mapper:
![](./img/user-federation/02-keycloak-new-group-mapper.png)

The following values have to be adapted due to use of ApacheDS:
- LDAP Groups DN = ```ou=groups,ou=system```
- Group Object Classes = ```groupOfUniqueNames```
- Membership LDAP Attribute = ```uniqueMember```
- Mode = ```LDAP_ONLY```

Finally you can ```Sync Keycloak Groups To LDAP```.

## Add Role Mapper
Furthermore roles have to be assigned properly as well:
![](./img/user-federation/03-keycloak-new-role-mapper.png)

**In our case we assume groups and roles to be the same!**

The following values have to be adapted due to use of ApacheDS:
- Name = ```role-mapper```
- Mapper Type = ```role-ldap-mapper``` (selection from predefined values)
- LDAP Roles DN = ```ou=groups,ou=system```
- Role Object Classes = ```groupOfUniqueNames```
- Membership LDAP Attribute = ```uniqueMember```
- Mode = ```LDAP_ONLY```

Again you can ```Sync Keycloak Roles To LDAP```.

## Synchronize/ Clean-up

![](./img/user-federation/04-keycloak-synchronize-remove.png)

On the concrete user federation you can finally synchronize:
- only the changed users
- all users

Additionally you can clean up by:
- removing all imported