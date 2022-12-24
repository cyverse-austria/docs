# User Portal

## Preq

### TODO: add source location

### Images

1. harbor.cyverse.org/hub/library/nginx:1.20-alpine **Replaced with**:nginx:1.20-alpine

2. mbwali/portal:tug-stable
    * Todo: tekton should build this via the URL.

## Deploy

```bash
# create ns
kubectl create ns user-portal

# deploy 
kubectl apply -k portal/user-portal/base -n user-portal
```
