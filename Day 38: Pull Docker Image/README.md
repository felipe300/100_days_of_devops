# Day 38: Pull Docker Image

**Objective**: Pull an image to make tests

**Context**: The project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

docker images # list current images
docker rmi [IMAGE_ID] # delete image
# go to docker hub official page to look for the official image of (busybox:musl)
docker pull [IMAGE_NAME] # pull image (busybox:musl)
docker tag [IMAGE_NAME] [IMAGE]:[NEW_TAG_NAME] # (media)

exit
```

**NOTE**:
