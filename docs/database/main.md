# Databases

CyVerse is using [PostgreSQL](https://www.postgresql.org/) as its database.

**These database dedicated to the *discovery environment* of Cyverse, which is used for multiple services such as:**


| Database      | Owner    | Auto Init    | Auto Migrate |
| ------------- | -------- | ------------ | ------------ |
| [de Database](de-db.md)            | de       | no           | no           |
| [Notifications Database](notifications-db.md) | de       | no           | no           |
| [Metadata Database](metadata-db.md)      | de       | no           | no           |
| [DE Releases](de-releases.md)   | de       | no           | no           |
| [Grouper Database](grouper-db.md)       | grouper  | yes          | ?            |
| [QMS Database](qms-db.md)           | de       | configurable | configurable |
| [Unleash Database](unleash-db.md)       | de       | yes          | ?            |
| [Keycloak Database](keycloak-db.md)      | keycloak | yes          | ?            |
| [Portal Database](portal-db.md)      | portal_db_reader       | no           | no           |


**NOTE: permissions database has been merged with DE database.**

## Install
The installation of this database is manully done on the host `DB_HOST.com'`.
See documentation on [how to install postgresql?](https://www.postgresguide.com/setup/install/)

**Installing postgresql 12 on Centos7**

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

**IPv4 local connections:**

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

### Databases and its Users

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

**This database dedicated to the *iRODS***

* [iRODS Database](irods-db.md)
