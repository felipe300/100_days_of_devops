# Day 41: Write a Docker File

**Objective**: Write a custom image

**Context**: As per recent requirements shared by the application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

cd /opt/docker
touch Dockerfile

docker build -t my-apache-server .
docker container run -d my-apache-server --name apache2
> docker apache2 status

# exit docker container
> exit

exit
```

- `Dockerfile`

```Dockerfile
# 1. Base Ubuntu image
FROM ubuntu:24.04

# 2. Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# 3. Install Apache and curl
RUN apt-get update && apt-get install -y curl apache2 && apt-get clean

# 4. Expose port 80 by default
RUN sed -i 's/Listen 80/Listen 3000/g' /etc/apache2/ports.conf
EXPOSE 3000

# 5. Start Apache "foreground" to avoid been stooped
RUN service apache2 start && service apache2 status
CMD ["apachectl", "-D", "FOREGROUND"]
```

**NOTE**:

- Check the version of Ubuntu for this challenge
- Check the specific port for this challenge, in this case is the port 3000
