# Day 14: Linux Process Troubleshooting

**Objective**: Check that Apache is working properly on specific Port

**Context**: the system monitoring service has detected that Apache(httpd) is not working properly.

**Steps**:

```sh
ssh [user]@[hostname]
su - # to avoid using sudo and enter the password multiple times. Work as a "super user"
systemctl status httpd --no-pager # check current status
netstat -lntp | grep ":[PORT]" # check if port is being used (8088), sendmail is using it

systemctl stop sendmail
systemctl disable sendmail

systemctl stop sendmail.socket 2>/dev/null || true # For security, this will stop the socket if exists
systemctl disable sendmail.socket 2>/dev/null || true # For security, this will stop the socket if exists
netstat -lntp | grep [PORT] | echo "Port 8088 is free now!" # Check if [PORT] (8088) id free

systemctl start httpd # start Apache service
systemctl enable httpd # enable Apache server
systemctl status httpd --no-pager # check Apache server status

sudo netstat -lntp | grep [PORT] # Check which service is using [PORT] (8088)

sudo grep "^Listen" /etc/httpd/conf/httpd.conf # validate changes
sudo apachectl configtest # syntax check
exit

curl -I http://[SERVER]:[PORT] # check if it's running (stapp01, stapp02, stapp03) on port (8088)
```

**NOTE**:
