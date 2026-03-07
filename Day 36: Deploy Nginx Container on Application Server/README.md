# Day 36: Deploy Nginx Container on Application Server

**Objective**: Deploy a Nginx Image

**Context**:

**Steps**:

```sh
ssh [user]@[hostname]
sudo su -

docker images # list current download images
docker pull nginx:alpine # Get image from docker hub
docker run --name [CONTAINER_NAME] -p 8081:80 -d nginx:alpine # run container with name (nginx_3)
docker ps # check running containers

exit
```

**Notes**
