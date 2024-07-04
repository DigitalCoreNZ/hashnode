---
title: "Creating a Local LinuX Container."
datePublished: Mon Jan 22 2024 09:00:49 GMT+0000 (Coordinated Universal Time)
cuid: clrop6h22000o08jqdlkwexao
slug: creating-a-local-linux-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706172136304/1d56561a-64c7-4f8a-8dba-dd56ee30cc6e.png
tags: lxc, lxd, linux-daemon, linux-container

---

Update: Friday 9<sup>th</sup> February 2024.

# TL;DR.

This post provides a step-by-step guide to creating and configuring a local Linux container on a Debian-based Linux distro. It covers the procedures of creating a new container, adding a user account, fixing home directory issues, and setting up security measures like UFW, Fail2Ban, and CrowdSec.

> **Attributions:**
> 
> [https://ubuntu.com/containers](https://ubuntu.com/containers)***↗.***

# An Introduction.

A container is an isolated system that can run processes, procedures, and programs without affecting other containers or the base distro.

> The purpose of this post is to produce a template for creating containers.

# The Big Picture.

Containers, unlike virtual machines, are lightweight and efficient. Yes, containers rely on the host kernel, but it's a small price to pay for a capable containment technology.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu), and
    
* an [LXD installation](https://solodev.app/installing-lxd-and-using-lxcs).
    

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

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707467534222/31398c54-97a1-46e1-a179-acb1c430e9c5.png align="center")

> NOTE: I choose to use BTRFS and an existing host interface called enp6s0.  
> (I used the `ip addr` command to find the name of my host interface.)

## Deleting the LXD.

* I can delete the LXD:
    

```plaintext
sudo snap remove --purge lxd
```

* I can delete the LXD installer:
    

```plaintext
sudo apt remove --purge lxd-installer
```

> NOTE: The `--purge` flag removes of everything, including configuration files, etc.

## Creating a New Container.

> NOTE: The "container-name" below is a placeholder. This placeholder should be replaced with an actual container name.

* From the terminal, I create a new container:
    

```bash
lxc launch ubuntu:22.04 container-name
```

* I bash into the container:
    

```bash
lxc exec container-name -- bash
```

* I update and upgrade the container:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt autoclean && \
sudo apt --fix-broken install && \
sudo apt autoremove -y
```

## Adding a User Account to the Container.

* From within the container, I create a new user:
    

```bash
adduser yt
```

* I add the new user to the 'sudo' group:
    

```bash
usermod -aG sudo yt
```

> NOTE: usermod let's me (-a)ppend the sudo (-G)roup to the 'yt' account.

* I reboot the container:
    

```bash
reboot
```

The next step is to fix the home directory problem.

## Fixing the Home Directory Problem.

> NOTE: I use Nano to add an entry to the `.bashrc` file.

* From the terminal, I log in to the container with the 'yt' account:
    

```bash
lxc exec container-name -- su yt
```

* I open the `.bashrc` file with the Nano text editor:
    

```bash
sudo nano ~/.bashrc
```

* I add the following to the bottom of the file, save (CTRL +S) the changes, and exit (CTRL + X) the Nano text editor:
    

```bash
cd ~
```

* I reboot the container:
    

```bash
sudo reboot
```

# Top 20 LXC Commands.

LXC comes with a lot of controls, but I find these 20 commands very useful:

1. `lxc --version` to check the version (and if the command doesn't work, then I'd know an installation problem occurred),
    
2. `lxc network list` to list all the network adapters,
    
3. `lxc launch ubuntu:22.04 test-container3` to launch a container,
    
4. `lxc storage ls` to list storage pool,
    
5. `lxc list` or `lxc ls` to list all the running containers,
    
6. `lxc stop test-container3` to stop a container,
    
7. `lxc start test-container3` to start a container,
    
8. `lxc restart test-container3` to restart a container,
    
9. `lxc stop test-container3` followed by `lxc delete test-container3`, or `lxc delete test-container3 -f` to delete a container,
    
10. `lxc exec test-container3 cat /etc/os-release` to execute a command on the container,
    
11. `lxc info test-container3` to check a container's Information,
    
12. `lxc exec test-container3 -- bash` to get shell access to an LXC container as root,
    
13. `lxc image list images: | grep -i centos` to list prebuilt images,
    
14. `lxc network show lxdbr0` to display information about network interface(s),
    
15. `lxc profile show default` to check the default profile using lxc command,
    
16. `lxc snapshot test-container3 test-container3_snap` followed by `lxc info test-container3` to take snapshot of an instance,
    
17. `lxc restore test-container3 test-container3_snap` to restore an instance from a snapshot,
    
18. `lxc export test-container3 /root/backup/lxd/test-container3_bkp--$(date +'%m-%d-%Y').tar.xz --optimized-storage` to take backup of an instance,
    
19. `lxc import /root/backup/lxd/test-container3_bkp--05-07-2022.tar.xz` followed by `lxc list` to restore instance from a backup, and
    
20. `lxc --help` to check all the options that are available to an LXC command.
    

> Attribution:
> 
> [https://www.cyberithub.com/20-best-lxc-command-examples-to-manage-linux-containers/](https://www.cyberithub.com/20-best-lxc-command-examples-to-manage-linux-containers/)

## OPTIONAL: Enabling, and Setting Up, UFW.

* From the terminal, I log in to the container with the 'yt' account:
    

```bash
lxc exec container-name -- su yt
```

* I check the UFW status:
    

```bash
sudo ufw status
```

* I enable the UFW:
    

```bash
sudo ufw enable
```

* I install a UFW rule:
    

```bash
sudo ufw allow from 192.168.?.?
```

> NOTE: I use `ip a` in my workstation terminal to find my IP address. ***I replace the IP address above with the actual address for the***`workstation`***, e.g. 192.168.188.41.***

* I check the status of the UFW and list the rules by number:
    

```bash
sudo ufw status numbered
```

> NOTE 1: UFW will, by default, block all incoming traffic, including SSH and HTTP.
> 
> NOTE 2: I will update the UFW rules as I deploy other services to the container.

* I delete a UFW rule by number if needed:
    

```bash
sudo ufw delete 1
```

* I disable UFW if needed:
    

```bash
sudo ufw disable
```

* I reboot the container:
    

```bash
sudo reboot
```

## OPTIONAL: Installing, and Setting Up, Fail2Ban.

* From the terminal, I log in to the container with the 'yt' account:
    

```bash
lxc exec container-name -- su yt
```

* From the `homelab` terminal (`CTRL` + `ALT` + `T`) connected to the container, I install Fail2Ban:
    

```bash
sudo apt install fail2ban -y
```

* I copy the `jail.conf` file as `jail.local`:
    

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

* I open the `jail.local` file in Nano:
    

```bash
sudo nano /etc/fail2ban/jail.local
```

* I change a few (SSH-centric) settings in the `jail.local` file, then I save those changes, and exit the Nano editor:
    

```bash
[DEFAULT]
⋮
bantime = 1d
maxretry = 3
⋮
[sshd]
enabled = true
port = ssh,22
```

* I restart Fail2Ban:
    

```bash
sudo systemctl restart fail2ban
```

* I check the status of Fail2Ban:
    

```bash
sudo systemctl status fail2ban
```

* I enable Fail2Ban to autostart on boot:
    

```bash
sudo systemctl enable fail2ban
```

* I reboot the container:
    

```bash
sudo reboot
```

## OPTIONAL: Installing, and Setting Up, CrowdSec.

I can also use [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container) as another security layer.

# The Results.

Linux containers provide a lightweight and efficient alternative to traditional virtual machines. This guide outlined the process of creating and configuring a local Linux container, with additional steps for adding user accounts, resolving common issues, and implementing security measures such as UFW, Fail2Ban, and CrowdSec. While containers do rely on the host kernel, the benefits they offer in terms of performance and resource utilization make them a worthwhile consideration for any developer or system administrator. Understanding containers and how to use them effectively is key to maximizing their potential.

# In Conclusion.

Linux containers are an efficient alternative to traditional virtual machines and offer a lightweight solution that maximizes performance and resource utilization. Unlike virtual machines, containers are designed to be efficient but they rely on the host kernel.

I've outlined step-by-step procedures to creating and configuring local Linux containers while also covering how to add user accounts, resolving common issues, and implementing security measures such as UFW, Fail2Ban, and CrowdSec.

These containers are a game-changer for developers and system administrators, offering benefits that make them a worthwhile consideration in my tech stack. Knowing about containers and how to use them is important for getting the most out of this technology.

What are your thoughts on using Linux containers? Have you used them before? Let's discuss below!

Until next time: Be safe, be kind, be awesome.