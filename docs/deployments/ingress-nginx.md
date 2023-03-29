# ingress-nginx

**ingress-nginx** is used to give vice-apps ingresses, using nodeport and what not.


## deploy

The deployment manifests are in [k8s-resources](k8s-resources.md).

### (optional) changing the env

Modify file `resources/kustomize/ingress-nginx/overlays/prod/args.yaml`, to change the namespace.

```diff
- --default-backend-service=prod/vice-default-backend
+ --default-backend-service=discover/vice-default-backend
```

### Deploy kustomize

This script will create a namespace `ingress-nginx`.

```bash
kubectl apply -k resources/kustomize/ingress-nginx/overlays/prod
```



## Issues

**failed calling webhook**
```bash
"Internal error occurred: failed calling webhook \"validate.nginx.ingress.kubernetes.io\": Post \"https://ingress-nginx-controller-admission.ingress-nginx.svc:443/networking/v1/ingresses?timeout=10s\": service \"ingress-nginx-controller-admission\" not found"
```

**solution**
```bash
kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission
```