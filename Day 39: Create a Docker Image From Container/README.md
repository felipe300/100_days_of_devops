# Day 39: Create a Docker Image From Container

**Objective**: Create an image from a container

**Context**: A new request has been raised for the DevOps team to create a new image from a test container.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

docker images # list current images
docker ps # list running containers
docker ps -a # list containers

docker commit [CONTAINER_ID] [NEW_IMAGE_NAME]:[TAG] [DESTINY_FOLDER]

exit
```

**NOTE**:

Normally, when you stop and delete a Docker container, any changes you made inside it disappear. `docker commit` captures the current state of that container—its "writable layer"—and freezes it into a brand-new, static **image**.

How it Works

- **The Snapshot**: It takes the difference between the original image and your modified container.
- **The Result**: You get a new image that you can use to launch fresh containers that already have your changes baked in.
- **The Workflow**:
  1. Start a container.
  2. Change stuff inside it.
  3. Run `docker commit`.
  4. You now have a custom image.

Why use it?

**It's perfect for emergency debugging**. If you've spent an hour troubleshooting a complex environment inside a container and finally got it working, `docker commit` lets you save that progress immediately without having to figure out how to write the equivalent Dockerfile instructions first.

**Warning**: It’s great for a "quick fix," but it's generally avoided for production because it creates "mystery meat" images—nobody else can see exactly what commands were run to get that result.

By default, Docker pauses the container while it's being committed to reduce the risk of data corruption. If you need the container to keep running without interruption, use the `--pause=false` flag:

```sh
docker commit --pause=false [ID] [NAME]
```

What isn't saved?

- **Data in Volumes**: Any data stored in "Volumes" (external storage linked to the container) will not be included in the new image.
- **Environment Variables**: Only variables defined in the original image or Dockerfile persist; those added during docker run might not carry over.

Dockerfile

Most of the time you will use a Dockerfile, instead.

1. **Create a `Dockerfile`**

2. **Specify your base image, and setup your content**

```dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y python3
COPY . /app
```

3. **Built image**: `docker build - t [NEW_IMAGE_NAME]:[TAG_NAME] [DESTINY_FOLDER]`
