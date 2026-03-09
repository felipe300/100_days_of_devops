# Day 37: Copy File to Docker Container

**Objective**: Copy a file from host machine to inside a container

**Context**: Save crypted files

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

docker ps # container currently running
docker ps -a # container history
cat /tmp/[FILENAME] # check the file to move
docker cp [HOST_PATH] [DOCKER_CONTAINER]:[DESTINATION_PATH] # copy a file from host to docker
docker cp [DOCKER_CONTAINER]:[DESTINATION_PATH] [HOST_PATH] # copy a file from docker to host
docker exec -it [DOCKER_CONTAINER] sh # get inside the container and check if file was created

exit
```

**NOTE**: It works the same if you are copying files or folders. Docker usually preserves the ownership and permissions of the files you copy. You can use `docker cp` whether the container is running or stopped. You can move manually and freely files or folder in a docker volume.
