# Day 43: Docker Ports Mapping

**Objective**: Deploy a persistent Nginx web server on Application Server by pulling the stable image and mapping host port to container port within a named container.

**Context**: The DevOps team is planning to host an application on a nginx-based container.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

docker images
docker pull nginx:stable # download nginx-based image stable
docker run -d -p [PORT]:80 --name [NEW_NAME] nginx:stable # name (beta)
docker run -d -p 8087:80 --name beta nginx:stable
docker ps # get container id
docker inspect [CONTAINER_NAME] | grep "HostPort" # (beta), get port number (8087)
docker inspect --format='{{(index (index .HostConfig.PortBindings "80/tcp") 0).HostPort}}' beta # OR you can get a clean return

exit
```

**NOTE**:
