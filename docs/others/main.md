# Post-Deployment Steps


## 1. Post-Deployment iRODS

### Gain Access to the Host and Switch to the iRODS Admin User

```bash
ssh <irods_user>@IRODS.HOST
sudo su - irods
```

### Grant Ownership of /TUG/home/shared to rodsadmin
Ensure that rodsadmin owns the specified directory:
```bash
ichmod own rodsadmin /TUG/home/shared
```

### Grant Read Access to Public
Grant public read access to the home and shared directories:

```bash
ichmod read public /TUG/home
ichmod read public /TUG/home/shared
```

### Create iRODS Account for portal
To create the user portal and set the password:
```bash
iadmin mkuser portal rodsadmin
iadmin moduser portal password PORTAL_PASSWORD
```

### Add portal to the rodsadmin Group
Add the portal user to the rodsadmin group:

```bash
iadmin atg rodsadmin portal
```


## 2. Grant `icat_reader` Database Permissions
To grant the `icat_reader` user the necessary database permissions, run the following SQL command:

```sql
--- \c ICAT
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA "public" TO icat_reader;
```


## 3. Add User to Admin Group (LDAP)
Follow these steps to add an existing user to the de-admins group in LDAP.

### Step 1: Create a LDIF File to Add the User
Create an LDIF file named `add-de_admins.ldif` to add a user to the `de-admins` LDAP group. Replace `YOUR_USER_NAME` with the actual username of the user you want to add.


```ldif
dn: cn=de_admins,ou=Groups,dc=tugraz,dc=at
changetype: modify
add: memberuid
memberuid: YOUR_USER_NAME
```

### Step 2: Run the LDAP Modify Command

Run the following command to apply the changes and add the user to the LDAP group:

```bash
read -s PASSWORD && export PASSWORD
ldapmodify -x -D "cn=Manager,dc=tugraz,dc=at" -w $PASSWORD -f add-de_admins.ldif
```
