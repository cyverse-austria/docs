# iRODS Database

This Database is used for iRODS.

*current postgresql version: 12*.

## Create required Database and User

After installing a postgresql database we would need to create required *users* and *Database*.

```sql
---
-- (ICAT) create database
CREATE DATABASE "ICAT";

-- (icat_reader) This user will access the database from discovery environment
CREATE USER icat_reader WITH ENCRYPTED PASSWORD 'YOUR_PASSWORD';
GRANT ALL PRIVILEGES ON DATABASE "ICAT" to icat_reader;

-- (irods) This user will access the database from the iRODS server
CREATE USER irods WITH ENCRYPTED PASSWORD 'YOUR_PASSWORD';
GRANT ALL PRIVILEGES ON DATABASE "ICAT" to irods;
```

## Initialize Database

Database initialization is fully automated and managed through Ansible playbooks, specifically handled by the [`setup_irods.yml`](https://github.com/CyVerse-Ansible/ansible-irods-cfg/blob/main/tasks/setup_irods.yml#L25) task.


## Grant `icat_reader` Database permissions

Run this only after the initialize of **iRODS database**.

```sql
--- \c ICAT
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA "public" TO icat_reader;
```

## Post-Deployment Steps

Also see the [post-iRODS deployment documentation](../others/main.md) for additional configuration steps.
