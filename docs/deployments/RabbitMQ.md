# AMQP
We are using ansible [playbooks](https://github.com/cyverse-austria/ansible-amqp) to install and configure AMQP server.


## Reindex RabbitMQ jobs

### access the vm where the RabbitMQ is installed.

```bash
ssh root@RABBITMQ_HOST
```

### Configure rabbitmqadmin

This step you have to do only once, if the rabbitmqadmin is not present.

```bash
mkdir adm
cd adm
wget http://localhost:15672/cli/rabbitmqadmin
chmod +x rabbitmqadmin
```

### Commands 

#### QA 

```bash
# check status
systemctl status rabbitmq-server.service -l

## add your password to a temp var
read -s PASSWORD && export PASSWORD

# list exchange
./rabbitmqadmin -V /cyverse/de list exchanges -u cyverse -p $PASSWORD

# publish the message to reindex all
./rabbitmqadmin publish -V /cyverse/de -u cyverse -p $PASSWORD exchange=de routing_key=index.all payload=""

# restart services
kubectl rollout restart deployment infosquito2 -n qa
kubectl rollout restart deployment search -n qa

# IF not deployed
# ./deploy.py -Bn qa -p infosquito2 search -C
```

#### PROD
```bash
## add your password to a temp var
read -s PASSWORD && export PASSWORD

# list
./rabbitmqadmin -V /tugraz/de list exchanges -u tugraz -p $PASSWORD

# publish the message to reindex all
./rabbitmqadmin publish -V /tugraz/de -u tugraz -p $PASSWORD exchange=de routing_key=index.all payload=""

```

