# Day 45: Resolve Dockerfile Issues

**Objective**: Perform a "surgical fix" on the existing `Dockerfile`. Identify why the command `docker build -t <image_name> .` is failing and correct the instructions without altering the core intent of the original developer.

**Context**: The development team has handed over a set of requirements to the DevOps team to containerize an application. One of your colleagues started the work but ran into errors during the build stage. In a real-world DevOps environment, this happens often when a `Dockerfile` is written with syntax errors, incorrect paths, or missing dependencies.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

cd /opt/docker/
ls # you will get "Dockerfile", "html", and "certs"
docker build . # get errors
cat Dockerfile

systemctl status docker --no-pager
systemctl status httpd --no-pager # I got "Unit apache.service could not be found."
yum install -y httpd
systemctl enable now httpd

# update the Dockerfile
vi Docker file

docker build -t [TAG_NAME] . # create an image with a tag "httpd"
docker run -d [TAG_NAME]
docker ps

docker inspect [CONTAINER_ID] | grep "IPAddress" # you will get something like "9175339fa3e2"
curl -I http://[IP_ADDRESS]:[PORT] # in this case is 8080

exit
```

```Dockerfile
FROM httpd:2.4.43

RUN sed -i "s/Listen 80/Listen 8080/g" /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule\ ssl_module\ modules\/mod_ssl.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

RUN sed -i '/LoadModule\ socache_shmcb_module\ modules\/mod_socache_shmcb.so/s/^#//g' /usr/local/apache2/conf/httpd.conf

RUN sed -i '/Include\ conf\/extra\/httpd-ssl.conf/s/^#//g' /usr/local/apache2/conf/httpd.conf

COPY ./certs/server.crt /usr/local/apache2/conf/server.crt

COPY ./certs/server.key /usr/local/apache2/conf/server.key

COPY ./html/index.html /usr/local/apache2/htdocs/
```

**NOTE**:

- In line 3 the path is wrong, the path should be `/usr/local/apache2/conf/httpd.conf`

When I did `cat Dockerfile` I notice a couple of tools and services like `sed` and `httpd (Apache)`. So I tried looking if these tools where installed and working properly
