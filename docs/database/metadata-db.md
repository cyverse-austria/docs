# Metadata Database

This Database is used for CyVerse Metadata service.

## Initialize database

### Access Database

```bash
ssh root@cy-db01.tugraz.at
psql -U postgres
```

### Create required Database

```bash
# create metadata database with de user
create database metadata with owner de;
```

### Add required extensions

```bash
# psql -U postgres
\c metadata
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**