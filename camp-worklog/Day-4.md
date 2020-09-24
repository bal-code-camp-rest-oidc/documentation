# Fourth day


## Keycloak Realm Openshift
The realm configuration of keycloak operator is limited. The following configurations are available:

![Realm-Sections](img/realm-1.png)

We tried to convert the given keycloak-json-configuration to yaml with the [Json2Yaml](https://www.json2yaml.com/).

We could not use it for our purpose, as we should also configure realm specific
roles, which are not supported.

Another solution to import config would be to use the  [keycloak-cli](https://github.com/adorsys/keycloak-config-cli) until the complete configuration is available on operator.

For this reason we imported the configuration through json import.

## Conclusion

For our CodeCamp, we stopped to configure the realm by gitops/scirpt-based, and
imported the given realm-config from the workshop through the KeyCloak UI Import-Feature.
