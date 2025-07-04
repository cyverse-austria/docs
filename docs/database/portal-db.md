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
# create user
create user portal_db_reader with password '********';

# create portal database with the owner portal_db_reader
create database portal with owner portal_db_reader;

## Grant user to member of postgres
# psql -U postgres
GRANT postgres TO portal_db_reader;
```

### Populate / Migrate the Database

Ensure the following before running the command:
- Docker is installed on your host machine.
- The host has network access to the target PostgreSQL database.

Clone the migration repository:

```bash
git clone https://github.com/cyverse-austria/portal2.git
```

Run the migrations using Docker:

```bash
docker run --rm \
  -v $(pwd)/portal2/migrations:/migrations \
  --network host \
  migrate/migrate \
  --database "postgres://$PORTAL_USER:$PORTAL_PASSWORD@$DB_HOST/portal?sslmode=disable" \
  -path /migrations \
  up
```

### Extra 

#### Give Admin privilege to a user

```sql
--update is_superuser
UPDATE account_user SET is_superuser = true WHERE username='USERNAME';

---update is_staff 
UPDATE account_user SET is_staff = true WHERE username='USERNAME';
```

#### Verify User email

```sql
-- check if its verified
select has_verified_email from account_user where username='USERNAME';

--Verify email
UPDATE account_user SET has_verified_email = true WHERE username='USERNAME';
```

#### Insert Services

by default the table `api_service` will be empty, in order to add a new service, we will to INSERT INTO the database.

For this we need to add first the `api_servicemaintainer` column, and then `api_service` -
as an example we will be adding a DE(Discovery environment) service.

```sql
-- check the tables content
select * from api_servicemaintainer;
select * from api_service;

-- First Insert into api_servicemaintainer
-- save the id of this record - which we will use in the next step
INSERT INTO api_servicemaintainer (name, website_url, created_at, updated_at) VALUES ('CyVerse', 'https://cyverse.tugraz.at', now(), now());

-- Second Insert into api_service
INSERT INTO api_service (name, description, about, service_url, is_public, icon_url, created_at, updated_at, service_maintainer_id, approval_key, subtitle) VALUES ('Discovery Environment', 'Use hundreds of bioinformatics apps and manage data in the CyVerse Data Store from a simple web interface', 'By providing a consistent user interface for access to the tools and computing resources needed for specialized scientific analyses, the Discovery Environment facilitates data exploration and scientific discovery.\r', 'https://de.cyverse.at/de', true, 'https://user.cyverse.at/assets/images/de.png', now(), now(), 3, 'DISCOVERY_ENVIRONMENT', '');

```

#### Insert Restricted Username (PENDING)

```sql
INSERT INTO account_restrictedusername (username, created_at, updated_at) VALUES ('username', now(), now());
```

#### make sure session Table exist

```bash
CREATE TABLE public.session (
    sid character varying NOT NULL,
    sess json NOT NULL,
    expire timestamp(6) without time zone NOT NULL
);
ALTER TABLE public.session OWNER TO portal;
CREATE INDEX "IDX_session_expire" ON public.session USING btree (expire);
```

#### Import GRID institutions

##### download required grid file

[Official website](https://digitalscience.figshare.com/articles/dataset/GRID_release_2021-09-16/16685428?backTo=/collections/GRID/3812929)

```bash
# download grid
wget https://digitalscience.figshare.com/ndownloader/files/30895309

# unzip
unzip 30895309
```

##### import to the database
For imorting this grid file we will use the script from [portal2/scripts/import_grid_institutions.py](https://gitlab.com/cyverse/portal2/-/blob/master/src/scripts/import_grid_institutions.py).

```bash
./import_grid_institutions.py --host root@DB_HOST.com --user portal_db_reader --database portal grid.csv
```

#### Populate these Tables
**These sql files can be found [here](https://github.com/cyverse-austria/portal2-db)**.

```bash
psql -U portal_db_reader -d portal -f ./account_country.sql
psql -U portal_db_reader -d portal -f ./account_region.sql
psql -U portal_db_reader -d portal -f ./account_gender.sql
psql -U portal_db_reader -d portal -f ./account_occupation.sql
psql -U portal_db_reader -d portal -f ./account_ethnicity.sql
psql -U portal_db_reader -d portal -f ./account_fundingagency.sql
psql -U portal_db_reader -d portal -f ./account_awarechannel.sql
psql -U portal_db_reader -d portal -f ./account_researcharea.sql
```


### Creating an iRODS Account for the Portal Service

To create an iRODS account for the Portal service, please refer to the documentation:

🔗 [Create iRODS Account for Portal](https://cyverse-austria.github.io/docs/others/main/#create-irods-account-for-portal)
