# Additional Instructions

## Add password for default Postgres User

1. Login with default user:
```
sudo -u postgres psql
```
2. Run the following command to add a password to default Postgres User:
```
ALTER USER username WITH ENCRYPTED PASSWORD 'newpassword';
```

## Configuring pg_hba.conf file

1. Locate file in */var/lib/postgres/data*

2. Change authentication method for local:
```
# before 
TYPE     DATABASE   USER    ADDRESS     METHOD
local    all        all                 peer
# after
TYPE     DATABASE   USER    ADDRESS     METHOD
local    all        all                 md5 
```

## Logging in

1. Use the following command with username
```
psql -U username -d database
```