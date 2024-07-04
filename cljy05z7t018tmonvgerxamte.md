---
title: "8 of 10: More Docker Containers."
datePublished: Tue Jul 11 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljy05z7t018tmonvgerxamte
slug: 8-of-10-more-docker-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999488759/55fada3e-cb61-4787-9801-66b8f39a75b3.png
tags: docker, lxc, lxd, docker-in-lxc, docker-in-linux-container

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | More Docker | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

I will create, and configure, another container for Docker. I will call it 'docker2', and I will enable nesting within the container. I will then install Docker, change the Docker IP address, test the installation, and change my settings (if needed).

## An Introduction.

In a previous post, I [installed Docker in a <mark>L</mark>inu<mark>X</mark> <mark>C</mark>ontainer](https://solodev.app/3-of-8-docker-in-a-linux-container). This time, I will... install Docker in a Linux container. However, I'll be using a modified, and simplified, process to achieve this outcome.

> The purpose of this post is to formalise a process for installing Docker in Linux containers.

## The Big Picture.

My next post is all about installing, and setting up, a Docker Swarm solution. A prerequisite for running a Docker Swarm is to have *at least* 3 Docker servers.

Beyond experimenting with Docker Swarm, I will also reference this post while learning to build infrastructure as code (IaC) solutions. I will need to practice making state files (For TerraForm) and Playbooks (for Ansible), so deploying Docker containers seems like a good candidate for learning IaC automation.

## Installing Docker in a Container. Again.

* From the `homelab` terminal (`CTRL` + `ALT` + `T`), I create a new container called 'docker2' where I set nesting to true:
    

```plaintext
lxc launch ubuntu:22.04 docker2 -c security.nesting=true
```

> NOTE: Nesting allows the 'docker2' container to host another container system, e.g. Docker.

* I bash into the new container:
    

```plaintext
lxc exec docker2 -- bash
```

* I update and upgrade the 'docker2' container:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install Docker:
    

```plaintext
sudo apt install -y docker.io
```

> NOTE: For the sake of brevity, I have skipped:
> 
> * [Adding a user account](https://solodev.app/1-of-3-setting-up-a-remote-container), installing OpenSSH, and "softening" the container,
>     
> * [Creating (and using) RSA keys](https://solodev.app/2-of-3-setting-up-a-remote-connection), establishing SSH connections, and "hardening" the container, and
>     
> * [Further "hardening" of the container](https://solodev.app/3-of-3-hardening-the-remote-container) using UFW and Fail2Ban.
>     

## Changing the Docker IP Address.

* I open (or create) a file in Nano:
    

```plaintext
sudo nano /etc/docker/daemon.json
```

* I add the following object, save the changes, and exit Nano:
    

```plaintext
{
    "bip": "172.17.0.2/24"
}
```

* I restart Docker:
    

```plaintext
sudo service docker restart
```

## Testing the Docker Installation.

* I run the 'hello-world' Docker project:
    

```plaintext
sudo docker run hello-world
```

## Other Docker Settings.

* If the 'hello-world' test fails, I will need to exit the container:
    

```plaintext
exit
```

* I configure the docker socket for the 'docker2' container:
    

```plaintext
lxc config device add docker2 docker-dev unix-char path=/var/run/docker.sock
```

* I bash back into the 'docker2' container:
    

```plaintext
lxc exec docker2 -- bash
```

* I run the 'hell-world' project again:
    

```plaintext
sudo docker run hello-world
```

## The Results.

This post provides a step-by-step guide on creating and configuring a new Docker container called 'docker2', enabling nesting, installing Docker, changing the Docker IP address, and testing the installation. By following these instructions, I can easily set up, and manage, Docker in a <mark>L</mark>inu<mark>X</mark> <mark>C</mark>ontainer.

## In Conclusion.

Spinning up, and tearing down, Docker containers may seem whimsical, but the ephemeral nature of containers is an important part of my `homelab` experience. I'm working my way toward an integrated solution for the 12 Startups project. The more posts I publish, the closer I get to the Agile-DevSecOps-CI/CD Nirvana.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | More Docker | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)