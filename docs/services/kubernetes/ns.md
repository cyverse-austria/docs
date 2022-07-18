# Namespaces

List of namespaces used for CyVerse deployment in kubernetes.
**Note**: this documentation is relavant only for single/current environment.

![Namespaces](../assets/namespaces.png)

## prod
This namespace is dedicated to the [core services](index.md) & some of non-core services such as : 
* redis-ha
* redis-haproxy
* elasticsearch

## irods-csi-driver
This namespace is dedicated to the [irods-csi-driver](https://github.com/cyverse/irods-csi-driver) deployment and configurations.

## keycloak
This namespace is dedicated to keycloak related deployment and configurations.

## openebs
This namespace is dedicated to the [openebs](https://openebs.io/) deployment.
OpenEBS turns any storage available on the Kubernetes worker nodes into local or distributed Kubernetes Persistent Volumes.


## ingress-nginx
This namespace is dedicated to the [ingress-nginx](https://docs.nginx.com/nginx-ingress-controller/) deployment.

## vice-apps
This namespace is dedicated to the [VICE](https://cyverse.org/node/50) related deployment and configurations.
