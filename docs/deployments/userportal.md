# User Portal

## Preq

### TODO: add source location

## Deploy

```bash
# create ns
kubectl create ns user-portal

# deploy 
kubectl apply -k portal/user-portal/base -n user-portal
```