# Keycloak
*Current keycloak version: 22.0*

## Preq

### configure database 

To setup and configure database please have a look at [keycloak database](../database/keycloak-db.md).


### create namsespace

```bash
# create ns
kubectl create ns keycloak
```

### Create required secrets & configmap

Keycloak deployment requires secrets and configmaps, which can be done via a `kustomization.yaml` file, please see below for an example of this template:

```yaml
secretGenerator:
- name: dbuser      # Database
  literals:
  - username=<USERNAME>
  - password=<PASSWORD>
- name: kcadmin     # keyclaok
  literals:
  - username=<USERNAME>
  - password=<PASSWORD>
configMapGenerator:
- name: keycloak-config
  literals:
  - KEYCLOAK_HOSTNAME=https://keycloak.example.com/auth
  - KEYCLOAK_HOSTNAME_STRICT_HTTPS=false
  - KEYCLOAK_HOSTNAME_STRICT=false
  - KEYCLOAK_LOGLEVEL=INFO
  - KEYCLOAK_PROXY=edge
  - DB_VENDOR=postgres
  - DB_ADDR=<DATABASE_HOST>
  - DB_PORT=5432
  - PROXY_ADDRESS_FORWARDING=true
  - JDBC_PARAMS=connectTimeout=21600
  - JAVA_OPTS=-server
    -Xms4096m
    -Xmx8192m
    -XX:MetaspaceSize=96m
    -XX:MaxMetaspaceSize=256m
    -Djboss.modules.system.pkgs=org.jboss.byteman
    -Djava.awt.headless=true
    -Dkeycloak.profile.feature.token_exchange=enabled
    -Djava.security.egd=file:/dev/urandom
namespace: keycloak
resources:
- deployment.yaml
- service.yaml
generatorOptions:
  disableNameSuffixHash: true
```

* Update the values of the `kustomization.yaml` file.
* place the `kustomization.yaml`, `deployment.yaml` and `service.yaml` inside a directory. e.g. `base`

### deployment & service YAML files:

**TODO:** find a way to add those files.

## Deploy

```bash
# apply kustomize
kubectl apply -k ./base/ -n keycloak
```
---

# Keycloak: Setting Up a New Realm for CyVerse

This guide walks you through the process of creating and configuring a fresh Keycloak realm for **CyVerse**.

---

## 1. Create the Realm

1. Log in to the Keycloak admin console.
2. Create a new realm named: **CyVerse**

---

## 2. Import Clients

Import predefined clients from the following repository:

- 📂 [Clients Configuration Files](https://github.com/mb-wali/cyverse.at/tree/main/k8s/keycloak/Admin-config/clients)

> **Note:** These configuration files are currently private. **TODO:** Make the repository public for easier access.

---

## 3. Add Mappers and Groups

Set up necessary mappers and user groups as outlined in the repository:

- 📘 [Admin Configuration Guide](https://github.com/mb-wali/cyverse.at/blob/main/k8s/keycloak/README.md#admin-configs)

> **TODO:** Ensure this documentation is made public if sharing with external teams.

---
