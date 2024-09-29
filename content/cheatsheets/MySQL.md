---
title: MySQL
tags:
  - cheatsheet
---

# MySQL

## User Management

### Create User

```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
CREATE USER 'username'@'129.12.12.192' IDENTIFIED BY 'password';
CREATE USER IF NOT EXISTS 'username'@'%' IDENTIFIED BY 'XXXXXXXX';
```

### Delete user

`DROP USER 'username'@'localhost';`

### Check User's Priviledges

```
SHOW GRANTS FOR 'cloudsqlsuperuser'
SHOW GRANTS FOR 'root'@'%';
SHOW GRANTS FOR 'root'@'localhost'
```

### Grant Users Permissions on a certain database

```
CREATE DATABASE test
GRANT ALL PRIVILEGES ON test.* TO 'username'@'localhost';

# Read Only permissions only
GRANT SELECT, SHOW VIEW ON test.\* TO 'username'@'%';
```

### See all users and their host

` SELECT User, Host FROM mysql.user;`

## Joins

to be continued...
