---
title: "Installing Proxmox VE on a Spare PC."
seoTitle: "Proxmox VE Setup on Intel NUC 10"
seoDescription: "Discover how to install Proxmox VE on an Intel NUC 10. Optimize virtualization with detailed steps and tips for tech enthusiasts."
datePublished: Wed Nov 19 2025 11:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cmbrs4gww000k02l98rdgbwkf
slug: installing-proxmox-ve-on-a-spare-pc
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1763582854257/08b76608-bda7-4561-99a8-6abb859202b6.png
tags: ubuntu, linux, networking, containers, virtualization, virtual-machines, homelab, pve, proxmox, serversetup, techguide, proxmoxve, intelnuc, servercluster

---

## TL;DR.

This post is a comprehensive walk-through on how I install PVE (Proxmox Virtual Environment) on a spare PC. I cover the step-by-step installation process, and tips for optimizing the virtual environment. This article is ideal for tech enthusiasts who want to maximize the capabilities of their Homelab by setting up a robust virtualization platform that supports both containers and virtual machines.

> **Attributions:**
> 
> *A post from* [*Proxmox*](https://proxmox.com/en/) *↗ on* [*setting up a Proxmox VE virtual machine*](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/) *↗, and*
> 
> A video from [Tailscale](https://www.youtube.com/@Tailscale) *↗* about [installing Proxmox VE on a PC](https://www.youtube.com/watch?v=zngSuqCM4d8) ***↗.***

---

## An Introduction.

Containers and virtual machines are technologies that allow operating systems and applications to be isolated within a runtime environment. Depending on the hardware specifications, PVE allows multiple containers and virtual machines to run on a single PC:

> The purpose of this post is to demonstrate how I install PVE and create a container.

---

## The Big Picture.

Learn how I efficiently install PVE on a spare PC with this comprehensive guide. Discover the prerequisites, step-by-step installation process, and tips that I use to optimize my virtual environment setup. PVE is perfect for tech enthusiasts looking to maximize their Homelab PCs.

---

## Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* A USB Thumb Drive.
    

---

## Updating my Base System.

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

## What are the Specs for my Spare PC?

An Intel NUC (Next Unit of Computing) is a small-form-factor computer designed by Intel, which offers a compact and powerful computing solution. This PC typically comes without RAM, storage, or an operating system, allowing me to customize the hardware according to my needs.

### NUC Specifications.

| Model | BXNUC10i3FNHN |
| --- | --- |
| Processor | Intel i3-10110U 2.10GHz Dual Core, 4 Threads, Up to 4.10GHz, 4MB SmartCache |
| Memory | Dual Channel, 2x DDR4-2666 SODIMM slots, 1.2V, 64GB maximum |
| Graphics | Intel UHD Graphics, 1x HDMI 2.0a Port, 1x USB 3.1 Gen 2 (10 Gbps), DisplayPort 1.2 via USB-C |
| Audio | Up to 7.1 surround audio via HDMI or DisplayPort signals, Headphone/microphone jack on the front panel, dual array front mics on the chassis front |
| Peripheral Connectivity | 1x HDMI 2.0 Port with 4K at 60Hz, 1x USB 3.1 Gen 2 (10 Gbps), DisplayPort 1.2 via USB-C, 1x Front USB 3.1 Type A (Gen 2) Port, 1x Front USB 3.1 Type-C (Gen 2) Port, 2x Rear USB 3.1 Type A (Gen 2), 2x Ethernet Ports, 2x Internal USB 2.0 via header |
| Bluetooth |  |
| Storage | 1x M.2 22x42/80 (key M) slot for SATA3 or PCIe X4 Gen3 NVMe, SATA Interface, SDXC slot with UHS-II support |
| Networking | Intel Wi-Fi 6 AX201, Bluetooth, i219-V Gigabit Ethernet |
| Power Adapter | 19VDC Power Adapter |

### Hardware Specifications.

| Memory | 64GB |
| --- | --- |
| Storage | 256GB M.2 internal, 256GB SSD internal, 2TB HDD external |
| OS | A modified Debian LTS kernel running under PVE |

---

## What is PVE?

PVE (Proxmox Virtual Environment) is an open-source virtualization platform designed for setting up hyper-converged infrastructure and, under the GNU AGPLv3 license, can be used for commercial purposes. It lets me deploy and manage containers and virtual machines. PVE is built on a modified Debian LTS (Long Term Service) kernel, and supports two types of virtualization: containers with LXC (Linux Containers) and virtual machines with KVM (Kernel-level Virtual Machines). PVE features a web-based management interface, and there is also a mobile app available for managing PVEs.

---

### Creating a PVE Installation Thumb Drive.

* I download the PVE ISO file from [https://proxmox.com/en/downloads/proxmox-virtual-environment/iso](https://proxmox.com/en/downloads/proxmox-virtual-environment/iso).
    
* I grab a 32GB thumb drive and label it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748578190826/30b36cc8-7598-48ce-bddb-1b1f75a3033c.jpeg align="center")

* I plug the thumb drive into my PC.
    
* I start the `balenaEtcher-1.14.3-x64.AppImage` imaging utility that runs on Ubuntu.
    

> NOTE: There are versions of Balena Etcher for Windows, macOS, and (x64 & x86) Linux.

* I select the 1.57GB ISO file as the source, the 32GB thumb drive as the target, and then I click the blue `Flash` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748578590914/39679041-2ebc-4190-b0bd-a7a0e1540655.png align="center")

* After the ISO has been successfully flashed onto the thumb drive, I eject the thumb drive and remove it from my PC.
    

### Installing PVE.

> NOTE: PVE requires at least 3 drives that are directly connected to the NUC. I have an internal 256GB M.2 drive that uses the NVMe interface labelled `prox-int-nvme`, an internal 256GB SSD that uses the SATA interface which has been split into 2 × 128GB partitions labelled `prox-int-sata1` & `prox-int-sata2`, and an external 2TB HDD that uses the USB 3.0 interface labelled `prox-ext-usb3`. These configurations will be altered during the PVE setup process.

* I plug the PVE installation thumb drive into the NUC.
    
* I power up the NUC.
    
* I follow the installation instructions.
    
* I use the following network settings that work on my LAN:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762487898522/3828686b-8196-4dc1-bb23-00c6ebc09d75.png align="center")

