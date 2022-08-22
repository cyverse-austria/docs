# Notifications Database

This Database is used for CyVerse notifications service.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
psql -U postgres
```

### Create required Database

```bash
# create notifications database with de owner.
create database notifications with owner de;
```

### Add required extensions

```bash
# psql -U postgres
\c notifications 
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**

