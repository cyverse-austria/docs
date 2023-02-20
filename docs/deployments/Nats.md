# Install nats

**Here are some links for docs.**
* Docs for [nats](https://docs.nats.io/running-a-nats-service/nats-kubernetes) in k8s.
* [nats helm chart](https://nats-io.github.io/k8s/helm/charts/)
* CyverseUS [howto](https://gitlab.cyverse.org/core-sw/de-docs/-/tree/master/nats)

**install & configure nats (discover)**

```bash
# create certificates via cert-manager
kubectl apply -n discover -f resources/addons/nats/env/discover/nats-certs.yaml

# apply nodeport service
kubectl apply -n discover -f resources/addons/nats/env/discover/nats-service.yaml

# install nats via helm
helm repo add nats https://nats-io.github.io/k8s/helm/charts/
helm repo update

helm install nats nats/nats -n discover --values resources/addons/nats/values.yaml 
```


## Create `nats-services-creds` secret 
### TODO