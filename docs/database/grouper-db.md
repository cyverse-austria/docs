# Grouper Database

This Database is used for CyVerse Grouper service.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
psql -U postgres
```

### Create required Database and User

```bash
## create grouper user
create user grouper with password '********';

## create grouper database
create database grouper with owner grouper;
```

### Add required extensions

```bash
# psql -U postgres
\c grouper
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**