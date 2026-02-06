# Day 11: Install and Configure Tomcat Server

**Objective**: Install and config Java Tomcat

**Context**: The developer team finished a beat java app. to deploy it it was decided to use Tomcat.

**Steps**:

```sh
ls /tmp # in server jumhost there is an artifact ROOT.war
ssh [user]@[hostname]
sudo yum install -y tomcat # install tomcat
sudo systemctl enable --now tomcat # enable tomcat server
ls /etc/tomcat # here are stored the tomcat files
cat /etc/tomcat/server.xml # edit the "Connector port 6300"
sudo systemctl restart tomcat # restart the server
sudo systemctl status tomcat --no-pager # check status
exit

scp /tmp/ROOT.war [user]@stapp0x:/tmp/ # on jumhost

ssh [user]@[hostname]
sudo rm -rf /var/lib/tomcat/webapps/ROOT /var/lib/tomcat/webapps/ROOT.war # delete old artifact
sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/ROOT.war # move new artifact from jumhost to server app 2
sudo chown tomcat:tomcat /var/lib/tomcat/webapps/ROOT.war # change user and group to tomcat
sudo systemctl restart tomcat # restart tomcat server
exit

curl http://stapp0x:xxxx # check if connection is ok
```

- `etc/tomcatserver.xml`

```sh
<Connector port="6300" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```

**NOTE**:
