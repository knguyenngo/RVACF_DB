# RVACF DB

## Setup
### Arch Linux

**Installation**

1. Install PostGreSQL from official repo:
```
sudo pacman -S postgresql
```
2. Verify installation:
```
postgre --version
```

**Configuration**

1. Switch to Postgres user:
```
sudo -iu postgres
```
2. Default command to initialize the directory where PostgreSQL will store its data (default directory: */var/lib/postgres/data* ):
```
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'
```
3. **Recommended:** Enable data checksums for extra data integrity by adding *--data-checksums*:
```
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data' --data-checksums
```
4. **Recommended:** Change authentication methods for local and remote connections:
```
initdb --locale $LANG -E UTF8 -D 'var/lib/postgres/data' --data-checksums --auth-local=peer --auth-host=scram-sha-256
```
5. Check if data checksums are enabled:
```
psql --tuples-only -c "SHOW data_checksums"
```
6. Command to start database server after successful initialization:
```
pg_ctl -D /var/lib/postgres/data -l logfile start
```

**Enable PostgreSQL Server**

1. Start the PostgreSQL server:
```
systemctl start postgresql
```
2. Check status of server:
```
systemctl status postgresql
```
3. **Optional:** Enable PostgreSQL server to auto-start at boot
```
systemctl enable postgresql
```
4. Stop the PostgreSQL server:
```
systemctl stop postgresql
```

**Creating a new user in PostgreSQL Server**

1. Switch to Postgres default user to directly run SQL commands:
```
sudo -u postgres psql
```
2. Create a new user:
```
CREATE USER username
WITH ENCRYPTED PASSWORD
'password';
```
3. Create a new database (Database will be owned by user executing command):
```
CREATE DATABASE db_name;
```
4. Grant all permissions to desired user on the database:
```
GRANT ALL PRIVILEGES ON DATABASE db_name TO
username;
```
5. To check if database and user was created successfully, run ```\l``` to list all databases and ```\du``` to list all users

