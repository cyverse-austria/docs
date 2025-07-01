# DE Database

This Database is used for CyVerse discovery environment.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
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

### Populate / Migrate the Database

Ensure the following before running the command:
- Docker is installed on your host machine.
- The host has network access to the target PostgreSQL database.

Clone the migration repository:

```bash
git clone https://github.com/cyverse-austria/de-database.git
```

Run the migrations using Docker:

```bash
docker run --rm \
  -v $(pwd)/de-database/migrations:/migrations \
  --network host \
  migrate/migrate \
  --database "postgres://de:$DE_PASSWORD@$DE_HOST/de?sslmode=disable" \
  -path /migrations \
  up
```

### Additional database queries

```bash
# checkout to de user
psql -U de


SET search_path = public, pg_catalog;

# create table version 
CREATE TABLE version (
version character varying(20) NOT NULL,
applied timestamp DEFAULT now()
);

# populate the Version table from a file
# location of 999_version.sql: 
# https://github.com/cyverse-de/de-database/edit/master/old-databases/de-db/src/main/data/999_version.sql
psql -U postgres -h localhost -d de -f 999_version.sql
```
