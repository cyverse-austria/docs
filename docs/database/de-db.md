# DE Database

This Database is used for CyVerse discovery environment.

## Initialize database

### Access Database

```bash
ssh root@cy-db01.tugraz.at
psql -U postgres
```

### Create required Database and User

```bash
# create de user
create user de with password '********';

# create de database
create database de with owner de;
```

### Add required extensions

```bash
# psql -U postgres
\c de
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**