> NOTE: During the Management Network Configuration setup, I can use IPv4 or IPv6 but I CANNOT mix the 2 protocols. The Management Interface is the name of the NIC (Network Interface Card) that is installed in the NUC which, in my case, is eno1. The Hostname (FQDN) only matters if I intend to open, and host, PVE over the Internet. The IP Address (CIDR) is 192.168.0.60/24. The PVE tells the router that this is the IP address it wants. The Gateway is the IP address of my router, which is 192.168.0.1, and is needed to connect PVE to the LAN. The DHCP server is found at 192.168.0.1 because my router includes the server that is responsible for assigning IP addresses.

* After installation, the spare PC will reboot.
    
* At this time, I remove the USB installation thumb drive.
    
* At the login screen, I make a note of the PVE IP address and :port number that is displayed.
    
* On a PC that is connected to the same network as PVE, I open a browser, visit the IP address and :port, and bookmark that address.
    
* At the browser login screen, my user name is ‘root’ and my ‘password’ is the same one I gave during the installation.
    
* From the terminal, I SSH into PVE with root@ip\_address and password.
    

---

## A Note about Routers and DHCP Servers.

My router has 2 jobs:

* Connect to an ISP (Internet Service Provider) that, in turn, provides access to the Internet, and
    
* Route that connection to all the wired, and wireless, devices that share the LAN (Local Area Network).
    

As the name suggests, Internet connectivity is *routed* to all of the linked devices in the LAN. There are many devices, like smart phones, tablets, PCs, notebooks, and others, that use an Internet connection to improve their functionality. Many devices, like smart TVs, *require* that connectivity.

The problem is that all the devices that connect to the LAN require unique identifiers. These identifiers are called IP addresses. But where does a device get an IP address? To solve the IP address problem, my router has a built-in DHCP server where DHCP stands for Dynamic Host Configuration Protocol. Almost all routers have a DHCP server and the purpose of this server is to assign a dynamic IP address to every wired, and wireless, device in the LAN.

