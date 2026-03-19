# Day 42: Create a Docker Network

**Objective**: Create a Docker network

**Context**: The DevOps team needs to set up several docker environments for different applications.

**Steps**:

```sh
ssh [user]@[hostname]
sudo su - # to avoid using sudo and enter the password multiple times. Work as a "super user"

docker network ls # List current networks
docker network create [NETWORK_NAME] # Create a new network, use the example bellow
docker network connect [NETWORK_NAME] [CONTAINER_ID] # Connect a running container
docker network inspect [NETWORK_NAME] # Inspect details

docker network create --driver [DRIVER_NAME] \
    --subnet [IP_SUBNET_ADDRESS/MASK] \
    --ip-range [IP_ADDRESS/MASK] \
    [NETWORK_NAME] # Create network

exit
```

**NOTE**:

Docker Networking is the subsystem that allows containers to communicate with each other, the host machine, and external networks (like the Internet or your local LAN). Think of it as a virtual system of cables and switches managed entirely by software.

By default, Docker isolates containers. A container has its own Network Stack, which includes its own routing table, IP address, and firewall rules. Docker Networking is the bridge that breaks this isolation in a controlled way.
Key Benefits:

- **Service Discovery**: When containers are in the same custom network, they can talk to each other using their container names as hostnames.

- **Security**: You can create "Internal-only" networks for databases so they are never exposed to the outside world, while keeping your web server on a public-facing network.

Docker uses different "drivers" to provide different types of connectivity:

**Bridge (Default)** -> The most common driver. It creates a private internal network on the host. Containers on the same bridge can talk to each other, but they are hidden from the outside world unless you "publish" ports (e.g., -p 80:80).

**Host** -> The container shares the host's networking namespace directly. The container does not get its own IP address; if you run a web server on port 80 in the container, it uses port 80 of your actual computer.

**Overlay** -> Used in Docker Swarm or multi-host setups. It allows containers running on different physical machines to communicate as if they were on the same local network.

**Macvlan** -> This driver assigns a unique MAC address to each container, making it appear as a physical device on your local network. Your router will see the container as if it were another laptop or server plugged into the switch.

When a container needs to access the Internet, Docker uses NAT (Network Address Translation). The host acts as a gateway, masking the container's internal IP with the host's public IP to fetch data and then routing the response back to the specific container.
