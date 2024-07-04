---
title: "9 of 10: Docker Swarm with Docker Containers."
datePublished: Wed Jul 12 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljzfltry0dglmonvfgefhy5k
slug: 9-of-10-docker-swarm-with-docker-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999534278/77232940-a4f9-4944-a9c1-bd6df7f06eab.png
tags: docker, kubernetes, k8s, docker-swarm, k3s

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | Docker Swarm | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

I will install and set up Docker Swarm with a minimum of three Docker containers: one manager container and two worker containers. I will open some ports for communication, and deploy services using the docker stack commands.

## An Introduction.

My previous post "*in this 8-part mini-series"* covered [installing Portainer in a Docker container](https://solodev.app/6-of-8-portainer-in-the-docker-container). My *actual* previous post, however, covered [how to deploy multiple Docker containers](https://solodev.app/more-docker-containers). Why do I need multiple containers? Because a prerequisite for this lab is *a minimum* of three (3) Docker containers: I've named my containers `Docker`, `Docker2`, and (to absolutely no one's surprise) `Docker3`.

> The purpose of this post is to show how to install Docker Swarm across, at least, three Docker containers.

## The Big Picture.

The big idea is to set up an environment where I can develop my Docker Swarm management skills. From what I learned (online), Docker Swarm is easier to grasp than K3s or K8s. The big picture I'm looking toward combines Docker Swarm with Nginx reverse proxy and Nginx load balancing.

## Setting Up a Docker Swarm.

Here are the steps I use to set up a Docker swarm:

* I need *at least* 3 containers running Docker - The `Docker` container will run the Docker manager while the `Docker2` and `Docker3` containers will run the Docker workers. The `Docker` container must be able to communicate with the other containers over the network.
    
* I install Docker within all of the containers.
    
* From the terminal (`CTRL` + `ALT` + `T`) that is connected to the `Docker` container, I initialize the swarm mode:
    
    ```plaintext
    sudo docker swarm init --advertise-addr 192.168.?.?
    ```
    

> NOTE 1: This will make Docker (inside the Docker container) the host (or swarm manager).

> NOTE 2: I replace the ? above with the IP address for the `Docker` container. This is the experimental part. If this does not work, then I will need to figure out how to reference the IP address of the Docker instance instead.

* I issue the following UFW commands in all the containers:
    

```javascript
sudo ufw allow 2377/tcp
sudo ufw allow 2377/udp
sudo ufw allow 2376/tcp
sudo ufw allow 7946/tcp
sudo ufw allow 7946/udp
sudo ufw allow 4789/udp
```

> 2377 TCP for communication between manager nodes, 7946 TCP/UDP for node discovery, and 4789 UDP for overlay network traffic.

* The other two containers can join the swarm as workers by running the command given in the output of the `docker swarm init` command on the `Docker` terminal. It will be something like:
    
    ```plaintext
     sudo docker swarm join --token <token> <manager IP>:2377
    ```
    
* From the `Docker` terminal, I run `docker node ls` to view the swarm:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689575954456/a95e5cab-77ce-4a15-8338-8a54283799c6.png align="center")

* I can now deploy services to the swarm using `docker stack deploy` commands. The services will be scheduled across the manager and worker nodes.
    

This covers the basic steps to setting up a Docker swarm.

## The Results.

I demonstrated the process of setting up a Docker Swarm with Docker containers. By using a minimum of three containers, I was able to create a swarm of one manager node and two worker nodes. This setup allows for the efficient deployment and management of services across the swarm, providing a powerful tool for container orchestration. Docker Swarm will be a valuable addition to my toolkit as I continue to expand the capabilities of my `homelab`.

## In Conclusion.

If you've been linearly following this blog, then you'll notice a higgledy-piggledy order to these articles. I've touched on a number of OpTec services and now I need a mind map to guide me through my own thoughts. I'm ready to search for an optimal layout for these servers. Something like a high availability, load-balanced version of the following *might* work as a starting point:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689139371497/468c09b6-8c86-46a8-bffa-894fc753c26c.png align="center")

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | Docker Swarm | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)