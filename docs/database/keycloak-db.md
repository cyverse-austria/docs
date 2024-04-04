# Keycloak Database

This Database is used for Keycloak.

## Initialize database

### Access Database

```bash
ssh root@DB_HOST.com
psql -U postgres
```

### Create required Database and User

```bash
# create keycloak user
create user keycloak with password '********';

# create keycloak database
create database keycloak with owner keycloak;
```

### Migrate Database

There is no need to touch the database to migrate to newer version of Keycloak, since the migration happens automaticly with upgrading the version of Keycloak.


### Backup Database

To backup the database we will use the [pg_dump](https://www.postgresql.org/docs/current/app-pgdump.html), make sure this plugin is installed.

```bash
#       -U user  -d database
pg_dump -U keycloak -d keycloak > keycloak.sql
```

### Issues
Sometimes the login via SSO - requires you to again add your existing data, and adding it again throws an error because its already saved in the database.
you can remove the entry and try again to login with SSO.
```bash
keycloak=# DELETE FROM federated_identity WHERE federated_username='mb1990';
```
