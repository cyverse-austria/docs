# Unleash Database

This Database is used for CyVerse Unleash service.

## Initialize database

### Access vm

```bash
ssh root@cy-db01.tugraz.at
```

### Create required Database and User

```bash
# create unleash user
create user unleash with password '********';

# create unleash databased
create database unleash with owner unleash;
```

### Add required extensions

```bash
# psql -U postgres
\c unleash
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**