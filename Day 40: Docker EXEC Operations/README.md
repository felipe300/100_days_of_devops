# Day 40: Docker EXEC Operations

**Objective**: Install a service inside a running container

**Context**: One of the DevOps team members was working to configure services on a container that is running.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

echo $SHELL # get your current shell
docker ps # list running containers
docker exec -it [CONTAINER_NAME] [SHELL] # get the container name from "docker ps" and the shell

# inside the container
> systemctl status [PROGAM] --no-pager # "systemctl" is not installed, instead use "service"
> apt install [PROGAM] -y
> service [PROGAM] status
> cat /etc/apache2/ports.conf # check for port "80", and change it if asked (8089)
> apt install vim -y # install vim to edit files or you can use "nano" by default, or "sed"
> service [PROGAM] start

> curl -L https://localhost:[PORT] # in this case the port is (8089)

# Leave docker container
> exit

exit
```

**NOTE**:
