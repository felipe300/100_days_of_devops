# Day 9: MariaDB Troubleshooting

**Objective**: Check the current state of MariaDB and identity the root issue.

**Context**: Some of the applications can not connect with the database.

**Steps**:

```sh
ssh peter@stdb01 # login to database
sudo systemctl status [SERVICE_NAME]
sudo systemctl status mariadb # Check current status
sudo systemctl restart [SERVICE_NAME] # restart service

# Here it tells you to check "sudo journalctl -xeu mariadb.service"

sudo journalctl -xeu [SERVICE_NAME.service]
sudo journalctl -xeu mariadb.service # Check the journal logs

# Here it tells you to check "/var/lib/mysql" is not empty and have the right permissions
cd /var/lib/
# mysql do not exits only mysqld (they are not the same), so you need to created
sudo mkdir mysql
sudo chown -R mysql:mysql /var/lib/mysql # change group and owner

sudo systemctl restart mariadb
sudo systemctl status mariadb
exit
```

**NOTE**: The flow start with `systemctl status` and `systemctl restart`, just follow the instruction. You can use `sudo su` and enter the password, this allows you to avoid the `sudo` word for each command.
