# Third day

## Keycloak Operator Openshift

To install the operator you need to go to the operator -> operator hub section in the openshift console. There you will find a keycloak operator.

![operator1](img/keycloak-operator-1.png)

After installing it your operator is ready to install keycloak servers in given namespaces.

You can install the following components:
![operator2](img/keycloak-operator-2.png)

We start with installing a keycloak instance:
![operator3](img/keycloak-operator-3.png)

We end up with the following yaml configuration:
```yaml
apiVersion: keycloak.org/v1alpha1
kind: Keycloak
metadata:
  name: example-keycloak
  labels:
    app: sso
  namespace: okd4-sampleconfig
spec:
  externalAccess:
    enabled: true
  instances: 1
  keycloakDeploymentSpec:
    resources:
      requests:
        cpu: 500m
        memory: 2Gi
```

Route specification:

```yaml
spec:
  host: keycloak-okd4-sampleconfig.apps.okd.baloise.dev
  to:
    kind: Service
    name: keycloak
    weight: 100
  port:
    targetPort: keycloak
  tls:
    termination: reencrypt
  wildcardPolicy: None
```

