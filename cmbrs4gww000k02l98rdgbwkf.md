---
title: "Installing Proxmox VE on an Intel NUC 10."
seoTitle: "Proxmox VE Setup on Intel NUC 10"
seoDescription: "Discover how to install Proxmox VE on an Intel NUC 10. Optimize virtualization with detailed steps and tips for tech enthusiasts."
datePublished: Wed Jun 11 2025 10:00:40 GMT+0000 (Coordinated Universal Time)
cuid: cmbrs4gww000k02l98rdgbwkf
slug: installing-proxmox-ve-on-an-intel-nuc-10
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1749598613011/87c7b086-7fb6-4a6c-83ba-dfbbfd7698ef.png
tags: ubuntu, linux, debian, networking, containers, virtualization, virtual-machines, homelab, proxmox, serversetup, techguide, techenthusiast, proxmoxve, intelnuc, servercluster

---

## TL;DR.

This post is a comprehensive walk-through on how I install Proxmox VE on an Intel NUC 10. I cover the step-by-step installation process, and tips for optimizing the virtual environment. This article is ideal for tech enthusiasts who want to maximize the capabilities of their Homelab by setting up a robust virtualization platform that supports both containers and virtual machines.

> **Attributions:**
> 
> *A post from* [*Proxmox*](https://proxmox.com/en/) *↗ on* [*setting up a Proxmox VE virtual machine*](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/) *↗, and*
> 
> A video from [Tailscale](https://www.youtube.com/@Tailscale) *↗* about [installing Proxmox VE on a PC](https://www.youtube.com/watch?v=zngSuqCM4d8) ***↗.***

---

## An Introduction.

Containers and virtual machines are technologies that allow operating systems and applications to be isolated within a runtime environment. Depending on the hardware specifications, Proxmox VE allows multiple containers and virtual machines to run on a single PC:

> The purpose of this post is to demonstrate how I install Proxmox VE and create a container.

---

## The Big Picture.

Learn how I efficiently install Proxmox VE on an Intel NUC 10 with this comprehensive guide. Discover the prerequisites, step-by-step installation process, and tips that I use to optimize my virtual environment setup. Proxmox is perfect for tech enthusiasts looking to maximize their Homelab PCs.

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

## What is an Intel NUC?

An Intel NUC (Next Unit of Computing) is a small-form-factor computer designed by Intel, which offers a compact and powerful computing solution. This PC typically come without RAM, storage, or an operating system, allowing me to customize my system according to my needs.

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
| OS | A modified Debian LTS kernel running under Proxmox VE |

---

## What is Proxmox VE?

Proxmox VE (Virtual Environment) is an open-source virtualization platform designed for setting up hyper-converged infrastructure and, under the GNU AGPLv3 license, can be used for commercial purposes. It lets me deploy and manage containers and virtual machines. Proxmox VE is built on a modified Debian LTS kernel, and supports two types of virtualization: containers with LXC and virtual machines with KVM. Proxmox VE features a web-based management interface, and there is also a mobile app available for managing PVEs (Proxmox Virtual Environments).

---

## Creating a Proxmox VE Installation Thumb Drive.

* I download the Proxmox ISO file from [https://proxmox.com/en/downloads/proxmox-virtual-environment/iso](https://proxmox.com/en/downloads/proxmox-virtual-environment/iso).
    
* I grab a 32GB thumb drive and label it.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748578190826/30b36cc8-7598-48ce-bddb-1b1f75a3033c.jpeg align="center")

* I plug the thumb drive into my PC.
    
* I start the `balenaEtcher-1.14.3-x64.AppImage` imaging utility that runs on Ubuntu.
    
* I select the 1.57GB ISO file as the source, the 32GB thumb drive as the target, and then I click the blue `Flash` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748578590914/39679041-2ebc-4190-b0bd-a7a0e1540655.png align="center")

* After the ISO has been successfully flashed onto the thumb drive, I eject the thumb drive and remove it from my PC.
    

### Installing Proxmox VE.

> NOTE: Proxmox VE requires at least 3 drives that are directly connected to the NUC. I have an internal 256GB M.2 drive that uses the NVMe interface labelled `prox-int-nvme`, an internal 256GB SSD that uses the SATA interface which has been split into 2 × 128GB partitions labelled `prox-int-sata1` & `prox-int-sata2`, and an external 2TB HDD that uses the USB 3.0 interface labelled `prox-ext-usb3`. These configurations will be altered during the Proxmox VE setup process.

* I plug the Proxmox VE installation thumb drive into my NUC.
    
* I power up my NUC.
    
* I follow the installation instructions.
    
* I use the following network settings that work on my LAN:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762487898522/3828686b-8196-4dc1-bb23-00c6ebc09d75.png align="center")

