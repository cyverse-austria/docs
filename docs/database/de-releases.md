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

### Populate / Migrate the Database

Ensure the following before running the command:
- Docker is installed on your host machine.
- The host has network access to the target PostgreSQL database.

Clone the migration repository:

```bash
git clone https://github.com/cyverse-de/mgmt.git
```

Run the migrations using Docker:

```bash
docker run --rm \
  -v $(pwd)/mgmt/db/migrations:/migrations \
  --network host \
  migrate/migrate \
  --database "postgres://de:$DE_PASSWORD@$DE_HOST/de_releases?sslmode=disable" \
  -path /migrations \
  up
```

*Note: Replace $DE_USER, $DE_PASSWORD, and $DE_HOST with the appropriate environment variables or values.*
