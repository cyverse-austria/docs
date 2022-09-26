# Portal Database

This Database is used for CyVerse User portal Service.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
psql -U postgres
```

### Create required Database and User
See also [portal2/setup-database](https://gitlab.com/cyverse/portal2#setup-database)


```bash
# create portal database and user
create user portal_db_reader with password '********';
## create portal database
create database portal with owner portal_db_reader;

## Grant user to member of postgres
# psql -U postgres
GRANT postgres TO portal_db_reader;
```

### Restore from dump
For this we have to download [portal.sql](https://gitlab.com/cyverse/portal2/-/blob/master/portal.sql) file.

```bash
# restor to user portal_db_reader and database portal
psql -U portal_db_reader -d portal -f portal.sql
```

### Populate Database (PENDING)
We need to populate this database, with:
* GRID
* required Tables


**TODO**

### Migrate Database

**TODO**