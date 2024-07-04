---
title: "Installing NGINX Proxy Manager into Containers."
slug: installing-nginx-proxy-manager-into-containers

---

# TL;DR.

\[pending\]

> **Attributions:**
> 
> [https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗,***
> 
> [https://www.linode.com/docs/guides/beginners-guide-to-lxd-reverse-proxy/](https://www.linode.com/docs/guides/beginners-guide-to-lxd-reverse-proxy/)***↗.***

# An Introduction.

\[pending\]

# The Big Picture.

\[pending\]

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

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

LXD (LinuX Daemon) is a container manager for creating and managing LXCs (LinuX Containers.) As a background service, LXD can automatically start containers when the host system boots.

LXCs (LinuX Containers) are isolated, OS-level virtualizations which, for efficiency, uses the Linux kernel of the host system. LXCs are virtual environments where its system processes can *not* affect other containers, or the host system, without running specific commands.

## Installing the LXD.

* I install the snap package manager, if required:
    

```plaintext
sudo apt install snapd -y
```

* I install the LXD:
    

```plaintext
sudo snap install lxd
```

* I initialise the LXD:
    

```plaintext
lxd init
```

> NOTE: I choose to use BTRFS and an existing host interface called eno1.  
> (I used the `ip addr` command to find the name of my host interface.)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707522220201/f9686c89-4a0b-4749-9b59-32f1cc84bc7a.png align="center")

## Deleting the LXD.

* I can delete the LXD:
    

```plaintext
sudo snap remove --purge lxd
```

* I can also delete the LXD installer, if required:
    

```plaintext
sudo apt remove --purge lxd-installer
```

> NOTE: The `--purge` flag removes of everything, including configuration files, etc.

## Setting Up an LXC.

* I list the existing containers:
    

```plaintext
lxc ls
```

* I launch a new container called Proxy:
    

```plaintext
lxc launch ubuntu:22.04 Proxy
```

* I bash into the container:
    

```plaintext
lxc exec Proxy -- bash
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
lxc exec Proxy -- su yt
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

## Changing the LXC SSH Port.

* From within the container, I use the `Nano` text editor to open the `sshd_config` file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `sshd_config` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
Port = 2424
```

* I reboot the container:
    

```plaintext
sudo reboot
```

> NOTE: Within the container, I can also install (or enable) [UFW](https://solodev.app/creating-a-local-linux-container#heading-optional-enabling-and-setting-up-ufw), [Fail2Ban](https://solodev.app/creating-a-local-linux-container#heading-optional-installing-and-setting-up-fail2ban), and [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container).

# What is Docker?

Docker is a free tool that helps me develop, ship, and run my applications in containers. Unlike LXCs (LinuX Containers that require a Linux distro to work), Docker containers are lightweight bundles that package my application source code, infrastructure, libraries, and dependencies into one file that can run on any PC.

## Updating the Container for Docker.

* From the (base) terminal, I create a `btrfs` storage pool called `docker`:
    

```plaintext
lxc storage create docker btrfs
```

* In the `docker` pool, I create a new storage volume called `ProxyVol`:
    

```plaintext
lxc storage volume create docker ProxyVol
```

* I attach the `Proxy` container to the `ProxyVol` volume:
    

```plaintext
lxc config device add Proxy docker disk pool=docker source=ProxyVol path=/var/lib/docker
```

* I change the nested containers setting to true:
    

```plaintext
lxc config set Proxy security.nesting=true
```

* I change the intercept system calls setting to true:
    

```plaintext
lxc config set Proxy security.syscalls.intercept.mknod=true
```

* I change the emulate system calls setting to true:
    

```plaintext
lxc config set Proxy security.syscalls.intercept.setxattr=true
```

* I `restart` the container:
    

```plaintext
lxc restart Proxy
```

## Installing Docker.

* From the (base) terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec Proxy -- su yt
```

> NOTE: The home directory (`~`) for my account was [set in the .bashrc file](https://solodev.app/1-of-2-installing-gitlab-ce-using-docker-in-an-lxc#heading-setting-the-lxc-home-directory) earlier in this post.

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
echo "deb [arch="$(dpkg --print-architecture)" \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update the `homelab` repo list:
    

```bash
sudo apt update
```

* I install `Docker` and its requirements:
    

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Checking the Docker Installation.

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

* I create the Docker group, if required:
    

```bash
sudo groupadd docker
```

## Setting the Docker Privileges.

* I add my account to the docker group:
    

```bash
sudo usermod -aG docker $USER
```

* I log in to the new `docker` group (or reboot the container):
    

```bash
newgrp docker
```

* I verify the Docker installation by running this command without a `sudo` prefix:
    

```bash
docker run hello-world
```

> NOTE: This command displays 'Hello from Docker!' if Docker is properly installed.

# What is NGINX Proxy Manager?

\[pending\]

## Setting the Proxy Directory.

* I make the `Proxy` directory and change to that directory:
    

```bash
mkdir ~/Proxy && cd ~/Proxy
```

## Downloading NGINX Proxy Manager with Docker Compose.

* I use Nano to create a Docker Compose file called `docker-compose.yml`:
    

```bash
sudo nano ./docker-compose.yml
```

* I copy the following, add it (CTRL + SHIFT + V) to the file, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
version: '3.8'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

> NOTE: Compose V2 ignores the `version: '3.8'` entry on the first line, which is included for Compose V1 compatibility. Since 2023, V1 is no longer updated.

* I run Docker Compose:
    

```plaintext
docker compose up -d
```

> NOTE: Docker Compose is `-d`etached from the terminal and runs as a daemon. (A daemon is a service that runs in the background.)

* I can stop the Docker container (if required) with the down command:
    

```plaintext
docker compose down
```

* I check the logs in real time:
    

```plaintext
docker compose logs -f -t
```

* I stop the logs with `CTRL + C`.
    

## Testing NGINX Proxy Manager.

* From the container terminal, I find the IP address for the host interface called `eth0`:
    

```plaintext
lxc ls
```

> NOTE: `eth0` was set when [the LXD was initialised](https://solodev.app/1-of-2-installing-gitlab-ce-using-docker-in-an-lxc#heading-installing-the-lxd) earlier in this post.

* I add the `eth0` IP address, and port 81, to a browser:
    

```bash
192.168.188.52:81
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707818065397/91f3e6ff-0ab1-4445-8ae7-9be0231a359d.png align="center")

* I login to the `admin@example.com` account:
    

```bash
username: admin@example.com
password: changeme
```

> NOTE: It is NEVER a good idea to use the root account of ANY program for running day-to-day operations. This includes local distros and self-hosted services. I ALWAYS create a user account for handling my daily activities.

# What is Cloudflare?

\[pending\]

## Connecting to Cloudflare.

\[pending\]

[https://silicon.blog/2023/01/22/how-to-combine-nginx-proxy-manager-with-cloudflare-to-access-your-websites-web-services-securely/](https://silicon.blog/2023/01/22/how-to-combine-nginx-proxy-manager-with-cloudflare-to-access-your-websites-web-services-securely/)

# The Results.

\[pending\]

# In Conclusion.

\[pending\]