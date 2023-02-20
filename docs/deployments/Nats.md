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


**exec inside the nats-box pod**

```bash
~ # nsc init
? enter a configuration directory /nsc/nats/nsc/stores
? Select an operator Create Operator
? name your operator, account and user de
[ OK ] created operator de
[ OK ] created system_account: name:SYS id:AD7P42WOUA25BDUXFQJRCMQYSYTWRD3SDNF3CUFG7DYB5GDQWPEZZA7D
[ OK ] created system account user: name:sys id:UDZPB3OP3ZKM6X6UDV25ZKX2FOWIBRUUCLNJOBLLD7BOV4OQFLJVEZ7Z
[ OK ] system account user creds file stored in `/nsc/nkeys/creds/de/SYS/sys.creds`
[ OK ] created account de
[ OK ] created user "de"
[ OK ] project jwt files created in `/nsc/nats/nsc/stores`
[ OK ] user creds file stored in `/nsc/nkeys/creds/de/de/de.creds`
> to run a local server using this configuration, enter:
>   nsc generate config --mem-resolver --config-file <path/server.conf>
> then start a nats-server using the generated config:
>   nats-server -c <path/server.conf>
all jobs succeeded
~ #  nsc add operator -n de --sys
[ERR ] operator named de exists already please inspect and use --force to overwrite
Error: all jobs failed
~ #  nsc add operator -n cyverse --sys
[ OK ] generated and stored operator key "OANHTCLQLGTQFVRPNBTJ7HD56HTKMORLSLBZYUD7ETQAB3EQUBYFRD7J"
[ OK ] added operator "cyverse"
[ OK ] When running your own nats-server, make sure they run at least version 2.2.0
[ OK ] created system_account: name:SYS id:AA3TP5UNGFT3Z3CZAQDUUKYTWBMCBWMPQQ7Z4BVFG43ZBNRKQUJHBWJF
[ OK ] created system account user: name:sys id:UCSUROZYTQZPVC6NRFUMLOLZ472ZFCUREKVN6J7FOUGXYCU4BCVZ43J3
[ OK ] system account user creds file stored in `/nsc/nkeys/creds/cyverse/SYS/sys.creds`
~ # nsc generate nkey -o --store
OBH2PGMFLUSYDTA3OUTSOJT5LSRIY2CJU6MCEMJJMAMULWZMYHSEISQN
operator key stored /nsc/nkeys/keys/O/BH/OBH2PGMFLUSYDTA3OUTSOJT5LSRIY2CJU6MCEMJJMAMULWZMYHSEISQN.nk

~ # nsc edit operator --sk OBH2PGMFLUSYDTA3OUTSOJT5LSRIY2CJU6MCEMJJMAMULWZMYHSEISQN
[ OK ] added signing key "OBH2PGMFLUSYDTA3OUTSOJT5LSRIY2CJU6MCEMJJMAMULWZMYHSEISQN"
[ OK ] edited operator "cyverse"
~ # nsc add account -n de -K OANHTCLQLGTQFVRPNBTJ7HD56HTKMORLSLBZYUD7ETQAB3EQUBYFRD7J
[ OK ] generated and stored account key "AAPA2QMALWDT7MQOITMTTOULTVMUJM2CW4UGPBKECAJDYCYBK6JZNH2Z"
[ OK ] added account "de"
~ # nsc generate nkey -a --store
ABDVLFKHFWYBHJWUNC35S3VA4YGCW2SVD6MU2RSZBOJD42SJFXZLY372
account key stored /nsc/nkeys/keys/A/BD/ABDVLFKHFWYBHJWUNC35S3VA4YGCW2SVD6MU2RSZBOJD42SJFXZLY372.nk

~ #   nsc edit account -n de --sk ABDVLFKHFWYBHJWUNC35S3VA4YGCW2SVD6MU2RSZBOJD42SJFXZLY372
[ OK ] added signing key "ABDVLFKHFWYBHJWUNC35S3VA4YGCW2SVD6MU2RSZBOJD42SJFXZLY372"
[ OK ] edited account "de"
~ # nsc add user --account de --name services -K ABDVLFKHFWYBHJWUNC35S3VA4YGCW2SVD6MU2RSZBOJD42SJFXZLY372
[ OK ] generated and stored user key "UAYRAHG5GXMA4DX4S46HYWWPIK5MWO64RRHXBGUDB32WXCOW6EKQFJUN"
[ OK ] generated user creds file `/nsc/nkeys/creds/cyverse/de/services.creds`
[ OK ] added user "services" to account "de"
~ # cat /nsc/nkeys/creds/cyverse/de/services.creds
-----BEGIN NATS USER JWT-----
eyJ0eXAiOiJKV1QiLCJhbGciOiJlZDI1NTE5LW5rZXkifQ.eyJqdGkiOiJOUlVCTDM1RFBNN1hZRFNFQkdHSVYzN0NUTVJKNElZNzIzREJWWk5ISkE1U1pCSkUzWlJRIiwiaWF0IjoxNjc2MzkzOTIxLCJpc3MiOiJBQkRWTEZLSEZXWUJISldVTkMzNVMzVkE0WUdDVzJTVkQ2TVUyUlNaQk9KRDQyU0pGWFpMWTM3MiIsIm5hbWUiOiJzZXJ2aWNlcyIsInN1YiI6IlVBWVJBSEc1R1hNQTREWDRTNDZIWVdXUElLNU1XTzY0UlJIWEJHVURCMzJXWENPVzZFS1FGSlVOIiwibmF0cyI6eyJwdWIiOnt9LCJzdWIiOnt9LCJzdWJzIjotMSwiZGF0YSI6LTEsInBheWxvYWQiOi0xLCJpc3N1ZXJfYWNjb3VudCI6IkFBUEEyUU1BTFdEVDdNUU9JVE1UVE9VTFRWTVVKTTJDVzRVR1BCS0VDQUpEWUNZQks2SlpOSDJaIiwidHlwZSI6InVzZXIiLCJ2ZXJzaW9uIjoyfX0.cvlb9j2VTjUckg2LttXFUGdfGqY8v7xDuzEbrjM6PwHaXjfbeeJ2kuVxdCfDWfH5uNWh04iF_qnieewpDH1nBw
------END NATS USER JWT------

************************* IMPORTANT *************************
NKEY Seed printed below can be used to sign and prove identity.
NKEYs are sensitive and should be treated as secrets.

-----BEGIN USER NKEY SEED-----
SUANTZ7PO7A7PCZKZULIFIEJX5E62YRLJIP76UKBA4A3AVNKMQJ26DFSU4
------END USER NKEY SEED------

*************************************************************
```

**copy secert file from the nats-box pod & create from it a secret**
```bash
# copy the cred file from the pod 
kubectl -n discover cp nats-box-6cdf5f4bb-q9s5m:/nsc/nkeys/creds/cyverse/de/services.creds services.creds

# create the secret from a file which we have created
kubectl -n discover create secret generic nats-services-creds --from-file services.creds
```
