# Metadata Database

This Database is used for CyVerse De Releases.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
psql -U postgres
```

### Create required Database

```bash
# create metadata database with de user
create database de_releases with owner de;
```

### Add required extensions

```bash
# psql -U postgres
\c de_releases 
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
```

### Populate Database

**TODO**

### Migrate Database

**TODO**
