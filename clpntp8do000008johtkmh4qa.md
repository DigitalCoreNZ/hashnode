---
title: "Installing Distrobox."
datePublished: Sat Dec 02 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpntp8do000008johtkmh4qa
slug: installing-distrobox
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701641439392/51175fc3-c574-4f9c-95b4-e4d30f92562d.png
tags: containers, distrobox

---

# TL;DR.

Distrobox is a container system. The main advantages of using Distrobox include:

* The isolation of container libraries,
    
* Easy access to the host hardware, and
    
* Easy access to the host file system.
    

# Prerequisites.

* A Linux-based distro (I use Ubuntu), and
    
* [A Docker installation](https://solodev.app/installing-docker).
    

# An Introduction.

Distrobox is a utility that allows me to run other Linux distributions in my terminal. The advantage is that I can then run any app that was specifically designed for that distro. For example, I can run DaVinci Resolve on CentOS 7 in Distrobox on Ubuntu:

> The purpose of this post is to demonstrate the installation process for Distrobox.

# The Big Picture.

When it comes to container solutions, I usually reach for LXD/LXC (LinuX Daemon, the container manager, and the LinuX Containers themselves). The advantage is that running LXCs are isolated and, by default, cannot interfere with other containers or the (base) system. However, it is cumbersome getting data out of, and putting data into, a running LXC. This is where Distrobox shines. Although running processes are isolated, those processes can easily access the (base) file system and, if needed, the computer hardware as well.

# Updating my System.

* From the (base) terminal, I update my (base) system:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is Distrobox?

Distrobox is a tool that allows me to run any Linux distribution within my terminal. It enables both backward and forward compatibility with any software, and the freedom to use whichever distribution I'm most comfortable with. Distrobox uses Podman, Docker, or Lilipod to create containers using the Linux distribution of my choosing. It aims to run any software, on top of my host system, without any hassle.

[https://distrobox.it/](https://distrobox.it/)***↗.***

## Installing Distrobox.

* I use the `Curl` command to download, and run, the Distrobox installation script:
    

```bash
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sudo sh
```

> NOTE: If I'm nervous about running a foreign script, I can always download it and manually check its contents.

* After installation, the terminal displays the following:
    

```bash
 Checking dependencies...
 Downloading...
 Unpacking...
 Installation successful!
 Shell scripts are located in /usr/local/bin
 Manpages are located in /usr/local/share/man/man1
```

* I reboot my system to load the Distrobox settings into memory.
    

## Uninstalling Distrobox.

* The following `Curl` command removes Distrobox:
    

```bash
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/uninstall | sudo sh
```

## Distrobox Environment Commands.

* I run the following to display a list of Distrobox commands:
    

```bash
distrobox
```

# The Results.

Distrobox presents a powerful solution for managing Linux distributions, offering seamless integration with my host system. By isolating container libraries, providing easy access to host hardware, and ensuring straightforward interactions with the host file system, it enhances the versatility of my software development environments. Whether for development, testing, or running different applications in isolated environments, Distrobox simplifies the process, making it accessible those who are new to container technology. With Distrobox installed, I gain the ability to run a wide range of GUI and CLI applications directly from their preferred distributions, breaking down compatibility barriers and fostering a more productive computing experience.

# In Conclusion.

Have I ever felt limited by my Linux distribution? Distrobox changes the game by allowing me to run *any* Linux distribution within my terminal. It's about giving me the flexibility to wrap my software in a layer of simplicity.

Here's why Distrobox is a game-changer:

* Isolates container libraries.
    
* Ensures easy access to host hardware.
    
* Provides straightforward access to the host file system.
    

Prerequisites? Just a Linux-based distro (I’m on Ubuntu) and Docker. That’s it. Installing Distrobox is a breeze with a simple `Curl` command. But what truly sets Distrobox apart is its ability to offer both backward and forward compatibility with any software. It uses Podman, Docker, or Lilipod to create containers, making any software run on top of my host system without hassle.

The results? A powerful solution for managing Linux distributions, enhancing the versatility of software development environments, and breaking down compatibility barriers. Distrobox is not just a tool; it's a revolution for Linux users, making computing experiences more productive and enjoyable.

Learn more about Distrobox here: [https://distrobox.it/](https://distrobox.it/)

Have you tried Distrobox yet? What has your experience been like? Let's discuss below!

Until next time: Be safe, be kind, be awesome.

#Linux #Distrobox #SoftwareDevelopment #ContainerTechnology #OpenSource #TechTips #LinuxContainers #DevOps #Coding #Technology