# QMS Database

This Database is used for CyVerse QMS service.

## Initialize database

### Access vm

```bash
ssh root@DB_HOST.com
```

### Create required Database

```bash
# create qms database with de owner
create database qms with owner de;
```

### Add required extensions

```bash
# psql -U postgres
\c de
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
create extension "insert_username";
```

### Populate Database

**TODO**


### Migrate Database

**TODO**