In most cases, each device in the LAN is dynamically, i.e. automatically, assigned an IP address from a pool of available, unassigned addresses. Most often, devices will use the same dynamic IP addresses when they connect to the LAN, but sometimes the DHCP server will issue a new IP address. This is a fine solution and is NOT a problem. In most cases.

Servers, however, are special use cases. PVE, as well as the containers and virtual machines it manages, require *static* IP addresses. My NUC 10 will need static IP addresses if it, and the containers, want to be accessible in my local LAN. The reason I need IP addresses *that DO NOT CHANGE* is because I will setup a Kubernetes cluster and each node needs to know how to find each other. (Setting up a cluster is beyond the scope of this post.)

Replacing dynamic IP addresses with static IP addresses requires:

* Accessing my router and making changes to the DHCP settings for each container and virtual machine (which is *also* beyond the scope of this post), and
    
* Reflecting those changes to each container and virtual machine running on PVE.
    

---

## The PVE Server.

PVE (Proxmox Virtual Environment) is the server that hosts the containers and virtual machines I deploy.

---

### Accessing PVE.

* I use a browser to login to PVE:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762491437546/674cff6a-903b-449a-bd9c-885c314008c7.png align="center")

* On the left of the screen, I go to `Datacenter > nuclab60`.
    
* In the 2nd pane, I click ‘Shell‘.
    

---

### The Helper Script.

* In a new browser tab, I visit [http://helper-scripts.com/](https://community-scripts.github.io/ProxmoxVE/).
    
* I search for ‘pve post install‘.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762490969910/44ff4e69-0f0d-4fbc-8aac-9494f3319a82.png align="center")

* I copy the script command.
    

---

### Running the Helper Script.

* Back in the Shell for nuclab60, I run the helper script command from the terminal:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492508747/308667bd-d3eb-4cae-849e-42fffe6c1712.png align="center")

> NOTE: I answer ‘yes’ to MOST of the questions when asked but there are 3 exceptions, as listed below.

* I answer ‘no’ to ‘Disable high availability?’:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451321563/2c94ed4f-12a3-4e6c-8da4-f39afc64b811.png align="center")

> NOTE: High availability will be used when other nodes are created.

* I answer ‘no’ to ‘Update Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451488029/9440bbae-c167-4acb-9e48-6d8cd2e6c6fc.png align="center")

> NOTE: I will update PVE manually later in this post.

* I answer ‘no’ to ‘Reboot Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451626813/9ee7cf61-d8db-4a69-9497-d6b48177c869.png align="center")

> NOTE: I will reboot once I finish updating the remote system and upgrading PVE.

* Once the script has finished, I update the system:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492721385/7aa75a5a-9840-4c12-b3f8-110c06912454.png align="center")

> NOTE: The ‘sudo’ command is not required as the root account has full privileges.

* Once the updates have been downloaded, I run the ‘pveupgrade‘ command to update the system and the PVE installation:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492827888/1c0d9bdb-0f64-4158-a301-656fd97aab91.png align="center")

* Due to the installation of a kernel update, I need to reboot PVE:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762493073753/3d8b8b81-c5d3-459d-ae2d-e82f094d047f.png align="center")

---

## Preparing PVE.

Before I can create any containers or virtual machines, I need to prepare PVE and the assets it will use.

---

### Downloading an OS to PVE.

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > local (nuclab60)`.
    
* In the 2nd pane, I click `ISO Images`.
    
* In the 3rd pane, I click the grey `Download from URL` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762550929041/a1a1eafc-cd6b-4b82-9525-387d8485be5b.png align="center")

* In the pop-up modal, I add [`https://releases.ubuntu.com/24.04.3/ubuntu-24.04.3-live-server-amd64.iso`](https://releases.ubuntu.com/24.04.3/ubuntu-24.04.3-live-server-amd64.iso) to the `URL:` field so that PVE can download the ISO for Ubuntu Server 24.04.2 LTS.
    
* I click the blue `Query URL` button to check the link:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551133028/79464be1-463d-459e-af6b-63d436e0bfb4.png align="center")

* I click the blue `Download` button to start the download:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551187522/dec4a9ea-6852-4a6c-8def-09436d5bd24b.png align="center")

