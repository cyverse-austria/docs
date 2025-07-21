# [OpenEBS](https://openebs.io/)

## Install with Helm

```bash
helm repo add openebs https://openebs.github.io/openebs
helm repo update

helm install openebs --namespace openebs openebs/openebs --create-namespace

# If you do not want to install OpenEBS Replicated Storage, use the following command
helm install openebs --namespace openebs openebs/openebs --set engines.replicated.mayastor.enabled=false --create-namespace
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