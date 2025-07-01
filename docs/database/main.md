# Databases

CyVerse is using [PostgreSQL](https://www.postgresql.org/) as its database.

**Most of These database dedicated to the *discovery environment* of Cyverse, which is used for multiple services such as:**

| Database      | Owner    | Auto Init    | Auto Migrate |
| ------------- | -------- | ------------ | ------------ |
| [de Database](de-db.md)            | de       | no           | no           |
| [Notifications Database](notifications-db.md) | de       | no           | no           |
| [Metadata Database](metadata-db.md)      | de       | no           | no           |
| [DE Releases](de-releases.md)   | de       | no           | no           |
| [Grouper Database](grouper-db.md)       | grouper  | yes          | ?            |
| [QMS Database](qms-db.md)           | de       | configurable | configurable |
| [Unleash Database](unleash-db.md)       | unleash_user       | yes          | ?            |
| [Keycloak Database](keycloak-db.md)      | keycloak | yes          | ?            |
| [Portal Database](portal-db.md)      | portal_db_reader       | no           | no           |

**NOTE: permissions database has been merged with DE database.**

## Setup
On this paragraph  we will cover first and necessary steps to configure the database.

### ~postgres/12/data/pg_hba.conf

**IPv4 local connections:**

Add IP or IP range of kubernetes worker node, that requires connection to this database.

| TYPE | DATABASE | USER | ADDRESS | METHOD |
|------|----------|------|---------|--------|
|host  |all       | all  | *******/32 |md5   |


### ~postgres/12/data/postgresql.conf

```bash
# vi ~postgres/12/data/postgresql.conf
listen_addresses = '*'          # what IP address(es) to listen on;
```

**This database dedicated to the *iRODS***

* [iRODS Database](irods-db.md)

| Database      | Owner    | Auto Init    | Auto Migrate |
| ------------- | -------- | ------------ | ------------ |
|  [iRODS Database](irods-db.md)  | icat_reader & irods       | no           | no           |
