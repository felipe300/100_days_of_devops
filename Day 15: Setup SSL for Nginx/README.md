# Day 15: Setup SSL for Nginx

**Objective**: Install and configure Nginx with SSL Certificates.

**Context**: A new Application will be deploy on a server, and you need to use Nginx ans SSL Certificates.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

which nginx # check if nginx is installed
nginx -v # check if nginx is installed
ls /tmp/nautilus.crt # check for nautilus SSL certificate
ls /tmp/nautilus.key # check for nautilus key

yum install -y nginx # install nginx
systemctl enable --now nginx # enable nginx service
which nginx
nginx -v
sudo systemctl status nginx --no-pager # check service status

mkdir -p /etc/nginx/ssl # create "ssl" folder under nginx
mv /tmp/nautilus.crt /tmp/nautilus.key /etc/nginx/ssl/ # move .crt and .key files
chmod 600 stc/nginx/ssl/nautilus.key # give permission to key
vi /etc/nginx/nginx.conf # update nginx config file
sudo nginx -t # check syntax
vi /usr/share/nginx/html/index.html # edit the content of the file
sudo systemctl restart nginx # restart the service
sudo ss -lntp | grep ':443' # check if nginx is listening on port (443)

exit

curl -Ik https://[SERVER] # check if it's running (stapp01)
curl k https://[SERVER] # you will get the content of the index.html : "Welcome!"
```

- `/etc/nginx/nginx.conf`

```bash
server {
    listen              443 ssl;
    server_name         _;

    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    root /usr/share/nginx/html;
    index index.html;
}
```

**NOTE**:

- check that you are using `https` instead of `http`, because you are now using SSL certificates
- In the curl you just need to check if the server is running
- use the tag `-I` to only get the headers
- use the tag `k` to allow "insecure" certificate, most of the time this is used to test or prototyping
