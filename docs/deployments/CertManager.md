### install & configure cert-manager via k8s-resources

```bash
kubectl create namespace cert-manager

# install cert-manager custom
kubectl apply -f resources/addons/cert-manager/cert-manager.custom.yaml

# apply issuer
kubectl apply -f resources/addons/cert-manager/issuers.yaml
```

