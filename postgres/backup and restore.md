# Backup and Restore

> this assumes you are using the application dbeaver and that you have the postgres.app installed.

## Backup

1. Within dbeaver Edit the driver properties for PostgreSQL and on the Native Client choose 'Add Home'
   and choose the bin folder within the postgres.app. Similar to `/Applications/Postgres.app/Contents/Versions/12/bin`, dbeaver will use the native client tools to perform backups and restores.
2. Right click on the db you want to backup and choose 'Tools > Backup'.

3. Follow the prompts and use the following settings:

	- Format: Custom
	- Encoding: UTF-8
	- Do not backup privileges: true
	- Discard objects owner: true

> A file similar to `dump-go-202005081354.backup` will be in the folder you specified.

## Restore

1. If you havent already done so create a database and user that you want to restore too:
```sql
CREATE DATABASE db;
CREATE USER db_user WITH PASSWORD 'password';
ALTER ROLE db_user SET client_encoding TO 'utf8';
ALTER ROLE db_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE db_user SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE db TO db_user;
```

2. In dbeaver connect to that database using the user you created.

3. Right click on the db and choose 'Tools > Restore'.

4. Follow the prompts and use the following settings:

	- Format: Custom

> The owner of the objects will be the user you have connected with so there is no need for anything further.

