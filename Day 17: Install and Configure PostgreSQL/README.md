# Day 17: Install and Configure PostgreSQL

**Objective**: Install and configure PostgreSQL

**Context**: The team are planning to deploy a new application. This application uses PostgreSQL as a database, which is already installed on the DB Server.

**Steps**:

```sh
ssh [user]@[server] # Login to Server 1
sudo su -

postgres --version # check current version and if installed
systemctl status postgresql --no-pager # check status
systemctl enable --now postgresql # enable and start
systemctl restart postgresql # restart the server
pg_isready # postgres utility, to now if it OK

# Log in postgres
sudo -u postgres psql

exit
```

```sql
-- user: kodekloud_sam, password: dCV3szSGNA
CREATE USER [MY_USER] WITH PASSWORD '[SECRET_PASSWORD]';
DROP USER [MY_USER];

-- database: kodekloud_db3
CREATE DATABASE [DATABASE];
DROP DATABASE [DATABASE];

-- grant full permission
GRANT ALL PRIVILEGES ON DATABASE [DATABASE] TO [MY_USER];
```

```bash
sudo -u postgres createuser --interactive # create a user, enter a username, example ["dev_user"]
sudo -u postgres createdb my_database # create database
sudo -u postgres createdb -O dev_user my_database # create a database for this user with full privileges
sudo -u postgres dropuser dev_user # drop database
```

**NOTES**

- `pg_isready` response `/var/run/postgresql:5432 - accepting connections` means you are good to go, else `no response` means the service is down or blocked.
- You can use both way from inside Postgres or from the terminal. Think of it like this: Terminal commands are for automation and speed, while SQL (inside Postgres) is for precision and deep configuration.
