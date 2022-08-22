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

**TODO**