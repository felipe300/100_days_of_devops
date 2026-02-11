# Day 16: Install and Configure Nginx as an LBR

**Objective**: Install and configure Nginx as a Load Balancer (LBR)

**Context**: Traffic to an application managed by team has grown considerably, causing service degradation. As a solution, it was decided to migrate the application to a high-availability architecture, using an Nginx-based HTTP Load Balancer. The migration is already complete, and only the configuration of the LBR (Load Balancer) server remains.

**Steps**:

```sh
# Jumphost
sudo ss -tulpn | grep -E 'apache2|httpd' # check apache port (3002) for Centos
grep "Listen" /etc/httpd/conf/httpd.conf

sudo netstat -tulpn | grep -E 'apache2|httpd' # check apache port (3002) for Debian Ubuntu
grep "Listen" /etc/apache2/ports.conf

# Servers
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

systemctl enable --now httpd
systemctl restart httpd
systemctl status httpd

yum install firewalld
systemctl enable --now firewalld
firewall-cmd --state
firewall-cmd --permanent --add-port=[PORT]/tcp # Configure port (3002) permanently
firewall-cmd --reload

exit

# Load Balancer
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

which nginx # check if nginx is installed
nginx -v # check if nginx is installed

yum install -y nginx # install nginx
systemctl enable --now nginx # enable nginx service, then start it
vi /etc/nginx/nginx.conf # edit nginx.conf file

systemctl restart nginx
systemctl enable --now nginx
systemctl status nginx

# Check connectivity from LBR
curl -I http://172.16.238.10:3002
curl -I http://172.16.238.11:3002
curl -I http://172.16.238.12:3002

curl -I http://localhost

exit
```

- `/etc/nginx/nginx.conf`

```bash
# paste this instead of "server"
upstream nautilus_app {
    server 172.16.238.10:3002
    server 172.16.238.11:3002
    server 172.16.238.12:3002
}

server {
        listen 80;
        server_name _;

        location / {
            proxy_pass http://nautilus_app;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
}
```

**NOTE**:

- Depending on the machine, you will use `ss` (Centos) or `netstat` (Ubuntu)
- The flag `--now`, tells `systemctl` to `enable` the service, and then `start` it, all at once. It's a shortcut.
- Check and install the firewall if is not there.
- The `ip` for "upstream" come from "Nautilus" `ip` list for each server (`stapp`)
