# [OpenEBS](https://openebs.io/)

## Deploy

```bash
# create namespace
kubectl create ns openebs

# deploy
kubectl -n openebs apply -f https://openebs.github.io/charts/openebs-operator.yaml
```


## Issues

If encounter an issue regarding the openebs certificate expired:

`openebs admission-webhook.openebs.io\": Post \"https://admission-server-svc.openebs.svc:443/validate?timeout=5s\": x509: certificate has expired`

**do the followings**:

```bash
kubectl delete secret admission-server-secret -n openebs
kubectl delete validatingwebhookconfigurations.admissionregistration.k8s.io openebs-validation-webhook-cfg
kubectl rollout restart deployment openebs-admission-server -n openebs
```