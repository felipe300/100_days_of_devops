# Day 12: Linux Network Services

**Objective**: Fix Apache ports

**Context**: The monitoring reports that Apache service is down in a specific App Server.

**Steps**:

```sh
curl http://stapp01:8088 # Check if page is running
ssh [user]@[hostname]
sudo systemctl status httpd --no-pager # Check if apache is down, also confirm error. Status "failed"
# Look for the first line of the error: (98)Address already in use: AH00072: make_sock: could not bind to….0:8088
sudo netstat -lntp | grep [PORT] # Check which service is using [PORT] (8088)
sudo systemctl stop sendmail # stop service sendmail
sudo systemctl disable sendmail # disable service sendmail

sudo systemctl stop sendmail.socket 2>/dev/null || true # For security, this will stop the socket if exists
sudo systemctl disable sendmail.socket 2>/dev/null || true # For security, this will stop the socket if exists
sudo netstat -lntp | grep [PORT] | echo "Port 8088 is free now!" # Check if [PORT] (8088) id free

sudo systemctl start httpd # start apache service
sudo systemctl enable httpd # enale apache server
sudo systemctl status httpd --no-pager # check apache server status

sudo netstat -lntp | grep [PORT] # Check which service is using [PORT] (8088)

sudo iptables -L -n # Check the list of iptables, only port 22 is allow
sudo iptables -I INPUT 1 -p tcp --dport [PORT] -j ACCEPT # allows port [PORT] (8088)
sudo iptables -D INPUT -p tcp --dport [PORT] -j ACCEPT # disallow port [PORT] (8088)
sudo iptables -L INPUT -n --line-numbers # Show your port at the top

exit
curl http://stapp01:8088 # Check if page is running
```

**NOTE**:
