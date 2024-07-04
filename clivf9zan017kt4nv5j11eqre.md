---
title: "2 of 10: LXD on the Homelab."
seoDescription: "Learn to create a secure homelab using LXD, UFW, and Fail2Ban. Prepare storage, initialize LXD, and test LXC commands for efficient development."
datePublished: Wed Jun 14 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clivf9zan017kt4nv5j11eqre
slug: 2-of-10-lxd-on-the-homelab
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999274192/32272a43-181c-42fd-b318-db5a324ef98d.png
tags: lxc, containers, fail2ban, ufw, lxd

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | LXD Manager | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

Updated: Sunday 29<sup>th</sup> October, 2023.

## TL;DR.

LXD is a container manager for creating and managing containers. A remote `homelab`, for me, is simply an Intel NUC (Next Unit of Computing) that hosts containers. Most of my experiments involve passing data between containers.

This article covers setting up my remote `homelab`, hardening the lab with UFW and Fail2Ban, preparing an empty partition for LXD (<mark>L</mark>inu<mark>XD</mark>aemon), installing the LXD manager, initializing LXD, testing a few LXC (<mark>L</mark>inu<mark>XC</mark>ontainer) commands, and listing a few LXC commands that I find useful.

## An Introduction.

![containers](https://images.pexels.com/photos/906494/pexels-photo-906494.jpeg?cs=srgb&dl=pexels-chanaka-906494.jpg&fm=jpg&w=640&h=420 align="left")

My first post in this 8-part mini-series covered [*why* I'm building a `homelab`](https://solodev.app/1-of-8-my-first-homelab-a-brief-introduction). This time, I'm going to show *how* I'm setting up my remote `homelab` system.

> The purpose of this post is to present my process for running LXD on my `homelab`.

My focus throughout this post is to describe how I download and deploy the [LXD container manager](https://ubuntu.com/lxd) onto my remote, Ubuntu-based `homelab` system.

LXD is what I use to create *some* of my containers.

> NOTE: Actually, there are *TWO* container technologies I want to use at my startup:
> 
> * LXD (which I'll explain in a moment), and
>     
> * Docker (which I'll cover over the the remaining *FOUR* posts that make up this mini-series.)
>     

LXD stands for <mark>L</mark>inu<mark>XD</mark>aemon and is pronounced: "lexdee". This is a container manager that runs as a background process on my `homelab`. It is a tool that helps me manage the containers that I "spin up", "tear down", and use.

LXC stands for <mark>L</mark>inu<mark>XC</mark>ontainer and is pronounced: "lexsee". These are the container instances that can run concurrently on a single host. These containers use the Linux kernel of the host system, as well as other OS resources, to reduce the overhead of running multiple, isolated occurrences.

> NOTE: I can also spin up a virtual machine by using the `--vm` flag. When they're initialised, virtual machines download, and use, a kernel *within* the container itself. Virtual machines are useful when I need functionality that is not supported by the host kernel, or when I want to run a completely different operating system form the host.

## The Big Picture.

This is part 2 of an 8-part mini-series, and a great way to introduce a high concept like mine is to have a 10,000-metre overview. Here's the thing: What I'm about to describe might *blow your mind* and you *may* need to wipe some brain matter off your monitor. Keep some tissues handy.

Containers are technical constructs that I use to test the viability of my ideas and concepts. Remember, I'll be running containers on my `homelab` and, as the name implies, I'll be using this "lab" to conduct my experiments.

The results from each experiment will result in a write-up. That's the purpose of these posts; to describe:

* The methods I use,
    
* The results I achieve, and
    
* The conclusions I make.
    

That's right, I'm using the Scientific Method as the foundation for my posts. This entire blog should provide a clear path for engineers to follow while empowering them to modify these methods to meet their own needs.

As I mentioned, containers are technical entities, but they are *also* conceptual models. This means that containers can represent real-world, hosted servers (provided by Linode, Digital Ocean, etc.). The interactions these servers might have with each other will be patterned after successful container experiments that I'll run on my `homelab`. In other words, the services these containers provide will eventually run on *actual* servers. The way I'll make my containers work together shows how I want my hosted servers to work together.

For a solo developer like me, using containers to realise my Technical Designs, and then running security checks and ethical hacks on (and from within) these containers is simply *one* practice (among many) that may be used to validate my designs.

Truthfully, I have no idea how I'm going to build these tests, but that's the whole point of building a `homelab`. For developing my tests, I would probably develop a proto-method, run the experiments, and publish the results, e.g: Step 1 - Ask the Internet. Step 2 - Build a construct. Step 3 - Simulate a load. Step 4 - Measure the results. Step 5 - Change a parameter. Step 6 - Return to Step 3.

This is the big picture, every picture tells a story, and my story starts here.

First, I'll start by providing my local `workstation` system with access to the remote `homelab` system while blocking *EVERY OTHER SYSTEM IN THE WORLD*.

## Enabling, and Setting Up, UFW.

![firewall](https://images.pexels.com/photos/241028/pexels-photo-241028.jpeg?cs=srgb&dl=pexels-pew-nguyen-241028.jpg&fm=jpg&w=640&h=427 align="left")

The <mark>U</mark>ncomplicated <mark>F</mark>ire<mark>W</mark>all is a wrapper utility that makes setting up, and using, `iptables` very simple. It is easy to learn and extremely user-friendly. UFW is the first utility, in a toolbox of devices, that is used to "harden" a system.

Hardening is the process of reducing an "attack surface", and blocking potential "vectors", that malicious actors *could exploit* to execute their virulent activities. In other words, I will use *any* tool, and change *any* setting, to minimise the chances of "black hats", cyber-criminals, and/or foreign states, using my systems to harm others.

* On the remote `homelab` system, I run the updates and upgrades:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I check the UFW status:
    

```plaintext
sudo ufw status
```

* I enable the UFW:
    

```bash
sudo ufw enable
```

* I install a UFW rule:
    

```plaintext
sudo ufw allow from 192.168.0.?
```

> NOTE: I replace the IP address above with the actual address for the `workstation`, e.g. 192.168.188.41.

* I check the UFW status:
    

```plaintext
sudo ufw status
```

> NOTE: UFW will, by default, block all incoming traffic, including SSH and HTTP.

> ANOTHER NOTE: I will update the UFW rules as I deploy other services to the `homelab`.

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

* On the remote `homelab` system, I install Fail2Ban:
    

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
⋮
bantime = 1d
maxretry = 3
⋮
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

The next step is to install the LXD manager which handles the containers, images, profiles, commands, and resources.

## Installing the LXD Manager.

![manager](https://images.pexels.com/photos/1117211/pexels-photo-1117211.jpeg?cs=srgb&dl=pexels-david-dibert-1117211.jpg&fm=jpg&w=640&h=427 align="left")

> NOTE: Remember, LXD is an abbreviation for LinuX Daemon.

* On the remote `homelab` system, I install the Snap package manager:
    

```bash
sudo apt install snapd
```

* I install the `LXD` container manager:
    

```plaintext
sudo snap install lxd
```

* I'll also add my account to the LXD group if needed:
    

```bash
sudo adduser yt lxd
```

> NOTE: Adding myself to the LXD group means I can skip the `sudo` requirement when issuing LXD and LXC commands.

If the time ever came, this is how I'd uninstall LXD.

## Uninstall the LXD Manager.

* On the remote `homelab` system, I uninstall the Snap package manager:
    

```javascript
sudo snap remove --purge lxd
```

The next *optional* step is to set up an empty drive (or partition) where I can store my container images.

## OPTIONAL: Preparing an Empty Drive (or Partition) for LXD Storage.

![HDD](https://images.pexels.com/photos/33278/disc-reader-reading-arm-hard-drive.jpg?cs=srgb&dl=pexels-pixabay-33278.jpg&fm=jpg&w=640&h=427 align="left")

Using an empty drive (or partition) to store my images has advantages. I can:

* Secure images with repeatable, scheduled backups (think: CRON Jobs),
    
* Rebuild the host system without losing images,
    
* Move the drive (or partition) to another system,
    
* Improve reliability, performance, or capacity, by...
    
    * Enabling the cluster option, and/or
        
    * Including more drives.
        

Using an empty drive (or partition) to store my images has definite advantages. If this was a production system running a cluster, then I'd *absolutely* store my images on M.2 drives, SSDs, HDDs, and NAS systems.

* On the remote `homelab` system, I use Gnome <mark>Disks</mark> to format an empty partition, for example, the `/dev/sda2` device pictured below:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1686610144942/b602877a-f249-4728-820c-85fedf4e5254.png align="center")

> NOTE: In this example, `/dev/sda2` is the partition device I've decided to use.

* I reboot the system:
    

```plaintext
reboot
```

* On the remote `homelab` system, I list the PC hardware, e.g. eno1 (ethernet controller), /dev/sda2 (volume partition), etc.:
    

```bash
sudo lshw -short
```

* I unmount the empty partition:
    

```plaintext
sudo umount /dev/sda2
```

* I prepare the empty partition:
    

```plaintext
sudo dd if=/dev/zero of=/dev/sda2 bs=4M count=10
```

The next step is to initialise the LXD for use.

## Initialising the LXD Manager.

![initial](https://images.pexels.com/photos/10394994/pexels-photo-10394994.jpeg?cs=srgb&dl=pexels-brett-jordan-10394994.jpg&fm=jpg&w=640&h=480 align="left")

* I initialise the LXD service and *mostly* use the default settings during setup:
    

```bash
lxd init
```

These are my settings when I initialise the LXD service:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687325623451/7a1f9122-852d-4e53-ac70-70bf00769e31.png align="center")

* For the first highlighted section above, I chose BTRFS so I can use Docker,
    
* For the second highlighted section above, I had a spare HDD partition and I wanted to experiment with this setting, and
    
* For the third highlighted section above, I want each *remote* container on my `homelab` to receive an IP address from my router. If I'm initialising an LXD on my local `workstation`, I'd choose 'a new local network bridge' so I can use SSH connections from the same computer.
    

The last step is to test the LXC commands by spinning up and tearing down a couple of containers.

## Running a Quick Test.

![test](https://images.pexels.com/photos/60022/microscope-slide-research-close-up-60022.jpeg?cs=srgb&dl=pexels-public-domain-pictures-60022.jpg&fm=jpg&w=640&h=424 align="left")

From the `homelab` system, I initialise an image called `test1`:

```bash
lxc init ubuntu:22.04 test1
```

* I launch a container called `test2`:
    

```plaintext
lxc launch ubuntu:22.04 test2
```

* I list the containers:
    

```plaintext
lxc ls
```

> NOTE: `lxc init` creates a static image, `lxc launch` creates an image then runs it as a container.

* I (try to) delete `test1` and `test2`:
    

```plaintext
lxc delete test1 test2
```

* I list the containers again only to see that `test2` still exists:
    

```plaintext
lxc ls
```

* I delete `test2` using the -f(orce) flag:
    

```plaintext
lxc delete test2 -f
```

* I list the containers one more time to see everything has been deleted:
    

```plaintext
lxc ls
```

Here are my results:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683510898323/062a5e54-1b8b-4edf-8d05-a2239461fbbb.png align="center")

Please note the following about these results:

* "Creating test1" happened when I used `init` to build the image, while...
    
* "Creating test2" and "Starting test2" happened when I used `launch` to build the container,
    
* The `ls` (list) command shows the test1 image has a STOPPED STATE while the test2 container has a RUNNING STATE, and
    
* The delete command, which worked on the STOPPED STATE image of test1, did *not* work on the test2 container, until I used the `-f` (force) flag. This flag put the container into a STOPPED STATE and then deleted test2 which, as a consequence of changing states, had become an image.
    

> NOTE: While the `test1` instance was NOT running, it was called an image. If I told it to START, then it would have become the `test1` container. The `test2` instance WAS running, so it was called a container. If I told it to STOP, then it would have become the `test2` image. Yet another example of useless trivia floating around in my brain.

## 20 Common LXC Commands.

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

## 3 More LXC Commands.

There are three more LXC commands I often use:

* `lxc init ubuntu:22.04 test-container3`
    

Both the `lxc init` command and the `lxc launch` command (number 3. above) will download the image file of the requested system, in these cases, `ubuntu:22.04`. However, the `lxc launch` command goes one step further: The image is advanced to a running state by loading it into memory, and a container is initialised.

> NOTE: A container is simply an active, running instance of an image file. An image file is like the operating system (OS) files that are stored on an HDD or SSD when a PC is powered down. A container is like a running computer where the OS, utility, and app files have been loaded into memory.

* `lxc copy test-container3 test-container3-clone`
    

The l`xc copy` command is used to create a complete clone of a container. The filesystem of the original container (`test-container3`) is copied to a new image (`test-container3-clone`), including any updates and installations. I typically create one container, install the updates, and then make copies of that container as needed. Making a copy of an updated container is fast and saves time, but only if I want to use the same system as a base for other container projects.

* `lxc exec test-container3 -- su mylogin`
    

When logging in to the container, the `su mylogin` command tells `test-container3` to <mark>s</mark>witch the <mark>u</mark>ser to the `mylogin` account. For this to work, I would initially need to log in as `root` (number 12. above) and create the `mylogin` account.

## The Results.

This post covered the setup and usage of UFW and Fail2Ban for security, preparing an empty partition for storage, installing and initializing LXD, and testing LXC commands. LXD is an excellent tool for creating and managing multiple containers on a single host, offering a clean and efficient development environment.

## In Conclusion.

![an image of plastic tiles with letters that spell conclusion](https://images.pexels.com/photos/1888005/pexels-photo-1888005.jpeg?cs=srgb&dl=pexels-ann-h-1888005.jpg&fm=jpg&w=640&h=427 align="left")

LXD is a great system for spinning up, and running, multiple LXCs on a single host. (I hate it when my computers become a cesspool of development debris and database detritus, so using disposable containers for experimental exercises is a great use case for me.) Docker is *another* container system that is *extremely* popular with developers.

Be sure to check out my next post in this series where I run a Docker service within an LXD container.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | LXD Manager | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)