* I close the modal once I receive the ‘TASK OK’ message:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551720898/1cc54434-e656-4592-9b05-37ea637754a7.png align="center")

---

### **Preparing the Disks**.

> NOTE: The following is adapted from the instructions provided by the [PVE team](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/).

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve`.
    
* In the 2nd pane, I click `Disks`.
    
* In the 3rd pane, I select the `dev/sda` drive (that currently has 2 partitions).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762554101378/327bc127-931d-4abc-87c3-c2a10bf15eec.png align="center")

* I click the grey `Wipe Disk` button.
    
* In the Confirm modal, I click the blue `Yes` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762555505727/d3ac8cd5-f7ce-42a2-8e4c-629a8211533a.png align="center")

* I repeat the process for the `/dev/sdb` disk.
    
* Back in the 2nd pane, I click `Disks > ZFS`.
    
* In the 3rd pane, I click the grey `Create: ZFS` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762425971626/4d7d68d7-0bd4-42fa-88b6-ed5d94555007.png align="center")

* In the `Create: ZFS` modal, I add the following details and then click the blue ‘Create‘ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762426262241/b235add3-ef6c-4ec8-9c1b-03cab15e839d.png align="center")

> NOTE: The `/dev/sdb` disk is an external SDD that uses the USB 3.0 interface.

### Installing a Container Template.

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve > local (pve)`.
    
* In the 2nd pane, I click `CT Templates`.
    
* In the 3rd pane, I click the grey `Templates` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762555737511/be9cd9f8-9d45-4ed9-9e4c-083cfabf606a.png align="center")

* In the Templates modal, I select the `ubuntu-24.04-standard` template and click the blue `Download` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762555933959/94fff826-af15-4025-9964-1183783b15cf.png align="center")

> Now that all of the requirements are in place, I can take the next step by clicking the blue `Create CT` button (top-right of the screen), following the resulting prompts, and creating a container.

---

## Creating a New Container

This container is built to be cloned. As such, there is a lot of effort that goes into building it.

---

### “Create CT.”

* I use a browser to login to PVE.
    
* At the top-right of the screen, I click the blue ‘Create CT‘ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762558404220/01f4f41d-36a6-44af-9196-fdc66cdd3a39.png align="center")

* I add details to the ‘General’ tab, then I click the blue ‘Next’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762558556205/07dc05cd-d20f-42b1-aa86-997f1426381d.png align="center")

* I select the ‘Template:’, then I click the blue ‘Next’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762558699395/68981f3e-3df6-4c5e-b79f-30cd11e1cddd.png align="center")

* I select the ‘Storage:‘ (zfs-disk), set the size (56GB), then I click the blue ‘Next’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559126740/052da609-a2e3-4c2f-a6cc-31caf1360e16.png align="center")

* I leave the ‘Cores:‘ set to 1, then I click the blue ‘Next‘ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559170147/84c51057-a488-4fa4-a955-abb032895592.png align="center")

* I set the ‘Memory (MiB):’ (12288), the ‘Swap (MiB):’ (4096), then I click the blue ‘Next‘ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559235214/ddd9768b-fc2f-4d35-a6b4-27b05c51acea.png align="center")

* I set the ‘IPv4/CIDR:’, ‘Gateway (IPv4):’, then I click the blue ‘Next’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559308645/3ba179a5-aef7-4cb9-b173-d4fc253d6ea3.png align="center")

* I leave the DNS settings blank, then I click the blue ‘Next’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559352433/24f69e7d-8a78-4817-a467-9ae65baebded.png align="center")

* I check my settings, then I click the blue ‘Finish’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559398955/a72906ce-494a-448f-a582-82ec3865bbb2.png align="center")

---

### “Start at boot.”

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > 101 (nuclab61)`.
    
* In the 2nd pane, I click `Options`.
    
* In the 3rd pane, I select “Start at boot“ from the list and click the gray `Edit` button.
    
* In the “Edit: Start at boot“ modal, I tick the “Start at boot” option followed by the blue `OK` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763546634367/623125be-b6e2-4f48-9bc9-fb7288798f2c.png align="center")

---

### Creating a User Account for the Container.

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > 101 (nuclab61`):
    
* I start the container.
    
