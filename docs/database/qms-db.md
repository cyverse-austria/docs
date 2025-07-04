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
\c qms
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
create extension "insert_username";
```

### Populate / Migrate the Database

Ensure the following before running the command:
- Docker is installed on your host machine.
- The host has network access to the target PostgreSQL database.

Clone the migration repository:

```bash
git clone https://github.com/cyverse-austria/qms.git
```

Run the migrations using Docker:

```bash
docker run --rm \
  -v $(pwd)/qms/migrations:/migrations \
  --network host \
  migrate/migrate \
  --database "postgres://de:$DE_PASSWORD@$DB_HOST/qms?sslmode=disable" \
  -path /migrations \
  up
```

*Note: Replace $DE_USER, $DE_PASSWORD, and $DB_HOST with the appropriate environment variables or values.*