> NOTE: During the Management Network Configuration setup, I can use IPv4 or IPv6 but I CANNOT mix the 2 protocols. The Management Interface is the name of the NIC (Network Interface Card) that is installed in the NUC which, in my case, is eno1. The Hostname (FQDN) only matters if I intend to open, and host, Proxmox VE over the Internet. The IP Address (CIDR), as assigned by my router, is 192.168.0.50 with a subnet mask of 24 (255.255.255.0) that defines the subnet in my LAN to which this device belongs. The Gateway is the IP address of my router, which is 192.168.0.1, and is needed to connect the NUC to the Internet. The DHCP server is found at 192.168.0.1 because my router includes the server that is responsible for assigning IP addresses.

* After installation, the NUC will reboot.
    
* At this time, I remove the USB installation thumb drive.
    
* At the login screen, I make a note of the Proxmox VE IP address and :port number that is displayed.
    
* On a PC that is connected to the same network as Proxmox VE, I open a browser, visit the IP address and :port, and bookmark that address.
    
* At the browser login screen, my user name is ‘root’ and my ‘password’ is the same one I gave during the installation.
    
* From the terminal, I SSH into Proxmox VE with root@ip\_address and password.
    

---

## A Note about Routers and DHCP Servers.

My router has 2 jobs:

* Connect to an ISP (Internet Service Provider) that, in turn, provides access to the Internet, and
    
* Route that connection to all the wired, and wireless, devices that share the LAN (Local Area Network).
    

As the name suggests, Internet connectivity is *routed* to all of the linked devices in the LAN. There are many devices, like smart phones, tablets, PCs, notebooks, and others, that use an Internet connection to improve their functionality. Many devices, like smart TVs, *require* that connectivity.

The problem is that all the devices that connect to the LAN require unique identifiers. These identifiers are called IP addresses. But where does a device get an IP address? To solve the IP address problem, my router has a built-in DHCP server where DHCP stands for Dynamic Host Configuration Protocol. Almost all routers have a DHCP server and the purpose of this server is to assign a dynamic IP address to every wired, and wireless, device in the LAN.

In most cases, each device in the LAN is dynamically, i.e. automatically, assigned an IP address from a pool of available, unassigned addresses. Most often, devices will use the same dynamic IP addresses when they connect to the LAN, but sometimes the DHCP server will issue new dynamic IP addresses. This is a fine solution and is NOT a problem. In most cases.

Servers, however, are special use cases. Proxmox VE, as well as the containers and virtual machines it manages, require *static* IP addresses. My Pi5 SBCs (Single Board Computers) will also need static IP addresses if they want to become nodes in my server cluster. The reason each node in a cluster needs an IP address *that doesn’t change* is because they need to know how to find each other.

Replacing dynamic IP addresses with static IP addresses requires:

* Accessing my router and making changes to the DHCP settings for each server node (which is beyond the scope of this post), and
    
* Reflecting those changes to each container, virtual machine, and Pi5 that makes up my server cluster.
    

---

## Accessing Proxmox VE.

* I use a browser to login to Proxmox VE.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762491437546/674cff6a-903b-449a-bd9c-885c314008c7.png align="center")

* On the left of the screen, I go to `Datacenter > nuclab60`.
    
* In the 2nd pane, I click ‘Shell‘.
    

---

## The Helper Script.

* In a new browser tab, I visit [http://helper-scripts.com/](https://community-scripts.github.io/ProxmoxVE/).
    
* I search for ‘pve post install‘.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762490969910/44ff4e69-0f0d-4fbc-8aac-9494f3319a82.png align="center")

* I copy the script command.
    

---

## Running the Helper Script.

* Back in the Proxmox tab, I run the helper script command from the terminal:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492508747/308667bd-d3eb-4cae-849e-42fffe6c1712.png align="center")

> NOTE: I answer ‘yes’ to MOST of the questions when asked but there are 3 exceptions, as listed below.

* I answer ‘no’ to ‘Disable high availability?’:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451321563/2c94ed4f-12a3-4e6c-8da4-f39afc64b811.png align="center")

> NOTE: High availability will be used when other nodes are created.

* I answer ‘no’ to ‘Update Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451488029/9440bbae-c167-4acb-9e48-6d8cd2e6c6fc.png align="center")

> NOTE: I will update Proxmox manually.

* I answer ‘no’ to ‘Reboot Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451626813/9ee7cf61-d8db-4a69-9497-d6b48177c869.png align="center")

> NOTE: I will reboot once I finish updating the remote system and upgrading Proxmox VE.

* Once the script has finished, I update the system:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492721385/7aa75a5a-9840-4c12-b3f8-110c06912454.png align="center")

> NOTE: The ‘sudo’ command is not required as the root account has full privileges.

* Once the updates have been downloaded, I run the ‘pveupgrade‘ command to update the system and the Proxmox VE installation:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762492827888/1c0d9bdb-0f64-4158-a301-656fd97aab91.png align="center")

* Due to the installation of a kernel update, I need to reboot Proxmox VE:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762493073753/3d8b8b81-c5d3-459d-ae2d-e82f094d047f.png align="center")

---

