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


## Server deploy in openshift

### Github Actions
We wanted to build an image to deploy our library server to openshift. To do this we decided to use the new github actions instead of travis. To build the image we decided to use native [gradle bootBuildImage task](https://spring.io/guides/gs/spring-boot-docker/). To enable the right docker image name we need to add the following lines to build.gradle:
```gradle
bootBuildImage{
    imageName='luechtdiode/oidc-ws-library-server'
}
```

We searched for a Action that pushes only the builded image, but all availlable
Github-Actions in the Marketplace managed both (build & push) in one atomic step.

Our soultion now is motivated by [www.prestonlamb.com/blog](https://www.prestonlamb.com/blog/creating-a-docker-image-with-github-actions), where all plain docker-commands are scripted straight forward as Github-Action-Steps.

### Env Variables
To pass keycloak parameters to our new docker image, we substituted our hard-coded values with environment variables. 

```yaml
spring:
  ...
  security:
    oauth2:
      resourceserver:
        jwt:
          jwk-set-uri: ${JWK_SET_URI}
          issuer-uri: ${ISSUER_URI}
```

After that change we are able to parametrize our keycloak uris from the openshift-instance, starting the local dockerized server-instnance to test
the new substituted env-variables:

```bash
docker run \
    --rm -p 9091:9091 \
    -e JWK_SET_URI=https://keycloak-okd4-sampleconfig.apps.okd.baloise.dev/auth/realms/workshop/protocol/openid-connect/certs \
    -e ISSUER_URI=https://keycloak-okd4-sampleconfig.apps.okd.baloise.dev/auth/ \
    realms/workshop docker.io/luechtdiode/oidc-ws-library-server:latest

```
We could use the postman-testcases to authenticate on keykloak in openshift (getting the access-token) and calling the rest-api in the dockerized backend-server.
