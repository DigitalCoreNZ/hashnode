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
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748580985843/c31a04e6-1167-4ce8-8d50-428c4b18ed88.png align="center")

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
    

Below is a Proxmox VE container where the `Edit: Network Device (veth)` is open:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749459270865/e221bbf5-087e-446c-b58d-b8a42f66181b.png align="center")

> NOTE: There are prerequisites that I need to meet before I can build this container.

---

## Running the Helper Script.

* I visit [http://helper-scripts.com/](http://helper-scripts.com/).
    
* I search for ‘proxmox ve post install‘.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749449711896/6bccba72-3d65-450e-90cb-d82b76186c7d.png align="center")

* I copy the script command.
    
* I open a local terminal.
    

> NOTE: I can run the following commands from a browser that is logged into Proxmox VE by going to `Datacenter > pve > Shell`. However, the text is very small, so I am using a local terminal instead.
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749453209487/0fcd70a6-cc89-424e-945f-9cf17124c194.png align="center")

* I use the ssh (secure shell) command to login to the remote Proxmox VE:
    

```bash
ssh root@192.168.0.60
```

* The password is the same one I use when logging in to the Proxmox VE browser GUI:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749450728113/d3f959e7-57ed-4d87-9c2f-3fb81b02e889.png align="center")

* I paste the helper script command into the terminal:
    

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/tools/pve/post-pve-install.sh)"
```

> NOTE: Answer ‘yes’ to MOST of the questions when asked but there are 3 exceptions, as listed below.

* I answer ‘no’ to ‘Disable high availability?’:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451321563/2c94ed4f-12a3-4e6c-8da4-f39afc64b811.png align="center")

> NOTE: High availability will be used when other nodes are created.

* I answer ‘no’ to ‘Update Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451488029/9440bbae-c167-4acb-9e48-6d8cd2e6c6fc.png align="center")

> NOTE: I will update Proxmox manually.

* I answer ‘no’ to ‘Reboot Proxmox VE now?‘:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749451626813/9ee7cf61-d8db-4a69-9497-d6b48177c869.png align="center")

> NOTE: I will reboot once I finish updating the remote system and upgrading Proxmox VE.

* Once the script returns me to the terminal screen, I update the system:
    

```bash
apt update
```

> NOTE: Sudo is not required as I am in the root account which has full privileges.

* Once the updates have been downloaded, but not installed, I run the following command to update the system and the Proxmox VE installation:
    

```bash
pveupgrade
```

* Due to the installation of a kernel update, I will reboot the remote Proxmox VE system:
    

```bash
reboot
```

> NOTE: The `reboot` command will automatically end the session between my local terminal and the remote Proxmox VE system.

---

## Downloading an OS to Proxmox VE.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve > local (pve)`.
    
* In the 2nd pane, I click `ISO Images`.
    
* In the 3rd pane, I click the grey `Download from URL` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748583261047/5dec42a4-c9a5-4145-bf16-0c40c9851da5.png align="center")

* In the pop-up modal, I add `https://releases.ubuntu.com/24.04.2/ubuntu-24.04.2-live-server-amd64.iso` to the `URL:` field so that Proxmox VE can download the ISO for Ubuntu Server 24.04.2 LTS.
    
* I click the blue `Query URL` button to check the link:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748583371806/f47fc57d-dc6d-431d-b716-e714682dcf29.png align="center")

* I click the blue `Download` button to start the download:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748583422133/5f088bef-c1ab-4118-8c25-5397dbd4c1c5.png align="center")

---

### **Initializing Drives for Containers and Virtual Machines**.

