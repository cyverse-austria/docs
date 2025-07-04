# Post-Deployment Steps


## 1. Post-Deployment iRODS

### Gain Access to the Host and Switch to the iRODS Admin User

```bash
ssh <irods_user>@IRODS.HOST
sudo su - irods
```

### Create iRODS Account for de-irods

To create the user de-irods and set the password:
```bash
iadmin mkuser de-irods rodsadmin
iadmin moduser de-irods password DE_USER_PASSWORD
```

### Add de-irods to the rodsadmin Group

Add the user de-irods to the rodsadmin group:
```bash
iadmin atg rodsadmin de-irods
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

### Grant `icat_reader` Database Permissions

To grant the `icat_reader` user the necessary database permissions, run the following SQL command:

```sql
--- \c ICAT
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA "public" TO icat_reader;
```

## 2. Post-Deployment DE(Discovery Environment)

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

### Add User to Admin Group (LDAP)

Follow these steps to add an existing user to the de-admins group in LDAP.

#### Step 1: Create a LDIF File to Add the User

Create an LDIF file named `add-de_admins.ldif` to add a user to the `de-admins` LDAP group. Replace `YOUR_USER_NAME` with the actual username of the user you want to add.

```ldif
dn: cn=de_admins,ou=Groups,dc=tugraz,dc=at
changetype: modify
add: memberuid
memberuid: YOUR_USER_NAME
```

#### Step 2: Run the LDAP Modify Command

Run the following command to apply the changes and add the user to the LDAP group:

```bash
read -s PASSWORD && export PASSWORD
ldapmodify -x -D "cn=Manager,dc=tugraz,dc=at" -w $PASSWORD -f add-de_admins.ldif
```

### ✅ Create Anonymous User Workspace for Apps

Ensure that your **LDAP** configuration includes an `anonymous` user and that this user is added to the `everyone` group.

---

#### 🐳 Run a Temporary Debian Container in Your Namespace

```bash
kubectl -n $NAMESPACE run testing \
  --rm -it \
  --image=debian:stable-slim \
  -- bash
```

#### Install `curl` Inside the Container

```bash
apt-get update && apt-get install curl
```

#### Trigger Workspace Creation for the Anonymous User

```bash
curl "http://apps/bootstrap?user=anonymous"
```


# User Provisioning: iRODS + LDAP

This guide explains how to create a new user in both **iRODS** and **OpenLDAP**, including group membership and password setup.

---

## 1. Create iRODS User Account

Run the following commands as an iRODS administrator:

```bash
iadmin mkuser user01 rodsuser
iadmin moduser user01 password user01password
```
This creates an iRODS user `user01` with the type `rodsuser` and sets the password to `user01password`.

## 2. Create LDAP User Account

### Step 1: Create an LDIF file for the new user
Example: `testuser.ldif`

```ldif
dn: uid=user01,ou=People,dc=tugraz,dc=at
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: user01
uidNumber: 40005
gidNumber: 10009
homeDirectory: /home/user01
mail: user01@cyverse.at
sn: surname
givenName: Test
cn: Test Surname
title: University/College Staff
o: Graz University of Technology
```

### Step 2: Add the user to LDAP
```bash
ldapadd -x -D "cn=Manager,dc=tugraz,dc=at" -w "$MANAGER_PASSWORD" -f testuser.ldif
```

## 3. Set LDAP Password for the User
```bash
ldappasswd -x \
  -D "cn=Manager,dc=tugraz,dc=at" \
  -w "$MANAGER_PASSWORD" \
  -s "user01password" \
  "uid=user01,ou=People,dc=tugraz,dc=at"
```

## 4. Add User to everyone Group

### Step 1: Create an LDIF file for group modification
Example: `add-everyone.ldif`

```ldif
dn: cn=everyone,ou=Groups,dc=tugraz,dc=at
changetype: modify
add: memberuid
memberuid: user01
```

### Step 2: Apply the group modification
```bash
ldapmodify -x -D "cn=Manager,dc=tugraz,dc=at" -w "$MANAGER_PASSWORD" -f add-everyone.ldif
```

## 5. Add User to community Group

### Step 1: Create an LDIF file for group modification
Example: `add-community.ldif`

```ldif
dn: cn=community,ou=Groups,dc=tugraz,dc=at
changetype: modify
add: memberuid
memberUid: user01
```

### Step 2: Apply the group modification
```bash
ldapmodify -x -D "cn=Manager,dc=tugraz,dc=at" -w "$MANAGER_PASSWORD" -f add-community.ldif
```
