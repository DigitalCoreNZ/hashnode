---
title: "Installing LXD and Using LXCs."
datePublished: Fri Jan 19 2024 09:00:13 GMT+0000 (Coordinated Universal Time)
cuid: clrkeu4zt000o09l80kqzbpv8
slug: installing-lxd-and-using-lxcs
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706172227189/9597a0ab-3ed4-430a-8115-a95057191614.png
tags: lxc, containers, virtual-machines, lxd

---

Update: Saturday 10<sup>th</sup> February 2024.  
Update: Wednesday 28<sup>th</sup> February 2024.

# TL;DR.

LXD (<mark>L</mark>inu<mark>XD</mark>aemon) is a container manager for creating and managing containers. LXCs (<mark>L</mark>inu<mark>XC</mark>ontainers) are isolated system instances where anything within the container can NOT affect other containers or the base distro/OS. Also, multiple container instances can run concurrently on a single host.

> **Attributions:**
> 
> [https://ubuntu.com/lxd](https://ubuntu.com/lxd)***↗.***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704973638230/7de81bc6-cc05-4948-9bee-df36ca3ca67f.png align="center")

# An Introduction.

This is a concise (read: less rambling) version of [a post from 2023](https://solodev.app/2-of-10-lxd-on-the-homelab). This time around, I will be more specific about my intentions for this adapted chronicle.

> The purpose of this post is to present the installation, and likely uses, of LXD/LXC.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704973659623/47b64773-c25d-40ae-a47d-642b09f48778.png align="center")

# The Big Picture.

Containers are considered the Second Wave of System Isolation Technologies. The First Wave were virtual machines and the Third Wave are WASM/WASI binaries. Each Wave brought their own strengths and weaknesses.

| Name | Advantage | Disadvantage |
| --- | --- | --- |
| Wave 1: Virtual Machines | Isolation, less hardware, systems isolation, security, multiple OSs, ISA. | Resource heavy, expensive, complex. |
| Wave 2: Containers | Isolation, reduced complexity, security, distributed computing, consistency, orchestration, portability, efficiency, scalability, automation, shared kernel. | Stateless, may be hard to network, compatibility with other container technologies, |
| Wave 3: WASM | Portable, assemblies not needed after compilation, can run outside the browser with WASI. | Download size on Edge/2G and GSM/3G, not aware of the DOM - yet, lacks standard security defences. |

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704973687948/bc3fcb37-a70f-44ad-92a4-6805409a0c44.png align="center")

# Prerequisites.

* A Linux-based distro (I use Ubuntu).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704973704880/d291b34b-927a-4873-8ad3-b3bf39b53771.png align="center")

# Updating the System.

* I update my system:
    

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

## Installing the LXD.

* I install the snap package manager, if required:
    

```plaintext
sudo apt install -y snapd
```

* I install the LXD manager:
    

```plaintext
sudo snap install lxd
```

* I find the name of my host interface:
    

```bash
ip addr
```

> NOTE: My host interface name for the NIC (network interface card) is enp6s0.
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712191209985/be83bd9c-7efa-4896-a4e8-fa8d22017598.png align="center")

* I initialise the LXD:
    

```plaintext
sudo lxd init
```

> NOTE: When initialized, the host interface (enp6s0) will become available to the LXD manager. Now the LXD manager can connect to the router and ask for IP addresses for any running containers.
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712190917770/01120360-fb3d-4186-8921-571e192d5383.png align="center")

## Troubleshooting.

* I run a simple `LXC` command:
    

```bash
lxc ls
```

* Running the `LXC` command may result in one of these errors:
    

```bash
Error: Failed to connect to local LXD: Get "http://unix.socket/1.0": dial unix /var/snap/lxd/common/lxd/unix.socket: connect: permission denied
bash: /usr/sbin/lxc: No such file or directory
```

* To fix this issue, I provide access to the LXD group for my current account:
    

```bash
sudo usermod -aG lxd $(whoami)
```

* I change the GID (group ID) for the `LXD` manager:
    

```bash
newgrp lxd
```

* I test these changes by running the `LXC` command again:
    

```bash
lxc ls
```

## Deleting the LXD.

* I can delete the LXD, if required:
    

```plaintext
sudo snap remove --purge lxd
```

> NOTE: The `--purge` flag removes everything, including configuration files, etc.

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