## Downloading an OS to Proxmox VE.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > local (nuclab60)`.
    
* In the 2nd pane, I click `ISO Images`.
    
* In the 3rd pane, I click the grey `Download from URL` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762550929041/a1a1eafc-cd6b-4b82-9525-387d8485be5b.png align="center")

* In the pop-up modal, I add [`https://releases.ubuntu.com/24.04.3/ubuntu-24.04.3-live-server-amd64.iso`](https://releases.ubuntu.com/24.04.3/ubuntu-24.04.3-live-server-amd64.iso) to the `URL:` field so that Proxmox VE can download the ISO for Ubuntu Server 24.04.2 LTS.
    
* I click the blue `Query URL` button to check the link:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551133028/79464be1-463d-459e-af6b-63d436e0bfb4.png align="center")

* I click the blue `Download` button to start the download:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551187522/dec4a9ea-6852-4a6c-8def-09436d5bd24b.png align="center")

* I close the modal once I receive the ‘TASK OK’ message:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762551720898/1cc54434-e656-4592-9b05-37ea637754a7.png align="center")

---

### **Preparing the Disks**.

> NOTE: The following is adapted from the instructions provided by the [Proxmox VE team](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/).

* I use a browser to login to Proxmox VE.
    
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

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve > local (pve)`.
    
* In the 2nd pane, I click `CT Templates`.
    
* In the 3rd pane, I click the grey `Templates` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762555737511/be9cd9f8-9d45-4ed9-9e4c-083cfabf606a.png align="center")

* In the Templates modal, I select the `ubuntu-24.04-standard` template and click the blue `Download` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762555933959/94fff826-af15-4025-9964-1183783b15cf.png align="center")

> Now that all of the requirements are in place, I can take the next step by clicking the blue `Create CT` button (top-right of the screen), following the resulting prompts, and creating a container.

---

## Creating a New Container

* I use a browser to login to Proxmox VE.
    
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

The resulting container can now be cloned.

---

## Cloning the Container.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60`.
    
* I right-click the ‘101 (nuclab61)’ container and, in the pop-up menu, I click the ‘Clone’ option:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559530710/07abcc6a-5f52-425a-8f88-c11f0d50b77f.png align="center")

* In the ‘Clone CT 101 (nuclab61)’ modal, I enter the following details, then I click the blue ‘Clone’ button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559671586/b28d6ea9-46df-41f8-ad3f-c137b9f84724.png align="center")

* After a moment, a clone of the original container appears under `Datacenter > nuclab60`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1762559913550/f7a26f78-bf32-4197-bb75-7705b80f25a8.png align="center")

* I repeat this process two more times to meet my requirements.
    
* Once I have created all the containers I need, I select a container and then clicking the ‘Start’ button near the top-right of the screen:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763064012838/5a477892-980e-4d25-b22c-8b47e3672bb7.png align="center")

---

## Creating a User Account for a Container.

> Now I create user accounts for all of the containers.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > nuclab60 > 101 (nuclab61`):
    
* In the 2nd pane, I click `Console`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763064209330/18c821bb-be78-47d6-94a5-7910873d44bd.png align="center")

* In the 3rd pane, I login to the container using root as the `nuclab61 login:` and the password I created while building the container.
    
* Once logged in, I create a new user account:
    

```bash
adduser <user_name>
```

* I add the new user to the 'sudo' group:
    

```bash
usermod -aG sudo <user_name>
```

* I exit the root account of the container:
    

```bash
exit
```

* Towards the top-right of the console window, I open the drop down menu of the `Shutdown` option, by clicking the down arrow (⌄), and selecting `Reboot`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763064962161/5a6e1985-14a9-497e-b85d-04d2f2da9fc4.png align="center")

---

## The Results.

Installing Proxmox VE on an Intel NUC 10 provides a compact and efficient solution for managing virtual environments. The process involves preparing the installation hardware, creating a USB drive that is used as the installation media, and configuring the system to suit my network and storage needs. By following the steps outlined, I can effectively set up a robust virtualization platform that supports both containers and virtual machines. This setup not only maximizes the capabilities of the Intel NUC but also offers flexibility and scalability for various computing tasks.

---

## In Conclusion.

In this guide, I created a USB installation thumb drive for Proxmox VE, installed Proxmox VE onto a NUC10 PC, learned how to download an OS to Proxmox VE, installed CT templates, created a container, cloned that container multiple times, and created new accounts for those containers. By following these steps, I maximized the capabilities of the Intel NUC and now enjoy a robust virtualization platform that supports both containers and virtual machines. This setup offers flexibility and scalability for various computing tasks, making it perfect for tech enthusiasts and professionals alike.

Have you tried setting up Proxmox VE on a spare PC? What challenges did you face? How did you overcome those challenges? Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#ProxmoxVE #IntelNUC #Virtualization #Homelab #Containers #VirtualMachines #Networking #ServerSetup #ServerCluster #Linux #Debian #Ubuntu #TechGuide #TechEnthusiast