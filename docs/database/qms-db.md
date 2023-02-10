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
\c de
create extension "uuid-ossp";
create extension "moddatetime";
create extension "btree_gist";
create extension "insert_username";
```

### Populate Database

**TODO**


### Migrate Database

Once a while upon updating the k8s services, we would require to migrate the **qms-database**, to add the latest database changes.

#### Clone QMS repo

```bash
git clone https://github.com/cyverse/QMS.git
git fetch && git checkout prod
cd QMS
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

#### Run to migrate QMS database

**Note**: we are running the `/migration` directory from [QMS](https://github.com/cyverse/QMS.git)

```bash
migrate -database postgres://USER:PASSWORD@DB_HOST.com/qms?sslmode=disable -path migrations up
```
