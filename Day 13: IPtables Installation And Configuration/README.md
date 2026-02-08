# Day 13: IPtables Installation And Configuration

**Objective**: Rise security by adding Firewalls and Restricting ports

**Context**: Apache port is open for all request which is a big vulnerability. The port should be open only for "Nautilus HTTP LBR" (Load Balancer).

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"
yum install -y ip-tables-services # install ip-tables-services
systemctl enable iptables # enable service
systemctl start iptables # start service
systemctl status iptables --no-pager # status service

iptables -L -n # List tables, check port (8084) is not here
ss -tlun [PORT] | grep [PORT] # check port, everyone can access it

# Add variables
APACHE_PORT=8084 # Apache port
LBR_IP=172.16.238.14 # Load balancer ip

iptables -I INPUT 1 -p tcp -s $LBR_IP --dport $APACHE_PORT -m state --state NEW -j ACCEPT # allow traffic
iptables -I INPUT 2 -m state --state ESTABLISHED,RELATED -j ACCEPT # Accept established connections
iptables -A INPUT -p tcp --dport $APACHE_PORT -j DROP # Block the rest of the traffic
iptables -L INPUT -n --line-numbers # check changes
service iptables save # save changes

exit
curl http://stapp0x:[PORT] # Check if port (8084) is working in server (stlb01, stapp01, stapp02, and stapp03)
```

**NOTE**: Check the port and the server, at least you have to make the changes in three servers, and test in three servers ans the Load Balancer.
