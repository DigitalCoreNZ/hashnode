---
title: "3 of 10: Docker in a LinuX Container."
datePublished: Wed Jun 21 2023 08:03:17 GMT+0000 (Coordinated Universal Time)
cuid: clj5fgbyn001909mo2y9uh8fk
slug: 3-of-10-docker-in-a-linux-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999309541/a16fac53-7f47-477d-baa8-9a6f673da493.png
tags: docker, lxc, rsa, hardening, lxd

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | Docker | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

Create a Docker-compatible <mark>L</mark>inu<mark>XC</mark>ontainer, set up storage, install Docker within the container, add a user account, and install an SSH server for security.

## An Introduction.

My previous post in this 8-part mini-series covered [how I installed LXD on my remote `homelab` system](https://solodev.app/2-of-8-lxd-on-my-homelab). This time, I'm going to show *how* I create a remote container for running Docker.

> The purpose of this post is to present the process of running Docker within an LXD container.

Containers are great [virtualization environments](https://solodev.app/the-magic-of-virtualization) because they isolate running processes from my `homelab` system. After running these containers, I can easily delete any of them. <mark>L</mark>inu<mark>XC</mark>ontainers (LXCs) are better than virtual machines because they use fewer resources while running their virtual processes.

In a previous post, I discussed installing [the LXD container manager](https://solodev.app/1-of-5-lxd-on-my-homelab) on my `homelab` system. This time, I'm going to *use* LXD to create a container, make it Docker-compatible and, after deploying the container, install Docker *within* that container.

## The Big Picture.

It's Big Picture time and, if I go high enough, I can peek over the horizon. The advantage of a 10,000-metre-high view is I can see where I want to go (strategic planning) and decide if what I'm about to do (tactical activity) will help, or hinder, my progress toward a mid-term goal.

In the mid-term, I want to configure a number of services where I try to arrange them into easy-to-maintain, yet simple to expand, structures. Once this goal is achieved, I can then look into horizontal scaling as a form of fail-over protection. (I've given myself until the end of June 2023 to decide on the configuration of my long-term service operations.)

In the short term, I need a platform where I can create a number of services, connect these services into different configurations, simulate the loads these services will encounter, and measure their responses under ever-increasing pressure.

Now that I know what I want to achieve, it's time to build the first part of my lab.

## Creating an LXC Image for Docker.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683422567413/4b5f131b-ba87-4ffc-ad3f-0c5526903bc4.png align="center")

> NOTE: Remember, LXC (lek-see) is an abbreviation for <mark>L</mark>inu<mark>XC</mark>ontainer.

These are the steps I follow after opening a terminal (CTRL + ALT + T).

* From the `homelab` terminal, I initialise an image called `docker` that is built with the `Ubuntu 22.04` image:
    

```bash
lxc init ubuntu:22.04 docker
```

* I list all the images and containers that are available on the system. (There should only be one image listed (it's an image because the STATE is STOPPED)):
    

```plaintext
lxc ls
```

> NOTE: Images and containers are THE SAME THING, but exist in different states. When starting an image, it changes to being a container. When a container is stopped, it changes back to being an image. Again, images are static snapshots while containers are running (dynamic) instances.

The next step is to create storage for the container.

> **Attribution:**  
> [blog.simos.info](http://blog.simos.info)

## OPTIONAL: Creating Storage for the Container.

![](https://images.pexels.com/photos/117729/pexels-photo-117729.jpeg?cs=srgb&dl=pexels-azamat-esenaliev-117729.jpg&fm=jpg&w=640&h=427 align="center")

In the previous post, [I installed (and initialised) the LXD container manager](https://solodev.app/2-of-8-lxd-on-the-homelab). As part of that process, I *could have* created a ZFS pool on the external partition. Docker does not support ZFS, but it does support BTRFS. Therefore, this section involves setting up a BTRFS pool.

* From the `homelab` terminal, I create a storage pool called `docker-pool` that uses the `btrfs` file system:
    

```bash
lxc storage create docker-pool btrfs
```

* I create a volume called `docker-vol` within `docker-pool`:
    

```plaintext
lxc storage volume create docker-pool docker-vol
```

* I attach the `docker` image to a new device called `docker-hdd`:
    

```plaintext
lxc config device add docker docker-hdd disk pool=docker-pool source=docker-vol path=/var/lib/docker-hdd
```

> NOTE: Devices can be added to, or removed from, a running container. VMs also support hotplugging for some [device types](https://linuxcontainers.org/lxd/docs/latest/reference/devices/#devices), but not all.

* I list the volumes within the `docker-pool` storage pool:
    

```plaintext
lxc storage volume list docker-pool
```

> NOTE: Although the`docker-pool` storage pool is used by 1 device, the `docker-hdd` device I configured in the previous step, I can easily connect other devices to this storage pool.

Here are my results:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683513441704/77b323c0-2721-402e-b507-aba01827b508.png align="center")

The next step is to tweak the Docker image.

## Tweaking the Docker Image.

![](https://images.pexels.com/photos/5584158/pexels-photo-5584158.jpeg?cs=srgb&dl=pexels-jessica-lewis-creative-5584158.jpg&fm=jpg&w=640&h=480 align="center")

Running a container system, like Docker, within another container system, like LXD, will cause issues that need addressing.

* From the `homelab` terminal, I set nesting to true:
    

```bash
lxc config set docker security.nesting true
```

* I set mknod to true:
    

```bash
lxc config set docker security.syscalls.intercept.mknod true
```

* I set setxattr to true:
    

```bash
lxc config set docker security.syscalls.intercept.setxattr true
```

* I show the `docker` configuration to check these settings:
    

```bash
lxc config show docker
```

The next step is to install a Docker instance within the container.

> **Attribution:**  
> [ubuntu.com](http://ubuntu.com)

## Installing Docker within the Container.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683426169718/1b9050e0-b618-4d84-ad48-5b793705cf85.png align="center")

* From the `homelab` terminal, I start the `docker` image:
    

```plaintext
lxc start docker
```

* I bash into the `docker` container:
    

```bash
lxc exec docker -- bash
```

* I update and upgrade the container:
    

```bash
apt clean && apt update && apt dist-upgrade -y && apt autoremove -y
```

* I install the following requirements:
    

```plaintext
# apt install -y ca-certificates curl gnupg lsb-release
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
    

```plaintext
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update the local repo (and everything else):
    

```bash
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install `Docker` and its peripherals:
    

```plaintext
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

* I check if `Docker` is active:
    

```plaintext
systemctl is-active docker
```

* I check the status of `Docker`:
    

```bash
service docker status
```

Here are my results:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683515578740/0b435223-0ae5-4d4d-a544-cb0a9881a0fd.png align="center")

* I check the `Docker` version:
    

```bash
sudo docker version
```

Here is my result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684661359789/2f32345a-ef52-48c9-9f58-828a05d32050.png align="center")

* I list the information for Docker:
    

```bash
sudo docker info
```

Here is my result:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684661304047/b5cf94f1-9f78-43f6-a8d8-832845eef859.png align="center")

* I verify the installation:
    

```plaintext
sudo docker run hello-world
```

And again, here are my results:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683516064458/c54800c8-bebb-4da7-982e-b620223949a5.png align="center")

* I exit the Docker container:
    

```bash
exit
```

The next step is to check the storage pool.

> **Attribution:**  
> [ubuntu.com](http://ubuntu.com)

## Checking the Storage Pool.

![](https://images.pexels.com/photos/8657665/pexels-photo-8657665.jpeg?cs=srgb&dl=pexels-mo-eid-8657665.jpg&fm=jpg&w=640&h=360 align="left")

* From the `homelab` terminal, I display a list of all the available storage pools:
    

```plaintext
lxc storage list
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687326006211/efda376f-9bea-47c0-8ff3-aa75415b7102.png align="center")

* I show detailed information about the default pool:
    

```plaintext
lxc storage show default
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687326977423/d6a4cf9c-c845-4f5d-8eb6-aa8d6c3ed912.png align="center")

* I display the usage information for the default pool:
    

```plaintext
lxc storage info default
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687327195045/c99b1940-4ee0-46c7-97df-6a12a38d8e56.png align="center")

> NOTE: The <mark>total space</mark> listed above (2.73TB formatted) is the same as the <mark>size</mark> listed below (3.0TB unformatted):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687327741116/a04330c0-0777-4bef-9468-25983f345c74.png align="center")

* I list all the available storage volumes in the default pool:
    

```plaintext
lxc storage volume list default
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687327373810/59181a25-7afe-42f0-8208-e87531c0a0d7.png align="center")

The next step is to add a user account to the Docker container.

## Adding a User Account to the Docker Container.

![](https://images.pexels.com/photos/8761744/pexels-photo-8761744.jpeg?cs=srgb&dl=pexels-pavel-danilyuk-8761744.jpg&fm=jpg&w=640&h=427 align="left")

* From the `homelab` terminal, I bash into the `docker` container:
    

```plaintext
lxc exec docker -- bash
```

* I add a new user:
    

```plaintext
adduser yt
```

* I add the new user to the `sudo` group:
    

```plaintext
usermod -aG sudo yt
```

* I exit the container:
    

```plaintext
exit
```

The next step is to install OpenSSH within the container.

## Installing OpenSSH within the Docker Container.

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

## Configuring the SSH File in the Container.

This section will open up the container so it can be accessed with a username and password. This is the reason why I added a user account, and password, to the container: To gain access to the container from my `workstation` terminal.

* Within the Docker container, I open the "sshd\_config" file:
    

```plaintext
nano /etc/ssh/sshd_config
```

* I edit, and save, the following "sshd\_config" settings:
    

```plaintext
PasswordAuthentication yes
```

> NOTE: I will return to this file later in the post specifically to alter this, and other, settings.

* I test the SSH configuration:
    

```plaintext
sshd -t
```

* I restart the SSH system:
    

```plaintext
sudo systemctl restart ssh.service
```

* I `reboot` the container:
    

```plaintext
sudo reboot
```

* And finally, on the remote `homelab` system, I display the IP address for the new container:
    

```plaintext
lxc ls
```

Now that I have OpenSSH installed, the next step is to harden the container with UFW and Fail2Ban.

## Enabling, and Setting Up, UFW.

![firewall](https://images.pexels.com/photos/241028/pexels-photo-241028.jpeg?cs=srgb&dl=pexels-pew-nguyen-241028.jpg&fm=jpg&w=640&h=427 align="left")

Yes, the Uncomplicated FireWall was [installed on the `homelab` system](https://solodev.app/2-of-8-lxd-on-the-homelab#heading-enabling-and-setting-up-ufw). This time, I am installing the "hardening" tools within the Docker container.

* Within the Docker container, I check the UFW status:
    

```plaintext
sudo ufw status
```

* I enable the UFW:
    

```bash
sudo ufw enable
```

* I install a UFW rule:
    

```plaintext
sudo ufw allow from 192.168.?.?
```

> ***NOTE: I replace the IP address above with the actual address for the***`workstation`***, e.g. 192.168.188.41.***

* I check the status of the UFW:
    

```plaintext
sudo ufw status
```

> NOTE: UFW will, by default, block all incoming traffic, including SSH and HTTP.

> ANOTHER NOTE: I will update the UFW rules as I deploy other services to the container.

* I list the UFW rules by number:
    

```plaintext
sudo ufw status numbered
```

* I delete a UFW rule by number:
    

```plaintext
sudo ufw delete 1
```

* I disable UFW if required:
    

```plaintext
sudo ufw disable
```

Now that the UFW is setup, let's install another tool for hardening a system: Fail2Ban.

> **Attribution:**  
> [digitalocean.com](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

## Installing, and Setting Up, Fail2Ban.

![stop](https://images.pexels.com/photos/9166266/pexels-photo-9166266.jpeg?cs=srgb&dl=pexels-jan-van-der-wolf-9166266.jpg&fm=jpg&w=640&h=427 align="left")

Fail2Ban protects Linux systems against many security threats, such as dictionary, DoS, DDoS, and brute-force attacks.

* Within the Docker container, I install Fail2Ban:
    

```bash
sudo apt install fail2ban -y
```

* I change to the fail2ban directory:
    

```plaintext
cd /etc/fail2ban
```

* I copy the `jail.conf` file as `jail.local`:
    

```plaintext
sudo cp ./jail.conf ./jail.local
```

* I open the `jail.local` file in Nano:
    

```plaintext
sudo nano ./jail.local
```

* I change a few (SSH-centric) settings in the `jail.local` file, then I save those changes, and exit the Nano editor:
    

```plaintext
[DEFAULT]
. . .
bantime = 1d
maxretry = 3
. . .
destemail = your@email.here
sendername = Fail2Ban on Homelab

[sshd]
enabled = true
port = ssh,22
```

* I restart Fail2Ban:
    

```plaintext
sudo systemctl restart fail2ban
```

* I check the status of Fail2Ban:
    

```plaintext
sudo systemctl status fail2ban
```

* I enable Fail2Ban to autostart on boot:
    

```plaintext
sudo systemctl enable fail2ban
```

Now that I have hardened the Docker container, the next step is to create, and use, RSA keys from my `workstation` terminal.

## Creating, and Using, RSA Keys.

These steps will enable SSH sessions to the remote container, across the LAN, without needing a password.

## Creating an RSA Key Pair on the Local Workstation.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I start the ssh-agent:
    

```plaintext
eval "$(ssh-agent -s)"
```

* I generate a pair of RSA keys called "/home/brian/.ssh/container-name" (where I replace "container-name" with the *actual* name of the container):
    

```plaintext
ssh-keygen -b 4096
```

> NOTE: It is my convention to name RSA keys after the container or system on which they will be used.

* I add my SSH private key to the ssh-agent (where I replace "container-name" with the *actual* name of the container):
    

```plaintext
ssh-add /home/brian/.ssh/container-name
```

The next step is to upload the local public key to the remote Docker container.

## Uploading a Public Key to the Remote Container.

* From the `workstation` terminal, I use "ssh-copy-id" to upload the locally-generated public key to the remote container (where I replace "container-name" with the *actual* name of the container):
    

```plaintext
ssh-copy-id -i /home/brian/.ssh/container-name.pub yt@192.168.?.?
```

> NOTE: I replace the "?" with the actual IP address for the container.

The next step is to use SSH to login to the remote container.

## Using SSH to Login to the Remote Container.

* From the `workstation` terminal, I login to the “yt” account of the remote container:
    

```plaintext
ssh 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

The last step is to apply more hardening to the container.

## More Hardening of the Container.

* From the `workstation` terminal, I open the "sshd\_config" file in the remote container:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I edit, and save, the following "sshd\_config" settings:
    

```plaintext
PermitRootLogin no
PasswordAuthentication no
Protocol 2
```

> NOTE: Another change I typically make is switching out the default port number of 22 for something less obvious, e.g. 4444 (which is also too  
> obvious so don't use port 4444):
> 
> ```plaintext
> port 4444
> ```

* I restart the "ssh" service:
    

```plaintext
sudo systemctl restart ssh.service
```

* I reboot the remote container:
    

```plaintext
sudo reboot
```

> NOTE: Running the `exit`, `sudo reboot`, or `sudo poweroff` commands will close the connection to the remote `homelab` host.

* Finally, I test the connection to the remote container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the -p(ort) number with the actual port defined in the "sshd\_config" file, and replace the "?" with the actual octet for the container.

And that's it.

## The Results.

This post demonstrated how to create a Docker-compatible <mark>L</mark>inu<mark>XC</mark>ontainer, set up storage for Docker, install Docker within the container, add a user account to the container, install an SSH server, create RSA keys on another PC, upload the public key to the Docker container, connect to the Docker container without using a username or password, and further harden the container by disabling the PasswordAuthentication feature. Understanding the appropriate use of virtual machines, LXCs, and Docker containers is crucial in modern engineering, as each technology offers unique benefits and efficiencies.

## In Conclusion.

LXCs are great virtualization technologies because they are more resource-efficient than virtual machines. For the sake of clarity, I should also point out that Docker containers are way more efficient than LXCs. Of course, unlike virtual machines and LXCs, Docker containers do NOT run operating systems.

I think virtual machines, LXCs, and Docker containers, have their roles to play in modern engineering. The trick lies in knowing which to use for any given problem.

Be sure to check out my next post in this series where I install a local copy of Docker Desktop and connect it to the remote container.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | Docker | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)