> NOTE: The following is adapted from the instructions provided by the [Proxmox VE team](https://forum.proxmox.com/threads/proxmox-beginner-tutorial-how-to-set-up-your-first-virtual-machine-on-a-secondary-hard-disk.59559/).

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve`.
    
* In the 2nd pane, I click `Disks`.
    
* In the 3rd pane, I select the `dev/sda` drive (that currently has 2 partitions).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748584828748/d362dea2-a48d-4329-acde-d10cc182c880.png align="center")

* I click the grey `Wipe Disk` button.
    
* In the Confirm modal, I click the blue `Yes` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748584945425/544abe54-3909-4a63-b5bb-c9da498b967d.png align="center")

* I repeat the process for the `/dev/sdb` disk.
    
* Back in the 2nd pane, I click `Disks > LVM`.
    
* In the 3rd pane, I click the grey `Create: Volume Group` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748582841385/eebcb312-a152-4947-af16-c75e0f615f40.png align="center")

* In the `Create: LVM Volume Group` modal, I select the `/dev/sda` disk:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748585198379/c52aba41-999a-409b-987f-e34e15d60cb0.png align="center")

* I name the Group ‘Containers’, ensure the `Add Storage:` option is ticked, and click the blue `Create` button.
    
* I repeat the process for the `/dev/sdb` drive, except I name that group ‘VMs‘.
    

> NOTE: The `/dev/sda` disk is an internal SSD that uses the SATA interface while the `/dev/sdb` disk is an external HDD that uses the USB 3.0 interface.

### Installing a CT Template.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve > local (pve)`.
    
* In the 2nd pane, I click `CT Templates`.
    
* In the 3rd pane, I click the grey `Templates` button.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748594820627/9590ab68-d3b6-4fe7-8b6a-f1ee28ca53bd.png align="center")

* In the Templates modal, I select the `ubuntu-24.04-standard` template and click the blue `Download` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748595021450/77932deb-e7d9-4e1b-97e7-3320ef1d43b1.png align="center")

> Now that all of the requirements are in place, I can take the next step by using a browser to login to Proxmox VE, clicking the blue `Create CT` button (top-right of the screen), following the resulting prompts, and creating a container.

---

## Creating a New Account for the Container.

> After creating a container by clicking the blue `Create CT` button (top-right of the screen), and following the resulting prompts, I can now prepare the container for use.

* I use a browser to login to Proxmox VE.
    
* On the left of the screen, under Server View, I go to `Datacenter > pve > 101 ServerLab1` (where the `CT ID` and `Hostname` are the settings I gave when creating the container).
    
* In the 2nd pane, I click `Console`.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749339376114/12db2ba9-f96c-456e-9de0-819f84cf8d97.png align="center")

* In the 3rd pane, I login to the container using root as the `ServerLab1 login` and the same password I use to login to Proxmox VE.
    
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

* Towards the top-left of the console window, I open the drop down menu of the `Shutdown` option, by clicking the down arrow (⌄), and selecting `Reboot`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749339991320/4e5f0757-6541-40df-b769-68ac8cc7baed.png align="center")

---

## Logging In from a Remote Terminal.

* I open a local terminal.
    
* I use the ssh (secure shell) command to login to the remote container:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749340859602/048b8c43-5dc0-4ee4-a219-7533eb4b3c70.png align="center")

> NOTE: My `yt` account is temporary, is used for generating screenshots, and will be deleted after it has served its’ purpose.

---

## The Results.

Installing Proxmox VE on an Intel NUC 10 provides a compact and efficient solution for managing virtual environments. The process involves preparing the hardware, creating installation media, and configuring the system to suit my network and storage needs. By following the steps outlined, I can effectively set up a robust virtualization platform that supports both containers and virtual machines. This setup not only maximizes the capabilities of the Intel NUC but also offers flexibility and scalability for various computing tasks.

---

## In Conclusion.

In this guide, I walked through the prerequisites, step-by-step installation process, and tips for optimizing my virtual environment setup. From creating a Proxmox VE installation thumb drive to configuring network settings and initializing drives, the result is an Intel NUC 10 that hosts a container that is accessible across my LAN.

I learned how to download an OS to Proxmox VE, install CT templates, and create new accounts for my first container. By following these steps, I maximized the capabilities of the Intel NUC and now enjoy a robust virtualization platform that supports both containers and virtual machines. This setup offers flexibility and scalability for various computing tasks, making it perfect for tech enthusiasts and professionals alike.

Have you tried setting up Proxmox VE on a spare PC? What challenges did you face, and how did you overcome them? Let's discuss in the comments!

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#ProxmoxVE #IntelNUC #Virtualization #Homelab #Containers #VirtualMachines #Networking #ServerSetup #ServerCluster #Linux #Debian #Ubuntu #TechGuide #TechEnthusiast