* In the 2nd pane, I click `Console`.
    
* In the 3rd pane, I login to the container using root as the `nuclab61 login:` and the password I created while building the container.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763548852242/34220966-59d6-4c92-8df5-6a66279d3b49.png align="center")

* Once logged in, I create a new user account:
    

```bash
adduser brian
```

* I add the new user to the 'sudo' group:
    

```bash
usermod -aG sudo brian
```

* I log out of the root account for the container:
    

```bash
logout
```

* Towards the top-right of the console window, I open the drop down menu of the `Shutdown` option, by clicking the down arrow (⌄), and selecting `Reboot`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763549124333/0e716d01-684e-4b1e-bb97-cf9f6373eb7a.png align="center")

> Once the reboot is complete, I switch to a terminal on my local PC.

---

## Creating an RSA Key Pair on the Local PC.

* From a terminal (`CTRL` + `ALT` + `T`) on my local PC, I start the ssh-agent:
    

```bash
eval "$(ssh-agent -s)"
```

* I generate a pair of RSA keys called "/home/brian/.ssh/key-name" (where I replace "key-name" with the name of the remote server):
    

```bash
ssh-keygen -b 4096
```

> NOTE: It is my convention to name RSA keys after the remote server on which they will be used.

* I add the SSH key to my workstation account (where I replace "key-name" with the *actual* name of the ssh key):
    

```bash
ssh-add /home/brian/.ssh/nuclab61
```

---

### Uploading the Public Key to the Remote Container.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I use "ssh-copy-id" to upload the locally-generated public key to the remote container (where I replace "container-name" with the *actual* name of the container):
    

```bash
ssh-copy-id -i /home/brian/.ssh/nuclab61.pub brian@192.168.0.61
```

---

### Logging In to the Remote Container.

* From the terminal (CTRL + ALT + T), I login to the account of the remote server:
    

```bash
ssh -i /home/brian/.ssh/nuclab61 'brian@192.168.0.61'
```

> NOTE: I create RSA Key Pairs for the remaining containers.

---

## Preparing the Container.

The next step is to prepare the container for cloning.

---

### Updating the Container.

* I update Ubuntu:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

### Installing the Unattended Upgrades Utility.

* I install the `unattended-upgrades` package:
    

```bash
sudo apt install unattended-upgrades
```

* I manually trigger an Unattended Upgrade:
    

```bash
sudo unattended-upgrade
```

> NOTE: -d is the switch for running this command in debug mode.

* I check the Unattended Updates log to ensure everything is worked as expected:
    

```bash
sudo cat /var/log/unattended-upgrades/unattended-upgrades.log
```

---

### Hardening the Container.

* I open the "sshd\_config" file:
    

```bash
sudo nano /etc/ssh/sshd_config
```

* I add (CTRL + V) the following to the bottom of the "sshd\_config" page, save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor:
    

```bash
PasswordAuthentication no
PermitRootLogin no
Protocol 2
```

* I restart the "ssh" service:
    

```bash
sudo systemctl restart ssh.service
```

---

### Enabling, and Setting Up, UFW on the Container.

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
sudo ufw allow from 192.168.0.2
```

> NOTE: I specify the IP address of the PC from which I will connect using SSH\*\*\*.\*\*\*

* I check the status of the UFW and list the rules by number:
    

```bash
sudo ufw status numbered
```

> NOTE 1: UFW will, by default, block all incoming traffic, including SSH and HTTP.
> 
> NOTE 2: I will update the UFW rules as I deploy other services to the remote server.

* I can delete a UFW rule by number if needed:
    

```bash
sudo ufw delete 1
```

* I can also disable UFW if needed:
    

```bash
sudo ufw disable
```

---

### Installing, and Setting Up, Fail2Ban on the Container.

* I install Fail2Ban:
    

```bash
sudo apt install -y fail2ban
```

* I copy the `jail.conf` file as `jail.local`:
    

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

* I open the `jail.local` file in Nano:
    

```bash
sudo nano /etc/fail2ban/jail.local
```

* I make the following changes to a few (SSH-centric) settings in the `jail.local` file, then I save (CTRL + S) those changes, and exit (CTRL + X) the Nano text editor:
    

```bash
[DEFAULT]
⋮
bantime = 60m
ignoreip = 127.0.0.1/8 your_ip_address
⋮
[sshd]
enabled = true
port = ssh,22
```

* I restart Fail2Ban:
    

```bash
sudo systemctl restart fail2ban
```

* I check the Fail2ban whitelist:
    

```bash
sudo fail2ban-client status
```

* I check the status of Fail2Ban:
    

```bash
sudo systemctl status fail2ban
```

* I enable Fail2Ban to auto-start on boot:
    

```bash
sudo systemctl enable fail2ban
```

* I reboot the container:
    

```bash
sudo reboot
```

---

## “Clone.”

A clone is a direct, functional copy of a container that includes all of the settings from the original. After making the clones, I will adjust the settings of each so they will function correctly.

---

### Cloning the Container.

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60`.
    
