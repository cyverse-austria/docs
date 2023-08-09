# Kubernetes Cluster 

You can use **Ansible** to set up a kubernetes cluster.

Current kubernetes cluster is configured using ansible playbooks from [https://github.com/cyverse-austria/ansible-k8s.git](https://github.com/cyverse-austria/ansible-k8s.git).

You can use this ansible playbook to setup your own kubernetes Cluster on Operating Systems such as: **Centos7, Rocky Linux 8 and Debian 11**.

# Looking to setup your own k8s cluster?

If your are intrested to setup your own kubernetes cluster please follow the steps bellow.

## Preq

### Make sure you have at least **6** virtual machines configured with Centos7

* 1 Master node
* 4 worker nodes
* 1 worker node dedicated only for **vice-apps**

### Make sure you have Ansible installed, and you can reach your virtual machines via ssh

## Steps

### Clone the repo

```bash
# clone repo
git clone https://github.com/cyverse-austria/ansible-k8s.git

# navigate to cloned repo
cd ansible-k8s

```

### create your inventory

Create your inventory file under `/inventory/cyverse` and replace the host names as yours.
```bash
[k8s:children]
k8s-control-plane
k8s-worker

[kube-apiserver-haproxy]
k8-haproxy

[k8s-control-plane]
k8-c01
k8-c02

[k8s-storage:children]
k8s-worker

[k8s-worker:children]
vice-workers
k8s-workers

[k8s-workers]
k8-w01
k8-w02

[vice-workers]
k8-vice-w01

[outward-facing-proxy]
vice-haproxy-01

[haproxy]

[loadbalancer]
haproxy-01
```

### Run playbooks
**Note:** we are using `--user root --become`, if your virtual machines have a diffrent user you could change this.

#### Check if your hosts are reachable

```bash
ansible -i MYINVENTORY -m ping all --user root --become
```

#### Setup firewall configs

```bash
ansible-playbook -i MYINVENTORY firewalld-config.yml --user root --become
```

#### Provision your nodes

```bash
ansible-playbook -i MYINVENTORY provision-nodes.yml --user root --become
```

#### Init master/worker nodes

```bash
ansible-playbook -i MYINVENTORY multi-master.yml --user root --become
```

#### Tainting and Labeling VICE Worker Nodes

```bash
kubectl label nodes k8-vice-w01 vice=true
kubectl taint nodes k8-vice-w01 vice=only:NoSchedule
```
