# Day 20: Configure Nginx + PHP-FPM Using Unix Sock

**Objective**: Install and configure Nginx to work properly with PHP-FPM

**Context**: The development team is planning to launch a new PHP-based application. They need nginx running on a server using Unix Sock.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su

ls /var/www/html/ # Check for files: "index.php" and "info.php"

which nginx # check if nginx is installed

yum install -y nginx # install nginx
vi /etc/nginx/nginx.conf # enter config file and change: Server -> Listen port (8095), and Server -> root (/var/www/html)
nginx -t # check syntax
systemctl enable --now nginx # enable nginx service
nginx -v # check if nginx is installed
sudo systemctl status nginx --no-pager # check service status

whish ss
ss -lntp | grep [PORT] # check and confirm running port (8095)
curl localhost:8095
curl localhost:8095/info.php

cat /etc/os-release # check machine OS, for php-fpm, check if version is 7, or 8/9

php -v # check version
which dnf # You need to install and use "dnf" to install php-fpm
sudo dnf update -y
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm # install EPEL
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm # install REMI

sudo dnf module reset php -y # reset php
sudo dnf module enable php:remi-[VERSION] -y # enable php:remi version (8.1)

sudo dnf install -y php-fpm php-cli php-mysqlnd php-gd php-xml php-mbstring php-json php-opcache # install php
php -v

mkdir /var/run/php-fmp/ # if not exists /php-fpm/default.sock
vi /etc/php-fpm.d/www.conf # edit file conf

systemctl status php-fpm --no-pager
systemctl enable --now php-fpm

vi /etc/nginx/nginx.conf
nginx -t
systemctl reload nginx
curl localhost:8095

exit
```

- `/etc/nginx/nginx.conf`

It is important that the ports match, also under `index` you can add a directory instead of every single file

```bash
server {
        listen       8095;
        listen       [::]:8095;
        server_name  _;
        root         /var/www/html;
        index        index.html index.php info.php
}
```

- `/etc/php-fpm.d/www.conf`

```toml
listen = /run/php-fpm/www.sock # change this line for:
listen = /var/run/php-fpm/default.sock # new line
```

OR you can also change these line to be more precises

```toml
; Change these lines:
user = nginx
group = nginx
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```

- `/etc/nginx/nginx.conf`

```bash
# Add this code block inside "Server"
location ~ \.php$ {
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass unix:/var/run/php-fpm/default.sock;
    fastcgi_index index.php;
    include fastcgi.conf;
}
```

**NOTE**:

- Nginx do not know how to work with `.php` files, so you need to use Unix Sock
- to avoid using `sudo` and enter the password multiple times. Work as a "super user"