* In the second pane, I select “Search”.
    
* In the third pane, I right-click the ‘101 (nuclab61)’ container and, in the pop-up menu, I click the ‘Shutdown’ option if the container is running.
    
* In the third pane, I right-click the ‘101 (nuclab61)’ container and, in the pop-up menu, I click the ‘Clone’ option:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559530710/07abcc6a-5f52-425a-8f88-c11f0d50b77f.png align="center")

* In the ‘Clone CT 101 (nuclab61)’ modal, I enter the following details, then I click the blue ‘Clone’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559671586/b28d6ea9-46df-41f8-ad3f-c137b9f84724.png align="center")

* After a moment, a clone of the original container appears under `Datacenter > nuclab60`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559913550/f7a26f78-bf32-4197-bb75-7705b80f25a8.png align="center")

* I repeat this process two more times to meet my requirements.
    

---

### Network Settings for Each Clone.

* I use a browser to login to PVE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > 101 (nuclab61)`.
    
* In the 2nd pane, I click `Network`.
    
* In the 3rd pane, I select the Network Device and click the gray, `Edit` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763326487766/76e9a27b-02fb-48ca-bca6-9d6095ca8a36.png align="center")

* In the ‘Edit: Network Device’ modal, I change:
    
    * the ‘Name:’,
        
    * Ensure the ‘IPv4:’ radio button is set to ‘Static’,
        
    * Ensure the ‘IPv4/CIDR:’ setting is correct, and
        
    * Ensure the ‘Gateway (IPv4):’ setting is correct:
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763326666045/728c477e-d325-47ba-9024-3b0173e7ba42.png align="center")

* Once I confirm these settings, I click the blue `OK` button and repeat the process for the three remaining containers.
    

---

## Setting Up the Local Terminal.

The following describes:

* How to locally generate an RSA Key Pair for an SSH connection,
    
* Pushing the public key to the container,
    
* Logging in to the remote container,
    
* Updating the OS that is running on the container,
    
* Hardening the container by changing a few settings, and
    
* Installing and enabling security utilities like UFW and Fail2Ban.
    

> NOTE: These operations need to be performed for (and on) each container.

---

## The Results.

Installing PVE (Proxmox Virtual Environment) onto a spare PC results in a compact and efficient solution for creating, and managing, containers and virtual environments. The process involves preparing the installation hardware, creating a USB drive that is used as the installation media, and configuring the system to suit my network and storage needs. By following the steps above, I can set up a robust virtualization platform that supports both containers and virtual machines. This setup not only maximizes the capabilities of the spare PC but also offers flexibility and scalability for various computing tasks.

---

## In Conclusion.

In this guide, I created a USB installation thumb drive for PVE, installed PVE onto a spare PC, learned how to download an OS to PVE, installed CT templates, created a container, created a new account for that container, and cloned that container multiple times. By following these steps, I maximized the capabilities of the spare PC and now enjoy a robust virtualization platform that supports both containers and virtual machines. This setup offers flexibility and scalability for various computing tasks, making it perfect for tech enthusiasts and professionals alike.

Have you tried setting up PVE on a spare PC? What challenges did you face? How did you overcome those challenges? Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#ProxmoxVE #pve #IntelNUC #Virtualization #Homelab #Containers #VirtualMachines #Networking #ServerSetup #ServerCluster #Linux #Debian #Ubuntu #TechGuide