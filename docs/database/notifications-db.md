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

### Populate / Migrate the Database

Ensure the following before running the command:
- Docker is installed on your host machine.
- The host has network access to the target PostgreSQL database.

Clone the migration repository:

```bash
git clone https://github.com/cyverse-austria/notifications-db.git
```

Run the migrations using Docker:

```bash
docker run --rm \
  -v $(pwd)/notifications-db/migrations:/migrations \
  --network host \
  migrate/migrate \
  --database "postgres://de:$DE_PASSWORD@$DB_HOST/notifications?sslmode=disable" \
  -path /migrations \
  up
```
