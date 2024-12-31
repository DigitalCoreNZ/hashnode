---
title: "Docker Desktop on Ubuntu 24.04."
datePublished: Tue Dec 31 2024 09:00:18 GMT+0000 (Coordinated Universal Time)
cuid: cm5c8mu1h000l09mdg6pp2mfi
slug: docker-desktop-on-ubuntu-2404
tags: microservices, software-development, linux, docker, opensource, devops, containerization, docker-installation, docker-desktop, ubuntu-2404, docker-uninstallation, docker-tips

---

# TL;DR.

This post provides a comprehensive guide on installing and uninstalling Docker and Docker Desktop on Ubuntu 24.04. It covers the prerequisites, step-by-step installation process, and troubleshooting tips, ensuring a smooth setup for managing containerized applications and microservices. The guide also highlights the benefits of using Docker Desktop for efficient software development.

> **Attributions:**
> 
> [https://www.docker.com/](https://www.docker.com/) ***↗.***

---

# An Introduction.

Docker and Docker Desktop are essential tools for modern software development. Whether you're a beginner or an experienced developer, this article will help you enhance your development workflow.

> The purpose of this post is to describe how to install Docker and Docker Desktop on Ubuntu 24.04.

---

# The Big Picture.

Docker and Docker Desktop are pivotal to modern software development. The containerisation approach to coding enhances the portability and scalability of applications across different platforms, eliminating any “it runs on my system” obstacles.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

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

---

# What is Docker?

Docker is used to containerise apps (and their dependencies) so they can run on any desktop and/or server operating system.

## Installing Docker.

> **Attribution:**
> 
> [https://linuxiac.com/how-to-install-docker-on-ubuntu-24-04-lts/](https://linuxiac.com/how-to-install-docker-on-ubuntu-24-04-lts/) ***↗.***

* From the terminal, I add HTTPS and the Curl utility:
    

```bash
sudo apt install -y apt-transport-https curl
```

* I import the Docker GPG repository key:
    

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I add the official Docker repository to my system:
    

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I refresh my local repo list:
    

```bash
sudo apt update
```

* I install Docker:
    

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

* I check to see if Docker is active:
    

```bash
sudo systemctl is-active docker
```

* I test the installation:
    

```bash
sudo docker run hello-world
```

## Uninstalling Docker.

> **Attributions:**
> 
> [https://learnubuntu.com/uninstall-docker/](https://learnubuntu.com/uninstall-docker/) ***↗.***

* From the terminal, I stop the running Docker containers:
    

```bash
docker stop $(docker ps -a -q)
```

* I remove the Docker containers:
    

```bash
docker rm $(docker ps -a -q)
```

* I remove the Docker images:
    

```bash
docker rmi $(docker images -a -q)
```

* I prune the custom Docker networks:
    

```bash
docker network prune
```

* I prune the Docker containers, networks, images, cache and volumes:
    

```bash
docker system prune -a
```

* I purge every Docker package:
    

```bash
sudo apt purge docker-* containerd.io --auto-remove
```

* I remove the Docker files:
    

```bash
sudo rm -rf /var/lib/docker
```

* I remove the Docker group:
    

```bash
sudo groupdel docker
```

* I remove the Docker socket:
    

```bash
sudo rm -rf /var/run/docker.sock
```

* I remove Docker Compose:
    

```bash
sudo rm -rf /usr/local/bin/docker-compose && sudo rm -rf /etc/docker && sudo rm -rf ~/.docker
```

---

# What is Docker Desktop?

Docker Desktop is used to build, share, and run containerized applications and microservices.

## Installing Docker Desktop.

> **Attributions:**
> 
> [https://docs.docker.com/desktop/setup/install/linux/ubuntu/](https://docs.docker.com/desktop/setup/install/linux/ubuntu/) ***↗,***
> 
> [https://dev.to/chandrashekhar/docker-desktop-is-not-working-on-ubuntu-2404-lts--2kpa](https://dev.to/chandrashekhar/docker-desktop-is-not-working-on-ubuntu-2404-lts--2kpa) ***↗.***

* I download the latest version of Docker Desktop:
    

[https://docs.docker.com/desktop/release-notes/](https://docs.docker.com/desktop/release-notes/)

* From the terminal, I change to the `Downloads` directory:
    

```bash
cd ~/Downloads
```

* I install the DEB package:
    

```bash
sudo apt install ./docker-desktop*.deb
```

> NOTE: Ignore the error message after installation.

* I fix the permissions issue:
    

```bash
echo 'kernel.apparmor_restrict_unprivileged_userns = 0' | sudo tee /etc/sysctl.d/20-apparmor-donotrestrict.conf
```

* I reboot my system:
    

```bash
reboot
```

* After the reboot, I return to a terminal and launch Docker Desktop:
    

```bash
systemctl --user start docker-desktop
```

* From the Apps Drawer, I pin the Docker Desktop icon to the Dock.
    

## Uninstall Docker Desktop.

* From the terminal, I remove Docker Desktop from my system:
    

```bash
sudo apt remove docker-desktop
```

* I remove the configuration and data files:
    

```bash
sudo apt remove docker-desktop && sudo rm /usr/local/bin/com.docker.cli && sudo apt purge docker-desktop
```

---

# The Results.

Setting up Docker Desktop on Ubuntu 24.04 requires a series of steps that ensures a smooth installation process. By following the outlined procedures, I can effectively manage containerized applications and microservices on my system. Docker Desktop provides a user-friendly interface and powerful tools so I can build, share, and run applications efficiently.

---

# In Conclusion.

I have discovered how Docker Desktop can transform my workflow!

Docker is a game-changer, allowing me to containerize my apps and their dependencies, ensuring the app run seamlessly on any platform.

In guide guide, I walked through the steps of installing Docker and Docker Desktop on Ubuntu 24.04.

From updating my base system to fixing permissions issues, I've covered my simple installation process.

With Docker Desktop, I can easily build, share, and run containerized applications and microservices.

It's all about efficiency and user-friendly interfaces!

Curious about the uninstallation process? I've included that too, ensuring I have complete control over my rig.

By following these steps, I can effectively manage my containerized applications and microservices, making development a smoother and more efficient process.

Have you tried Docker Desktop on Ubuntu yet? What challenges did you face, and how did you overcome them? Let's discuss below!

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#Docker #DockerDesktop #Ubuntu2404 #Containerization #Microservices #Linux #SoftwareDevelopment #DevOps #OpenSource #DockerInstallation #DockerUninstallation #DockerTips