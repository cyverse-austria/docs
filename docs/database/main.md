# DE Database
CyVerse is using [PostgreSQL](https://www.postgresql.org/) as its database.

Current deployment of CyVerse Austria has a single virtual machine which hosts a [PostgreSQL](https://www.postgresql.org/) database.

**This database is used for multiple services such as:**

* keycloak
* de
* notifications
* metadata
* unleash
* grouper
* qms
* portal

**NOTE: permissions database has been merged with DE database.**

## Install
The installation of this database is manully done on the host `cy-db01.tugraz.at'`.
See documentation on [how to install postgresql?](https://www.postgresguide.com/setup/install/)

**Here is some commands that we have used to install postgresql 12 on a Centos7 vm**

```bash
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

sudo yum install -y postgresql12-server
sudo /usr/pgsql-12/bin/postgresql-12-setup initdb
sudo systemctl enable postgresql-12
sudo systemctl start postgresql-12
sudo yum install postgresql12-contrib
```

## Setup
On this paragraph  we will cover first and necessary steps to configure the database.

### ~postgres/12/data/pg_hba.conf

**# IPv4 local connections:**
Add IP or IP range of kubernetes worker node, that requires connection to this database.

| TYPE | DATABASE | USER | ADDRESS | METHOD |
|------|----------|------|---------|--------|
|host  |all       | all  | *******/32 |md5   |
|host  |all       | all  | *******/32 |md5   |
|host  |all       | all  | *******/32 |md5   |
|host  |all       | all  | *******/32 |md5   |
|host  |all       | all  | *******/32 |md5   |
|host  |all       | all  | *******/32 |md5   |

### ~postgres/12/data/postgresql.conf

```bash
# vi ~postgres/12/data/postgresql.conf
listen_addresses = '*'          # what IP address(es) to listen on;
```

### .pgpass

**TODO:**

## Initialize databases

## Create databases

**Access the vm**
```bash
# ssh root@cy-db01.tugraz.at
psql -U postgres
```

**create the required database with users**

```bash
# create de user
create user de with password '********';

# create de database
create database de with owner de;

# create notifications database with de owner
create database notifications with owner de;

# create metadata database with de owner
create database metadata with owner de;

# create unleash database and user
## create unleash user
create user unleash with password '********';
## create unleash databased
create database unleash with owner unleash;

# create grouper database and user
## create grouper user
create user grouper with password '********';
## create grouper database
create database grouper with owner grouper;

# create database qms with de user
create database qms with owner de;

# TODO create other databases
# 1. portal  # https://gitlab.com/cyverse/portal2#setup-database
```

| DATABASE | USER |
|------|----------|
|  de  |    de    |
|  notifications  |    de    |
|  metadata |  de    |
|  unleash  | unleash_user    |
|  grouper |  grouper    |
|  portal  |  portal    |
|  keycloak |    keycloak |
|  qms |    de |


## Add required extensions for databases

```bash
# psql -U postgres
# \c de
# \c notifications
# \c metadata
# \c unleash
# \c grouper
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";

# \c qms
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
create extension "insert_username";
```

## Populate Databases
**TODO**

### de Database
**TODO**

### notification Database
**TODO**

### metadata Database
**TODO**

### grouper Database
**TODO**

### unleash Database
This database does not requires populate, on first connection the required tables are created manully.

### keycloak Database
This database does not requires populate, on first connection the required tables are created manully.

### portal Database
**TODO:**

### qms Database
**TODO:**

