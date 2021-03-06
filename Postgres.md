### Backup 

```pg_dump -h hostname -p 5432 -U username databasename > your_output_file_path.dmp```

### Restore

``` psql -h hostname -U username -d databasename -f backup_file_path ```

 ### Find the activities connections
 
 ```SELECT * FROM pg_stat_activity WHERE datname = 'target_database' ```
 
 ### Terminate the active connections

``` SELECT pg_terminate_backend (pg_stat_activity.pid) FROM pg_stat_activity WHERE pg_stat_activity.datname = 'target_database' ```

- (Notice that if you use PostgreSQL version 9.1 or earlier, use the procpidcolumn instead of the pidcolumn because PostgreSQL changed procidcolumn to pidcolumn since version 9.2)

### Create database

``` createdb databasename -O owner -U username ```

### Grant privileges on database

``` psql -U postgres -c "GRANT ALL PRIVILEGES ON DATABASE databasename to database_owner" ```

### Drop database

```DROP DATABASE target_database ```

### Create user with read only privilege
``` sql 
SELECT * FROM pg_roles; -- check all users in pg
 CREATE USER your_username WITH PASSWORD 'your_password';
 -- (Switch database you want to)
 GRANT select ON ALL TABLES IN SCHEMA public to your_username;
``` 

### Ref
- [http://www.postgresqltutorial.com/postgresql-drop-database/](http://www.postgresqltutorial.com/postgresql-drop-database/)
