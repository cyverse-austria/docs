# vice apps

## create namespace
```bash
kubectl create ns vice-apps
```

## create a secret on namespace vice-apps

```bash
kubectl create secret generic vice-image-pull-secret \
    --from-file=.dockerconfigjson=/root/.docker/config.json \
    --type=kubernetes.io/dockerconfigjson -n vice-apps
```

## create serviceAccounts
```bash
## edit the namespace if you are running in a diffrent env
## vi /k8s-resources/resources/serviceaccounts/app-exposer.yml
kubectl apply -f /k8s-resources/resources/serviceaccounts/app-exposer.yml
kubectl apply -f /k8s-resources/resources/serviceaccounts/vice-app-runner.yml
```

## apply clusterrolebindings
```bash
## edit the namespace if you are running in a diffrent env
## vi /k8s-resources/resources/clusterrolebindings/app-exposer.yml
kubectl apply -f /k8s-resources/resources/clusterrolebindings/app-exposer.yml
```

## apply networkpolicies
**TODO make it better in docs**

```bash
# change the ip range: of file: /k8s-resources/resources/networkpolicies/vice-apps.yml
## from 
        # except:
        # - ********
        # - ********

## To
        # except:
        # - 10.0.10.0/24        # k8s master CIDR
        # - 164.92.209.248/32   # c1 
        # - 206.189.106.224/32  # w1 
        # - 167.71.9.238/32     # w2 
        # - 178.62.213.248/32   # w3 
        # - 134.122.50.71/32    # w4
        # - 157.245.73.20/32    # w5 
        # - 64.227.79.232/32    # vice-w1 

# run policy
kubectl apply -f /k8s-resources/resources/networkpolicies/vice-apps.yml
```

## apply roles

```bash
kubectl apply -f /k8s-resources/resources/roles/vice-apps.yml
```

## create porklock-config secrert for irods

### Create irods-config.properties

Create a file `irods-config.properties` and add the values.

```properties
porklock.irods-home=
porklock.irods-user=
porklock.irods-pass=
porklock.irods-host=
porklock.irods-port=
porklock.irods-zone=
porklock.irods-resc=
```

### create secret from file

```bash
kubectl -n vice-apps create secret generic porklock-config --from-file=irods-config.properties
```

## restart the services
```bash
kubectl rollout restart apps app-exposer templeton-incremental templeton-periodic -n NAMESPACE
```

## Install/configure ingress-nginx

For installing and configuring the **ingress-nginx** have a look at [ingress-nginx](ingress-nginx.md)

