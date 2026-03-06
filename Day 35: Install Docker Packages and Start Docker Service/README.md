# Day 35: Install Docker Packages and Start Docker Service

**Objective**: Learn and install Docker

**Context**: The DevOps team aims to containerize various applications.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su -

cat /etc/os-release # check your system OS, got "Centos 9"
# clean any previous installation
sudo dnf remove -y docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine \
                  podman \
                  buildah

# Set up the repository
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Install the Docker packages. LTS Version
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start Docker Engine.
sudo systemctl enable --now docker

# To run Docker commands without typing sudo every time, add your user to the docker group
# You will need to log out and log back in for this change to take effect.
sudo usermod -aG docker $USER

# check installation
systemctl status --no-pager docker

exit
```

**Notes**

Docker is a tool that allows you to package an application and everything it needs to run (like libraries, system tools, and settings) into a single, standardized unit called a container.

Advantages

- **"It Works on My Machine" Syndrome**: Docker eliminates environment mismatches. Since the container includes all dependencies, the app runs consistently across different systems.

- **Resource Efficiency**: Unlike Virtual Machines (VMs) which require a full operating system for each instance, Docker containers share the host's operating system kernel. This makes them much lighter and faster to start (seconds vs. minutes).

- **Portability**: You can build a container locally and deploy it to any cloud provider (AWS, Azure, Google Cloud) or on-premises server without changing the code.

- **Isolation**: Each container is isolated from others. If one app crashes or has a security vulnerability, it is less likely to affect the other apps running on the same server.

- **Version Control for Infrastructure**: You can track changes to your Docker images, roll back to previous versions if a bug is found, and share images via Docker Hub (like GitHub for containers).

Disadvantages

- **Security Risks**: Because containers share the same underlying OS kernel, a security breach in the kernel could potentially impact all containers on that host.

- **Performance on Non-Linux Systems**: Docker runs natively on Linux. On Windows and macOS, it has to run a small virtual Linux environment in the background, which can consume more RAM and CPU.

- **Storage Management**: Managing persistent data (like databases) can be complex because containers are meant to be temporary. If you delete a container without setting up "Volumes," you lose your data.

- **Learning Curve**: While basic commands are easy, managing complex systems with dozens of containers requires learning additional tools like Kubernetes or Docker Compose.

- **Graphical Apps**: Docker is primarily designed for command-line or web applications. Running apps with a complex Graphical User Interface (GUI) is difficult and clunky.
