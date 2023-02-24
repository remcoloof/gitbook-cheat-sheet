# Duplicate database

## Instructions

### SQL

Run the following command.

```
CREATE DATABASE newdb WITH TEMPLATE originaldb OWNER dbuser;
```

Note that the database should not be accessed by other users. To make the command above work we need to disconnect all users. Therefore, this method is not suited to clone a production database. Nevertheless, if you want to disconnect all other users run the following query.

```
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity 
WHERE pg_stat_activity.datname = 'originaldb' AND pid <> pg_backend_pid();
```

### pgAdmin 4 GUI

It is also possible to use the interface of pgAdmin 4. To clone a database you first need to make a backup of the source database by right clicking the database, Backup... and store to a file. Next, create a destination database. After creating this database right click, Restore... and select the backup file. The destination database should now contain a copy of the source database.

### psql

Also possible, but did not get this working yet.

## Resources

* [https://stackoverflow.com/questions/876522/creating-a-copy-of-a-database-in-postgresql](https://stackoverflow.com/questions/876522/creating-a-copy-of-a-database-in-postgresql)&#x20;
