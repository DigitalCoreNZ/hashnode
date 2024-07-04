---
title: "Installing GitLab CE into Containers."
datePublished: Tue Mar 05 2024 09:00:07 GMT+0000 (Coordinated Universal Time)
cuid: clte536sb000a09jp0v2t4fl1
slug: installing-gitlab-ce-into-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709463335163/86bb8d7a-a379-404a-a316-0da917bd16bb.png
tags: software-development, docker, devops, lxc, containerization, development-workflow, lxd, docker-in-lxc, tech-guide, gitlab-ce, linux-containers

---

# TL;DR.

This post provides a step-by-step guide to installing GitLab CE using Docker within an LXC (LinuX Container). I start by explaining the basics of LXD, LXC, and Docker, then move on to the installation processes for each utility. This guide also explores how I set up LXC and Docker, how I download GitLab CE from Docker Hub, and how I resolve common issues. The end result is GitLab CE running in a Docker container within an LXC, offering a more effective, and streamlined, development workflow.

> **Attributions:**
> 
> [https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗,***
> 
> [https://docs.gitlab.com/ee/install/docker.html](https://docs.gitlab.com/ee/install/docker.html)***↗,***
> 
> [https://docs.docker.com/compose/](https://docs.docker.com/compose/)***↗.***

# An Introduction.

Containers are important to a modular development and deployment workflows.

> The purpose of this post is to show two container technologies working together.

# The Big Picture.

The LXD and LXCs (LinuX Containers) use one type of container technology. Docker uses another type of container technology. Although LXCs and Docker both use containers, they each solve different problems and address their own, specific use cases. LXCs run processes that do not affect other containers, or the host system, and are easily run. Docker encloses, and runs, apps in containers that are easily shared.

This post uses the GitLab CE installation as a way to demonstrate LXC and Docker technologies working together. (Yes, I know this post is a little over the top 😁.)

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

# Updating my Base System.

* In a terminal, I update my base system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is LXD and LXC?

The LXD (LinuX Daemon) is the container manager that is used to create, and manage, LXCs (LinuX Containers). It is a background service that can automatically start LXCs when the host system boots, or stop any container from starting at all.

An LXC (LinuX Container) is an isolated, OS-level virtualization which, for efficiency, uses the Linux kernel of the host system. An LXC is a virtual environment where system processes within the LXC container can not affect other containers, or the host system, without specifically running certain commands.

[https://ubuntu.com/server/docs/containers-lxd](https://ubuntu.com/server/docs/containers-lxd)***↗,***

[https://ubuntu.com/server/docs/containers-lxc](https://ubuntu.com/server/docs/containers-lxc)***↗, and***

[https://solodev.app/installing-lxd-and-using-lxcs](https://solodev.app/installing-lxd-and-using-lxcs).

## Setting Up an LXC.

* I list the existing containers:
    

```plaintext
lxc ls
```

> NOTE: I need to [install LXD](https://solodev.app/installing-lxd-and-using-lxcs) if this command fails.

* I launch a new container called GitLab:
    

```plaintext
lxc launch ubuntu:22.04 GitLab
```

* I bash into the container:
    

```plaintext
lxc exec GitLab -- bash
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

* From the terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec GitLab -- su yt
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
Port 22
```

> NOTE: Port 22 is the default, so I'll choose my own, random, available port number.

* I restart the "ssh" service:
    

```bash
sudo systemctl restart ssh.service
```

* I reboot the container:
    

```plaintext
sudo reboot
```

> NOTE: Within the container, I can also install (or enable) [UFW](https://solodev.app/creating-a-local-linux-container#heading-optional-enabling-and-setting-up-ufw), [Fail2Ban](https://solodev.app/creating-a-local-linux-container#heading-optional-installing-and-setting-up-fail2ban), and [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container).

# What is Docker?

Docker is a tool for easily deploying, and running my applications on any platform. I can package an application with all its code, libraries, dependencies, and tools, which allows me to deploy that app as a single bundle. Docker guarantees that my application will run on any computer that also runs Docker.

[https://www.docker.com/](https://www.docker.com/)***↗.***

## Updating the Container for Docker.

* From the terminal, I create a `btrfs` storage pool called `docker`:
    

```plaintext
lxc storage create docker btrfs
```

* In the `docker` pool, I create a new storage volume called `GitLabVol`:
    

```plaintext
lxc storage volume create docker GitLabVol
```

* I attach the `GitLab` container to the `GitLabVol` volume:
    

```plaintext
lxc config device add GitLab docker disk pool=docker source=GitLabVol path=/var/lib/docker
```

* I change the nested containers setting to true:
    

```plaintext
lxc config set GitLab security.nesting=true
```

* I change the intercept system calls setting to true:
    

```plaintext
lxc config set GitLab security.syscalls.intercept.mknod=true
```

* I change the emulate system calls setting to true:
    

```plaintext
lxc config set GitLab security.syscalls.intercept.setxattr=true
```

* I `restart` the container:
    

```plaintext
lxc restart GitLab
```

## Installing Docker.

* From the terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec GitLab -- su yt
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

* I create the Docker group, if required:
    

```plaintext
sudo groupadd docker
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

# What is GitLab CE?

GitLab CE (Community Edition) is an open source, end-to-end software development platform with built-in version control, issue tracking, code review, CI/CD, and more.  
I can self-host GitLab CE on my own servers, in a container, or on a cloud provider.

## Setting the `GITLAB_HOME` Env.

* I make the `GitLab` directory using the `-p`arents flag:
    

```plaintext
sudo mkdir -p /srv/gitlab
```

* I define the `GITLAB_HOME` environment variable:
    

```plaintext
export GITLAB_HOME=/srv/gitlab
```

* I reboot the container:
    

```plaintext
sudo reboot
```

## Downloading GitLab with Docker Compose.

* From the terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec GitLab -- su yt
```

* I use Nano to create a Docker Compose file called `docker-compose.yml`:
    

```plaintext
sudo nano ./docker-compose.yml
```

* I copy the following, add it (CTRL + SHIFT + V) to the file, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
version: '3.6'
services:
  gitlab:
    image: gitlab/gitlab-ce:16.7.5-ce.0
    container_name: gitlab
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        # Add any other gitlab.rb configuration here, each on its own line
        external_url 'https://gitlab.example.com'
    ports:
      # These ports are in format <host-port>:<container-port>
      - '80:80'
      - '443:443'
      - '22:22'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'
```

> NOTE: Compose V2 ignores the `version: '3.6'` entry on the first line, which is included for Compose V1 compatibility. Since 2023, V1 is no longer updated.

* I run Docker Compose:
    

```plaintext
docker compose up -d
```

> NOTE 1: Docker Compose is `-d`etached from the terminal and runs as a daemon. (A daemon is a service that runs in the background.)

> NOTE 2: It will take up to ~5 minutes to start the GitLab service.

* I can stop the Docker container (if required) with the down command:
    

```plaintext
docker compose down
```

* I check the logs in real time:
    

```plaintext
docker compose logs -f -t
```

* I stop the logs with `CTRL + C`.
    

## Setting Up the Root Password.

* I setup the root password:
    

```plaintext
docker exec -it gitlab gitlab-rake "gitlab:password:reset[root]"
```

> NOTE: Be patient. It can take up to a minute for this command to respond.

* I exit the container:
    

```plaintext
exit
```

## Testing GitLab CE.

* From the terminal, I find the IP address for the host interface called `eth0`:
    

```plaintext
lxc ls
```

> NOTE: `eth0` was set when [the LXD was initialised](https://solodev.app/1-of-2-installing-gitlab-ce-using-docker-in-an-lxc#heading-installing-the-lxd) earlier in this post.

* I add the IP address to a browser.
    
* I login to the `root` account.
    

> NOTE: It is NEVER a good idea to use the root account of ANY program for running day-to-day operations. This includes local distros and self-hosted services. I ALWAYS create a user account for handling my daily activities.

# The Results.

In this post, I walked through the process of installing GitLab CE using Docker in an LXC. I began by discussing the basics of LXD, LXC, and Docker, then moved on to the installation processes for each. I also explored how to set up an LXC and Docker, and how to download GitLab CE from Docker Hub. By following the steps outlined in this guide, I was able to run GitLab CE in a Docker container within an LXC, thereby leveraging the benefits of both containerization technologies for my coding workflow.

# In Conclusion.

LXD (LinuX Daemon) is a container manager, while LXCs (LinuX Containers) are isolated, OS-level virtualizations. Docker is a tool that helps with bundling applications into container packages that can run anywhere. GitLab CE is an open-source, end-to-end software development platform and repository. I can self-host everything, or I can push it all to a cloud provider.

So, how did I bring them all together? First, I installed LXD, and then I created an LXC. Next, I updated the LXC to handle Docker and finally, I pulled the latest GitLab CE image from Docker Hub. Voila! I now have GitLab CE running in a Docker container within an LXC.

By leveraging these technologies, my development workflows have become more efficient. And remember: I always keep my systems updated and upgraded for optimal security and performance.

Do you have any thoughts on combining these technologies for your development workflows? Have you tried it before, or are you considering it now? Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

#GitLabCE #Docker #LXC #LXD #DockerInLXC #LinuxContainers #Containerization #DevOps #SoftwareDevelopment #TechGuide #DevelopmentWorkflow