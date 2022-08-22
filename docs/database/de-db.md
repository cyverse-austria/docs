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

### Populate Database
#### Clone de-database repository

```bash
git clone https://github.com/cyverse-de/de-database.git
cd de-database
```
#### install [golang-migrate](https://github.com/golang-migrate/migrate)
These steps are used on **Ubuntu** debian based OS.
```bash
curl -s https://packagecloud.io/install/repositories/golang-migrate/migrate/script.deb.sh | sudo bash
apt-get update
apt-get install -y migrate

# check
migrate -help
```

#### Run to populate de database
**Note**: we are running the `/migration` directory from [de-database](https://github.com/cyverse-de/de-database.git)
```bash
migrate -database postgres://USER:PASSWORD@DB_HOST.com/de?sslmode=disable -path migrations up
```

#### Additional database queries

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

### Migrate Database
Once a while upon updating the k8s services, we would require to migrate the **de-database**, to add the latest database changes.

#### Clone latest de-database

```bash
git clone https://github.com/cyverse-de/de-database.git
cd de-database
```
#### install [golang-migrate](https://github.com/golang-migrate/migrate)
These steps are used on **Ubuntu** debian based OS.
```bash
curl -s https://packagecloud.io/install/repositories/golang-migrate/migrate/script.deb.sh | sudo bash
apt-get update
apt-get install -y migrate

# check
migrate -help
```

#### Run to migrate de database
**Note**: we are running the `/migration` directory from [de-database](https://github.com/cyverse-de/de-database.git)
```bash
migrate -database postgres://USER:PASSWORD@DB_HOST.com/de?sslmode=disable -path migrations up
```
