# Redis HA

In this Document we will cover installing the **Redis Server** and **Redis Haproxy**, due to the `k8s-resources` configurations both would be installed and configured inside the **prod** namespace.

## Preq

Make sure to create a **values.yaml** and replace add your credentials:

**values.yaml**
Overrides the PersistentVolume, adds secrets and uses **openebs** as storage class.

```yaml
## replicas number for each component
replicas: 3

persistentVolume:
  enabled: true
  ## redis-ha data Persistent Volume Storage Class
  ## If defined, storageClassName: <storageClass>
  ## If set to "-", storageClassName: "", which disables dynamic provisioning
  ## If undefined (the default) or set to null, no storageClassName spec is
  ##   set, choosing the default provisioner.  (gp2 on AWS, standard on
  ##   GKE, AWS & OpenStack)
  ##
  storageClass: openebs-hostpath

## Sentinel specific configuration options
sentinel:
  auth: true
  authkey: <AUTH-KEY>
  password: <PASSWORD>

## Redis specific configuration options
auth: true
authkey: <AUTH-KEY>
redisPassword: <PASSWORD>
```

## Redis Server & Sentinel

```bash
# add helm repo
helm repo add dandydev https://dandydeveloper.github.io/charts
helm repo update

# deploy redis servers
helm upgrade --install --namespace prod redis-ha dandydev/redis-ha --values values.yaml

# uninstall
## helm uninstall --namespace prod redis-ha
```


# Redis Haproxy

## TODO

**redis-haproxy**
```bash
# make sure to load the configs to create service-config secret
# ./load_configs.py -e discover -n discover
kubectl apply -n prod -f resources/deployments/redis-haproxy.yml
```
