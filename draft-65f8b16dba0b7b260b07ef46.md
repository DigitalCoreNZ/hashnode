---
title: "5 of 5: Using Embeddings with LLMs."
slug: 5-of-5-using-embeddings-with-llms
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713400307394/e700293b-0922-4cf0-96cc-6de7fcf0fd08.png

---

JavaScript Scraping | Scrapy | ScrapeGraphAI | Nomic | Embeddings & LLMs

# TL;DR.

\[pending\]

> **Attributions:**
> 
> [https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗,***
> 
> [https://ubuntu.com/server/docs/containers-lxd](https://ubuntu.com/server/docs/containers-lxd)***↗,***
> 
> [https://ubuntu.com/server/docs/containers-lxc](https://ubuntu.com/server/docs/containers-lxc)***↗,***
> 
> [https://solodev.app/installing-lxd-and-using-lxcs](https://solodev.app/installing-lxd-and-using-lxcs),
> 
> [https://solodev.app/installing-docker](https://solodev.app/installing-docker), and
> 
> [https://www.docker.com/***↗***](https://www.docker.com/%E2%86%97)[***.***](https://www.docker.com/)

# An Introduction.

\[pending\]

# The Big Picture.

\[pending\]

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu), and
    
* [LXC/LXD](https://solodev.app/installing-lxd-and-using-lxcs).
    

# Updating my Base System.

* From the (base) terminal, I update my (base) system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

> NOTE: The Ollama LLM manager is already installed on my (base) system.

# What is LXD and LXC?

The LXD (LinuX Daemon) is the container manager that is used to create, and manage, LXCs (LinuX Containers). It is a background service that can automatically start LXCs when the host system boots, or stop any container from starting at all.

An LXC (LinuX Container) is an isolated, OS-level virtualization which, for efficiency, uses the Linux kernel of the host system. An LXC is a virtual environment where system processes within the LXC container can not affect other containers, or the host system, without specifically running certain commands.

[https://ubuntu.com/server/docs/containers-lxd](https://ubuntu.com/server/docs/containers-lxd)***↗,***

[https://ubuntu.com/server/docs/containers-lxc](https://ubuntu.com/server/docs/containers-lxc)***↗, and***

[https://solodev.app/installing-lxd-and-using-lxcs](https://solodev.app/installing-lxd-and-using-lxcs).

I ensure [LXD is installed](https://solodev.app/installing-lxd-and-using-lxcs) (`lxc --version`) before continuing with this post.

## Setting Up an LXC.

* I list the existing containers:
    

```plaintext
lxc ls
```

* I launch a new container called Default:
    

```plaintext
lxc launch ubuntu:22.04 Default
```

* I bash into the container:
    

```plaintext
lxc exec Default -- bash
```

* I update and upgrade the container:
    

```plaintext
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

## Adding a User Account to the LXC.

* From within the container, I add a new user:
    

```plaintext
adduser yt
```

* I add the new user to the `sudo` group:
    

```plaintext
usermod -aG sudo yt
```

> NOTE: usermod let's me (-a)ppend the sudo (-G)roup to the yt account.

* I exit the container:
    

```plaintext
exit
```

> NOTE: I exit the `root` account to use the `yt` account.

## Setting the LXC Home Directory.

* From the (base) terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec Default -- su yt
```

> NOTE: At the moment, the home directory is `/root`. This section will address the issue by changing the home directory to `~`.

* I use the Nano text editor to open the `.bashrc` file:
    

```plaintext
sudo nano ~/.bashrc
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `.bashrc` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
cd ~
```

## Hardening the Container.

* From within the container, I use the `Nano` text editor to open the `sshd_config` file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `sshd_config` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
PasswordAuthentication no
PermitRootLogin no
Protocol 2
Port = 2424
```

* I `restart` the `SSH` service:
    

```plaintext
sudo systemctl restart ssh
```

* I reboot the container:
    

```plaintext
sudo reboot
```

> NOTE: Within the container, I can also install (or enable) [UFW](https://solodev.app/creating-a-local-linux-container#heading-optional-enabling-and-setting-up-ufw), [Fail2Ban](https://solodev.app/creating-a-local-linux-container#heading-optional-installing-and-setting-up-fail2ban), and [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container).

# What is Docker?

Docker is a tool for easily deploying, and running my applications on any platform. I can package an application with all its code, libraries, dependencies, and tools, which allows me to deploy that app as a single bundle. Docker guarantees that my application will run on any computer that also runs Docker.

[https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗,***

[https://solodev.app/installing-docker](https://solodev.app/installing-docker), and

[https://www.docker.com/***↗***](https://www.docker.com/%E2%86%97)[***.***](https://www.docker.com/)

I ensure [Docker is installed](https://solodev.app/installing-docker) (`docker -v`) before continuing with this post.

## Preparing the Container for Docker.

* From the (base) terminal, I create a `btrfs` storage pool called `docker`:
    

```plaintext
lxc storage create docker btrfs
```

* In the `docker` pool, I create a new storage volume called `DefaultVol`:
    

```plaintext
lxc storage volume create docker DefaultVol
```

* I attach the `Default` container to the `DefaultVol` volume:
    

```plaintext
lxc config device add Default docker disk pool=docker source=DefaultVol path=/var/lib/docker
```

* I change the nested containers setting to true:
    

```plaintext
lxc config set Default security.nesting=true
```

* I change the intercept system calls setting to true:
    

```plaintext
lxc config set Default security.syscalls.intercept.mknod=true
```

* I change the emulate system calls setting to true:
    

```plaintext
lxc config set Default security.syscalls.intercept.setxattr=true
```

* I `restart` the container:
    

```plaintext
lxc restart Default
```

## Installing Docker.

* From the (base) terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec Default -- su yt
```

> NOTE: The home directory (`~`) for my account was [set in the .bashrc file](https://solodev.app/1-of-2-installing-gitlab-ce-using-docker-in-an-lxc#heading-setting-the-lxc-home-directory) earlier in this post.

* I install the following requirements:
    

```plaintext
sudo apt install -y ca-certificates curl gnupg lsb-release
```

* I make a `keyrings` directory:
    

```plaintext
mkdir -m 0755 -p /etc/apt/keyrings
```

* I add Docker’s official GPG key:
    

```plaintext
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I change the mode of the `docker.gpg` file:
    

```plaintext
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

* I install the `Docker` repository:
    

```plaintext
echo "deb [arch="$(dpkg --print-architecture)" \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update the `homelab` repo list:
    

```plaintext
sudo apt update
```

* I install `Docker` and its requirements:
    

```plaintext
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Checking the Docker Installation.

* I check if `Docker` is active:
    

```plaintext
systemctl is-active docker
```

* I check the status of `Docker`:
    

```plaintext
service docker status
```

* I check the `Docker` version:
    

```plaintext
sudo docker version
```

* I list the information for Docker:
    

```plaintext
sudo docker info
```

## Setting the Docker Privileges.

* I create the docker group, if required:
    

```plaintext
sudo groupadd docker
```

* I add my account to the docker group:
    

```plaintext
sudo usermod -aG docker $USER
```

* I log in to the new `docker` group (or reboot the container):
    

```plaintext
newgrp docker
```

* I verify the Docker installation by running this command without a `sudo` prefix:
    

```plaintext
docker run hello-world
```

> NOTE: This command displays 'Hello from Docker!' if Docker is properly installed.

# What is \[pending\]?

\[pending\]

# The Results.

\[pending\]

# In Conclusion.

\[pending\]

\[hash tags\]

[Scraping URLs](https://solodev.app/1-of-5-scraping-website-urls) | [Scraping Tutorial](https://solodev.app/2-of-5-scraping-tutorial-for-the-scrapy-tool) | Scraping Data | Making Embeddings | Using Embeddings