* From the terminal, I log in to the container with the `yt` account:
    

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

* I copy the following, add it (CTRL + SHIFT + V) to the bottom (CTRL + END) of the `sshd_config` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

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

# 23 Common Commands.

Here is a list of 23 commands that maybe somewhat useful. Although I commonly use only a handful of commands from this list, it's nice to have a reference on file:

1. `lxc --version` to check the version (and if the command doesn't work, then I'd know an installation problem occurred),
    
2. `lxc network list` to list all the network adapters,
    
3. `lxc init ubuntu:22.04 test-container3` to download an Ubuntu container,
    
4. `lxc launch ubuntu:22.04 test-container3` to launch an Ubuntu container,
    
5. `lxc storage ls` to list storage pool,
    
6. `lxc list` or `lxc ls` to list all the images and containers,
    
7. `lxc stop test-container3` to stop a container,
    
8. `lxc start test-container3` to start a container,
    
9. `lxc restart test-container3` to restart a container,
    
10. `lxc stop test-container3` followed by `lxc delete test-container3`, or `lxc stop test-container3 -f` to delete a container,
    
11. `lxc exec test-container3 cat /etc/os-release` to execute a command on the container,
    
12. `lxc info test-container3` to check a container's Information,
    
13. `lxc exec test-container3 -- bash` to get root access to a container,
    
14. `lxc exec test-container3 -- su mylogin` to get account access to a container,
    
15. `lxc copy test-container3 test-container3-clone` to copy a container,
    
16. `lxc image list images: | grep -i centos` to list prebuilt images,
    
17. `lxc network show lxdbr0` to display information about network interface(s),
    
18. `lxc profile show default` to check the default profile using lxc command,
    
19. `lxc snapshot test-container3 test-container3_snap` followed by `lxc info test-container3` to take snapshot of an instance,
    
20. `lxc restore test-container3 test-container3_snap` to restore an instance from a snapshot,
    
21. `lxc export test-container3 /root/backup/lxd/test-container3_bkp--$(date +'%m-%d-%Y').tar.xz --optimized-storage` to take backup of an instance,
    
22. `lxc import /root/backup/lxd/test-container3_bkp--05-07-2022.tar.xz` followed by `lxc list` to restore instance from a backup, and
    
23. `lxc --help` to check all the options that are available to an LXC command.
    

> Attribution:
> 
> [https://www.cyberithub.com/20-best-lxc-command-examples-to-manage-linux-containers/](https://www.cyberithub.com/20-best-lxc-command-examples-to-manage-linux-containers/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704973890076/16827347-fadb-4e3b-8749-2fe5c9a2a75b.png align="center")

# The Results.

LXD and LXC provide a powerful, flexible, and resource-efficient way to run isolated system instances on a single host. This technology represents the second wave of system isolation technologies, offering certain advantages over traditional virtual machines. The process of installing LXD and using LXC may seem complex at first, but once I understood the basics and familiarized myself with common commands, I could create, manage, and delete containers with ease. Whether I'm setting up a `homelab` or deploying applications in a production environment, mastering LXD/LXC is a valuable skill.

# In Conclusion.

LXD and LXC was a revolutionary system isolation technology. LXD (Linux Daemon) is a container manager that allows me to create and manage containers. LXCs (Linux Containers), on the other hand, are isolated system instances. They ensure that anything within the container doesn't affect other containers or the base operating system. This means multiple container instances can run concurrently on a single host.

Containers are considered the Second Wave of System Isolation Technologies. The First Wave were virtual machines and the Third Wave are WASM/WASI binaries. Each Wave brought their own strengths and weaknesses.

LXD and LXC provide a powerful, flexible, and resource-efficient way to run isolated system instances on a single host. This technology offers certain advantages over traditional virtual machines, making it a valuable skill to master.

Once I understood the basics, I could create, manage, and delete containers with ease. Whether setting up a `homelab` or deploying applications in a production environment, adopting LXD/LXC was a game-changer.

So, have you used LXD and LXC in your projects? What's your experience been like? Share your thoughts in the comments below!

Until next time: Be safe, be kind, be awesome.

> NOTE: All images generated by [ComfyUI](https://github.com/comfyanonymous/ComfyUI) using the [dreamshaper\_8](https://huggingface.co/digiplay/DreamShaper_8/tree/main) checkpoint.