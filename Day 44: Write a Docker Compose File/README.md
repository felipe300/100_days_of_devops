# Day 44: Write a Docker Compose File

**Objective**: Create and run a `docker-compose.yml` file to deploy a web server.

**Context**: The development team has created static website content. This content needs to be hosted on an HTTPD (Apache) web server using a containerized platform. The task is set within a simulated corporate infrastructure on a server.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

# check docker & docker compose
docker --version
docker compose version

cd /opt/docker/
touch docker-compose.yml
vi docker-compose.yml # edit the file

docker compose up -d # do this in the folder where is placed your "docker compose"
docker images
docker ps

curl -I http://localhost:8086 # this port (8086) should match the one in docker-compose file

exit
```

- `docker-compose.yml`

```Dockerfile
services:
  web:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8086:80"
    volumes:
      - /opt/data:/usr/local/apache2/htdocs/
```

**NOTE**:

- check the port
- check the folder for the volume
