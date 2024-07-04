---
title: "Installing Rust."
datePublished: Thu Feb 29 2024 09:00:16 GMT+0000 (Coordinated Universal Time)
cuid: clt6zw4lf000b08jp0mb50cg9
slug: installing-rust
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705899796183/eeb3cc49-dd8a-454c-a0c1-6c6437135a40.png
tags: rust, lxc, programming-ciovqvfcb008mb253jrczo9ye, developer-tools, systems-programming, rust-lang, rust-programming, linux-container, memory-safety, rustup, rustc, rust-installation, memory-safe

---

# TL;DR.

This post provides a step-by-step guide on how to install Rust, a powerful systems programming language, within a Linux Container (LXC). It covers the creation of the container, adding a user account to the container, fixing the home directory issue, and installing and managing Rust using the `rustup` tool. It also includes instructions on how to uninstall Rustup. The article emphasizes that, despite the simplicity of the installation process, Rust is an incredibly potent language.

> **Attributions:**
> 
> [https://www.rust-lang.org/](https://www.rust-lang.org/)***↗.***

# An Introduction.

Rust is a compiled, (mostly) memory-safe, systems programming language.

> The purpose of this post is to present a process for installing Rust.

# The Big Picture.

Although this is a very short post, the possibilities presented by a Rust installation are wide, and deep, and numerous. I can study the Rust language from the official [Rust Book](https://doc.rust-lang.org/book/) and [Cargo Book](https://doc.rust-lang.org/cargo/index.html), or I can learn from a more [interactive appliance](https://rust-book.cs.brown.edu/). In my opinion, a great way to learn how to use a powerful language like Rust is to build a training app for Rust programming using the Rust language. That's meta. (Here's a real-world comparison to this idea: [A lathe is the only machine that can build itself](https://blog.mmi-direct.com/machining-history-lathe-the-mother-of-all-tools).)

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Installing LXD and Using LXCs](https://solodev.app/installing-lxd-and-using-lxcs), and
    
* [Creating a LinuX Container](https://solodev.app/creating-a-linux-container).
    

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

# What is an LXC and LXD?

An LXC (LinuX Container) is an isolated, OS-level virtualization which, for efficiency, uses the Linux kernel of the host system. An LXC is a virtual environment where system processes within the LXC container can not affect other containers, or the host system, without specifically running certain commands.

The LXD (LinuX Daemon) is the container manager that is used to create, and manage, LXCs (LinuX Containers). It is a background service that can automatically start LXCs when the host system boots, or stop any container from starting at all.

## Creating a Container.

* I create an LXC (LinuX Container) called (`Rust`):
    

```bash
lxc launch ubuntu:22.04 Rust
```

* I bash into the container:
    

```bash
lxc exec Rust -- bash
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

> NOTE: usermod let's me (-a)ppend the sudo (-G)roup to the yt account.

* I reboot the container:
    

```bash
sudo reboot
```

The next step is to fix the home directory problem.

## Setting the LXC Home Directory.

* From the terminal, I log in to the container with the `yt` account:
    

```bash
lxc exec Scrapings -- su yt
```

> NOTE: At the moment, the home directory is `/root`. This section will address the issue by changing the home directory to `~`.

* I use the Nano text editor to open the `.bashrc` file:
    

```bash
sudo nano ~/.bashrc
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `.bashrc` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~
```

## Hardening the Container.

* From within the container, I use the `Nano` text editor to open the `sshd_config` file:
    

```bash
sudo nano /etc/ssh/sshd_config
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `sshd_config` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```bash
PasswordAuthentication no
PermitRootLogin no
Protocol 2
Port = 2424
```

* I `restart` the `SSH` service:
    

```bash
sudo systemctl restart ssh
```

* I reboot the container:
    

```bash
sudo reboot
```

> NOTE: Within the container, I can also install (or enable) [UFW](https://solodev.app/creating-a-local-linux-container#heading-optional-enabling-and-setting-up-ufw), [Fail2Ban](https://solodev.app/creating-a-local-linux-container#heading-optional-installing-and-setting-up-fail2ban), and [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container).

# What is Rust?

Rust is a systems programming language that empowers everyone to build reliable and efficient software. It is blazingly fast and memory-efficient: with no runtime or garbage collector, it can power performance-critical services and run on embedded devices. Rust is focused on performance, memory safety, and safe concurrency.

## Installing Rustup.

> NOTE: The `rustup` tool is used to install, and manage, Rust.

* From the terminal, I log in to the container with the 'yt' account:
    

```bash
lxc exec Rust -- su yt
```

* I use `curl` to download, and run, the `rustup` script:
    

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

* I reboot the container:
    

```bash
sudo reboot
```

## Updating Rustup.

* From the terminal, I log in to the container with the 'yt' account:
    

```bash
lxc exec Rust -- su yt
```

* I use `rustup` to update `rustup`:
    

```bash
rustup update
```

## Testing the Rust Compiler Installation.

* I check the Rust Compiler version:
    

```bash
rustc --version
```

## Uninstalling Rustup.

* I use `rustup` to `uninstall` it`self`:
    

```bash
rustup self uninstall
```

# The Results.

Rust is a powerful, memory-safe, systems programming language. This guide provided step-by-step procedures on how to install Rust within an LXC. I also covered how to add user accounts, fix the home directory issue, and manage Rust using the rustup tool. The installation process was very simple but does not detract from Rust being an incredibly powerful language.

# In Conclusion.

I have now installed Rust, a powerful, memory-safe, systems programming language. This guide described the steps I used to install this language.

Rust opens up a world of possibilities, and it's not as complex to install as you might think.

In this guide, I've installed Rust in an LXC (LinuX Container). I also covered how to add user accounts and fix home directory issue within the LXC, and how to manage Rust using the rustup tool. I also included the uninstall process for Rustup. The installation process is simple but doesn't detract from Rust being a powerful tool.

Whether you're looking to explore Rust for your next project or simply want to add another tool to your programming kit, this guide has got you covered.

Ready to dive into the world of Rust? Have you used Rust before? If so, what projects have you worked on? If not, are you considering giving it a try?

Let's start a conversation below!

Until next time: Be safe, be kind, be awesome.

#Rust #Programming #SystemProgramming #RustInstallation #LXC #LinuxContainer #Rustup #MemorySafety #SystemsProgramming #DeveloperTools