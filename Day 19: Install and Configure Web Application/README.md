# Day 19: Install and Configure Web Application

**Objective**: Get the servers ready to deploy a couple of static websites

**Context**: The Team is currently working on couple of static websites, but first you need to get the servers ready.

**Steps**:

App Servers

```sh
ssh [user]@[hostname]
sudo su -

which ss
which netstat

ss -lntp | grep [PORT] # Check which service is using [PORT] (8088)

yum install -y httpd
# edit the file(s) /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/
grep -r "Listen" /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/ # Check which port is using httpd
vi /etc/httpd/conf/httpd.conf /etc/httpd/conf.d/ # change port from 80 to 8088
sed -i 's/Listen 80/Listen [PORT]/' /etc/httpd/conf/httpd.conf # OR you can change the port (8088) with sed

systemctl enable --now httpd
systemctl status httpd --no-pager
# OR
systemctl is-active httpd

# After copy the files from JumpHost

ls /home/[user] # check if the files came from JumpHost
mv [DIRECTORY] /var/www/html/
cd /var/www/html/

exit
```

JumpHost

```sh
scp -r [SOURCE_DIRECTORY] [user]@[hostname]:[DESTINY_DIRECTORY] # copy files from "Server" to "JumpHost"
curl http://[hostname]:[PORT]/[DIRECTORY] # you will get "301 Moved Permanently"
curl -L http://[hostname]:[PORT]/[DIRECTORY]
```

**NOTES:**

- To move files between servers use `scp`
  - this command use `SSH` protocol
  - `-r`, means recursive, so "copy all files inside"
- In `curl`, use the flag `-L`, in case that the "files" were moved
- the difference between `systemctl is-active XXX`, and `systemctl status XXX` is the response
  - `systemctl is-active`, return a simple output and a code report, `0` or `1`
  - `systemctl status`, return a full state of the service
