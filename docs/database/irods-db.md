# iRODS Database

This Database is used for iRODS.

*current postgresql version: 12*.

## Create required Database and User

After installing a postgresql database we would need to create required *users* and *Database*.

```sql
---
-- (ICAT) create database
CREATE DATABASE "ICAT";

-- (icat_reader) This user will access the database from de
CREATE USER icat_reader WITH ENCRYPTED PASSWORD 'YOUR_PASSWORD';
GRANT ALL PRIVILEGES ON DATABASE "ICAT" to icat_reader;

-- (irods) This user will access the database from the Irods server
CREATE USER irods WITH ENCRYPTED PASSWORD 'YOUR_PASSWORD';
GRANT ALL PRIVILEGES ON DATABASE "ICAT" to irods;
```

## Initialize database

The initializing of the iRODS Database is done by [setup_irods.py](https://github.com/CyVerse-Ansible/ansible-irods-cfg/blob/13549b3917dae8d36bb4d4c110ca179cc31e4ee0/tasks/setup_irods.yml#L24C1-L24C35)
