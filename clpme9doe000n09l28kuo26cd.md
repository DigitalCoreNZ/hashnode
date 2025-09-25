---
title: "Installing Docker CE."
datePublished: Fri Dec 01 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpme9doe000n09l28kuo26cd
slug: installing-docker-ce
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1758162642181/c5d509a8-39e1-4db1-941d-66c4fc34c9d5.png
tags: docker, containers, isolation, installation, portability

---

Update: Thursday 18<sup>th</sup> September 2025.  
Update: Wednesday 24<sup>th</sup> September 2025.

# TL;DR.

This post explains how to install Docker, a tool that makes it easy to develop, ship, and run apps. Docker puts an app's code, infrastructure, libraries, and dependencies into one small package that runs on any computer. To install Docker, I update my system, install any requirements, add Docker's official GPG key, install the Docker repository, and check the installation. This post also shows how to uninstall Docker. The main advantages of using Docker include:

* An ability to run my apps on any system,
    
* Isolating processes from other containers and the host,
    
* Quick assembly and deployment, and
    
* Easily making containers for my apps.
    

> **Attributions:**
> 
> [https://www.docker.com/](https://www.docker.com/)***↗***

# An Introduction.

Docker is a utility that helps me package my applications so they can run on any computer system.

> The purpose of this post is to present a process for installing, and using, Docker.

# The Big Picture.

Docker is a container system. The main advantages of using Docker include:

* The isolation of running processes,
    
* The ease of creating new containers,
    
* Fast deployments, and
    
* Fast migrations.
    

# **Prerequisites.**

* A Linux-based distro (I use Ubuntu).
    

# What is Docker?

Docker is a free tool that helps me develop, ship, and run my applications in containers. Containers are lightweight bundles that package my application source code, infrastructure, libraries, and dependencies into one file that can run on any PC.

## Installing Docker.

* I update my (base) system:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

* I install the following requirements:
    

```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```

* I make a `keyrings` directory:
    

```bash
mkdir -m 0755 -p /etc/apt/keyrings
```

* I add Docker’s official GPG key:
    

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I change the mode of the `docker.gpg` file:
    

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

* I install the `Docker` repository:
    

```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update my (base) system:
    

```bash
sudo apt update
```

* I install the `Docker` Community Edition engine, the Docker CLI, the container daemon, and the Buildx and Compose plugins:
    

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Checking Docker.

* I check if `Docker` is active:
    

```bash
systemctl is-active docker
```

* I check the status of `Docker`:
    

```bash
service docker status
```

* I check the `Docker` version:
    

```bash
sudo docker version
```

* I list the information for Docker:
    

```bash
sudo docker info
```

## Docker Setup.

* I create the Docker group, if required:
    

```bash
sudo groupadd docker
```

* I add my user account to the Docker group:
    

```bash
sudo usermod -aG docker ${USER}
```

* I verify the installation:
    

```plaintext
sudo docker run hello-world
```

* I reboot the `homelab` system to load the Docker settings into memory (or I can reboot the system after installing Distrobox.)
    

## Uninstalling Docker.

* This command uninstalls Docker:
    

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt remove $pkg; done
```

## Docker Commands.

The commands I commonly use are highlighted in yellow.

### Management Commands.ls -al

| Command | Description |
| --- | --- |
| `docker dockerd` | Launch the Docker daemon |
| `docker info` | Display system-wide information |
| `docker inspect` | Return low-level information on a container or image |
| `docker version` | Show the Docker version information |

### Image Commands.

| Command | Description |
| --- | --- |
| `docker build` | Build an image from a Dockerfile |
| `docker commit` | Create a new image from a container’s changes |
| `docker history` | Show the history of an image |
| docker image rm \[ID\] -f | Remove image by ID |
| docker images | List images |
| `docker import` | Import the contents from a tarball to create a filesystem image |
| `docker load` | Load an image from a tar archive or STDIN |
| `docker rmi` | Remove one or more images |
| `docker save` | Save images to a tar archive |
| `docker tag` | Tag an image into a repository |

### Container Commands.

| Command | Description |
| --- | --- |
| `docker attach` | Attach to a running container |
| docker container prune -f | Remove all stopped containers |
| `docker cp` | Copy files/folders from a container to a HOSTDIR or to STDOUT |
| `docker create` | Create a new container |
| `docker diff` | Inspect changes on a container’s filesystem |
| `docker events` | Get real time events from the server |
| `docker exec` | Run a command in a running container |
| `docker export` | Export a container’s filesystem as a tar archive |
| `docker kill` | Kill a running container |
| `docker logs` | Fetch the logs of a container |
| `docker pause` | Pause all processes within a container |
| `docker port` | List port mappings or a specific mapping for the container |
| docker ps -a | List ALL containers |
| docker ps -f "status=exited" | List stopped containers |
| `docker rename` | Rename a container |
| `docker restart` | Restart a running container |
| docker rm | Remove one or more containers |
| `docker run` | Run a command in a new container |
| `docker start` | Start one or more stopped containers |
| `docker stats` | Display a live stream of container(s) resource usage statistics |
| docker stop | Stop a running container |
| `docker top` | Display the running processes of a container |
| `docker unpause` | Unpause all processes within a container |
| `docker update` | Update configuration of one or more containers |
| `docker wait` | Block until a container stops, then print its exit code |

### Shared Data Volume Commands.

| Command | Description |
| --- | --- |
| `docker volumes create` | Creates a new volume where containers can consume and store data |
| `docker volumes inspect` | Display information about a volume |
| `docker volumes ls` | Lists all the volumes Docker knows about |
| `docker volumes rm` | Remove one or more volumes |

### Hub and Registry Commands.

| Command | Description |
| --- | --- |
| `docker login` | Register or log in to a Docker registry |
| `docker logout` | Log out from a Docker registry |
| `docker pull` | Pull an image or a repository from a Docker registry |
| `docker push` | Push an image or a repository to a Docker registry |
| `docker search` | Search the Docker Hub for images |

### Network and Connectivity Commands.

| Command | Description |
| --- | --- |
| `docker network connect` | Connect a container to a network |
| `docker network create` | Create a new network |
| `docker network disconnect` | Disconnect a container from a network |
| `docker network inspect` | Display information about a network |
| `docker network ls` | Lists all the networks the Engine daemon knows about |
| `docker network rm` | Removes one or more networks |

### Swarm Commands.

| Command | Description |
| --- | --- |
| `docker swarm init` | Initialize a swarm |
| `docker swarm join` | Join a swarm as a manager node or worker node |
| `docker swarm leave` | Remove the current node from the swarm |
| `docker swarm update` | Update attributes of a swarm |
| `docker swarm join-token` | Display or rotate join tokens |

### Swarm Service Commands.

| Command | Description |
| --- | --- |
| `docker service create` | Create a new service |
| `docker service inspect` | Inspect a service |
| `docker service ls` | List services in the swarm |
| `docker service rm` | Remove a service from the swarm |
| `docker service scale` | Set the number of replicas for the desired state of the service |
| `docker service ps` | List the tasks of a service |
| `docker service update` | Update the attributes of a service |

### Swarm Node Commands.

| Command | Description |
| --- | --- |
| `docker node promote` | Promote a node that is pending a promotion to manager |
| `docker node demote` | Demotes an existing manager so that it is no longer a manager |
| `docker node inspect` | Inspect a node in the swarm |
| `docker node update` | Update attributes for a node |
| `docker node ps` | List tasks running on a node |
| `docker node ls` | List nodes in the swarm |
| `docker node rm` | Remove one or more nodes from the swarm |

### Compose Commands.

| Command | Description |
| --- | --- |
| `docker compose attach` | Attach local standard input, output, and error streams to a service's running container |
| `docker compose build` | Build or rebuild services |
| `docker compose config` | Parse, resolve and render compose file in canonical format |
| `docker compose cp` | Copy files/folders between a service container and the local filesystem |
| `docker compose create` | Creates containers for a service |
| `docker compose down` | Stop and remove containers, networks |
| `docker compose events` | Receive real time events from containers |
| `docker compose exec` | Execute a command in a running container |
| `docker compose images` | List images used by the created containers |
| `docker compose kill` | Force stop service containers |
| `docker compose logs` | View output from containers |
| `docker compose ls` | List running compose projects |
| `docker compose pause` | Pause services |
| `docker compose port` | Print the public port for a port binding |
| `docker compose ps` | List containers |
| `docker compose pull` | Pull service images |
| `docker compose push` | Push service images |
| `docker compose restart` | Restart service containers |
| `docker compose rm` | Remove stopped service containers |
| `docker compose run` | Run a one-off command on a service |
| `docker compose scale` | Scale services |
| `docker compose start` | Start services |
| `docker compose stats` | Display a live stream of container(s) resource usage statistics |
| `docker compose stop` | Stop services |
| `docker compose top` | Display the running processes |
| `docker compose unpause` | Unpause services |
| `docker compose up` | Create and start containers |
| `docker compose version` | Show the Docker Compose version information |
| `docker compose wait` | Block until the first service container stops |
| `docker compose watch` | Watch build context for service and rebuild/refresh containers when files are updated |

# The Results.

Docker is an invaluable tool that allows me to package my applications into containers, ensuring that they can run on any system. This simplifies the process of developing, shipping, and running my applications, and also enhances the efficiency of deployments and migrations. After going through the installation process, I should now have Docker installed on my Linux-based system, and be able to leverage its capabilities to improve my development workflow. Remember, the power of Docker lies in its ability to isolate running processes and easily create new containers, improving the way I deploy my applications.

# In Conclusion.

How do I package my applications so they can run on ANY computer?

This was Docker, a container system that isolated any running processes, easily created new containers, supported fast app deployments, and allowed quick and easy migrations. It was like having my own, personal mini-shipyard for "shipping" applications to... anywhere.

How did it work?

Docker packaged the source code for my app, its infrastructure, any required libraries, and all the needed dependencies into one lightweight bundle. This bundle, or 'container', could then run on any PC. It was like having my entire tech stack in a portable suitcase!

This guide walked me through installing Docker.

First, I needed a Linux-based distro. I use Ubuntu. Then followed these steps:

1. I updated my system.
    
2. I installed the necessary requirements.
    
3. I made a 'keyrings' directory.
    
4. I added Docker’s official GPG key.
    
5. I changed the mode of the 'docker.gpg' file.
    
6. I installed the Docker repository.
    
7. I updated the repo list.
    
8. I installed Docker and its requirements.
    
9. I checked if Docker was active.
    
10. I verified the installation.
    
11. I rebooted the system to load the Docker settings into memory.
    

Voila! I installed Docker.

But what if I wanted to uninstall Docker? Just one command does the trick. Easy-peasy, right?

Docker is an invaluable tool that simplifies the process of developing, shipping, and running applications. It's a game-changer in the world of deployments and migrations.

So, who's ready to give Docker a try? Or if you're already using it, share your experience. How has Docker improved your workflow?

Until next time: Be safe, be kind, be awesome.