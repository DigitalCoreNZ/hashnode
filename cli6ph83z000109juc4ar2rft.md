---
title: "1/3: Setting Up a Remote Container."
datePublished: Fri May 19 2023 20:26:54 GMT+0000 (Coordinated Universal Time)
cuid: cli6ph83z000109juc4ar2rft
slug: 1-of-3-setting-up-a-remote-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701641357830/6e7b6e44-6264-41fc-9ec5-442a3f562d5f.png
tags: lxc, containers, remote-access, homelab, lxd

---

Containers are used to "contain" running processes from interfering with each other and the host system. They belong to the Second Wave of Software Emulators, where Virtual Machines were the First Wave and WASM/WASI is the Third Wave. Emulators "pretend" to be operating systems so processes can run in them.

## Prerequisites.

* A Linux-based distro (I use Ubuntu), and
    
* [An LXD installation](https://solodev.app/2-of-10-lxd-on-the-homelab), if required.
    

## Creating a New Container.

The "container-name" below is a placeholder. This placeholder should be replaced with an actual container name.

* From the `homelab` terminal, I create a new container:
    

```plaintext
lxc launch ubuntu:22.04 container-name
```

* Then I bash into the container:
    

```plaintext
lxc exec container-name -- bash
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

## Adding a User Account to the Container.

![](https://images.pexels.com/photos/8761744/pexels-photo-8761744.jpeg?cs=srgb&dl=pexels-pavel-danilyuk-8761744.jpg&fm=jpg&w=640&h=427 align="left")

* From the `homelab` terminal (`CTRL` + `ALT` + `T`) connected to the container, I create a new user:
    

```plaintext
adduser yt
```

* I add the new user to the 'sudo' group:
    

```plaintext
usermod -aG sudo yt
```

> usermod let's me (-a)ppend the sudo (-G)roup to the 'yt' account.

* I exit the container:
    

```plaintext
exit
```

The next step is to fix the home directory problem.

## Fixing the Home Directory Problem.

I can use Nano to add an entry to the `.bashrc` file.

* From the `homelab` terminal, I log in to the container with the 'yt' account:
    

```plaintext
lxc exec container-name -- su yt
```

* I open the `.bashrc` file with Nano:
    

```javascript
sudo nano ~/.bashrc
```

* I add the following to the bottom of the file, save the changes, and exit Nano:
    

```javascript
cd ~
```

* I reboot the container:
    

```javascript
sudo reboot
```

The next step is to install OpenSSH within the container.

## Installing OpenSSH within the Container.

![](https://images.pexels.com/photos/39624/padlock-lock-chain-key-39624.jpeg?cs=srgb&dl=pexels-pixabay-39624.jpg&fm=jpg&w=640&h=427 align="left")

I can use OpenSSH to block access to this container.

* From the `homelab` terminal, I log in to the container with the 'yt' account:
    

```plaintext
lxc exec container-name -- su yt
```

* I install OpenSSH:
    

```plaintext
sudo apt install openssh-server -y
```

* I can check the status of OpenSSH:
    

```plaintext
sudo systemctl status sshd
```

* If needed, I can enable OpenSSH:
    

```plaintext
sudo systemctl enable --now ssh
```

The next step is to configure the SSH file in the container.

## 'Softening' the Container.

In this section, I will 'soften down' the container so it can be accessed with a username and password. This is the reason why I added a user account, and password, in the sections above: To gain access to the container from my `workstation` terminal.

<mark>THIS IS A TEMPORARY CONDITION AND WILL BE FIXED IN THE </mark> [<mark>NEXT LAB</mark>](https://solodev.app/2-of-3-setting-up-a-remote-connection#heading-hardening-the-container)<mark>.</mark>

* From the `homelab` terminal (`CTRL` + `ALT` + `T`) that is connected to the container, I open the "sshd\_config" file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I edit, and save, the following "sshd\_config" setting:
    

```plaintext
PasswordAuthentication yes
```

> NOTE: I will return to this file in the next post to [fix this, and other, settings](https://solodev.app/2-of-3-setting-up-a-remote-connection).

* I restart the SSH system:
    

```plaintext
sudo systemctl restart ssh.service
```

* I `sudo reboot` the container:
    

```plaintext
sudo reboot
```

* And finally, on the remote `homelab` system, I display the IP address for the new container:
    

```plaintext
lxc ls
```

Now that I have OpenSSH installed, the next step is to [set up a remote connection](https://solodev.app/2-of-3-setting-up-a-remote-connection).

And remember: Be safe, be kind, be awesome.