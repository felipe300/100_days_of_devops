# Day 18: Configure LAMP server

**Objective**: Host a WordPress site inside a server

**Context**: The team has already done some infrastructure configuration on the server. But there are some task to be done, yet.

**Steps**:

App Servers

```sh
ssh [user]@[hostname]
sudo su -

cat /var/www/html/index.php # Check the credentials of the file

systemctl is-active ss
systemctl is-active netstat

ss -lntp | grep [PORT] # Check which service is using [PORT] (8088)

yum install -y httpd
# edit the file(s) /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/
grep -r "Listen" /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/ # Check which port is using httpd
vi /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/ # change port from 80 to 8088
sed -i 's/Listen 80/Listen [PORT]/' /etc/httpd/conf/httpd.conf # OR you can change the port (8088) with sed

systemctl enable --now httpd
systemctl status httpd --no-pager

# install php
yum install -y php php-mysqlnd php-fpm
systemctl restart httpd
exit
```

DB Server

```sh
ssh [user]@[hostname]
sudo su -

yum install -y mariadb-server

systemctl enable --now mariadb
systemctl status mariadb --no-pager
mysql_secure_installation
mysql

exit
```

Database

Credentials comes from your project setup.

```sql
CREATE DATABASE [DATABASE_NAME];
CREATE DATABASE kodekloud_db10;
CREATE USER '[USERNAME]'@'%' IDENTIFIED BY '[PASSWORD]';
CREATE USER 'kodekloud_rin'@'%' IDENTIFIED BY 'BruCStnMT5';
GRANT ALL PRIVILEGES ON [DATABASE_NAME].* TO '[USERNAME]'@'%';
GRANT ALL PRIVILEGES ON kodekloud_db10.* TO 'kodekloud_rin'@'%';
FLUSH PRIVILEGES;
```

**NOTES:**

- make the `httpd`, and `php` installation for `stapp01`, `stapp02`, and `stapp03`
- use `systemctl is-active XXX` to check if a service is active or not.
- you can use either "`ss`" or "`netstat`"
- check the page `https://80-port-uwtjepo6w2xgfako.labs.kodekloud.com/` by click in the "App" button.
