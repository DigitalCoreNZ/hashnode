---
title: "Using Distrobox on Ubuntu to run DaVinci Resolve on Ubuntu (not a typo)."
datePublished: Sun Dec 03 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpp952tm000a09jn41vs8pwc
slug: using-distrobox-on-ubuntu-to-run-davinci-resolve-on-ubuntu-not-a-typo
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701950905119/0525def4-3152-419f-ba07-ec2964cd8415.png
tags: docker, images, containers, davinci-resolve, distrobox

---

## TL;DR.

Running DaVinci Resolve on a Linux distribution (distro) other than CentOS, RHEL, or Rocky Linux is a problematic venture. The following post will present a way to easily test, and possibly host, DaVinci Resolve on other Linux distros.

> **Attributions:**
> 
> [https://www.youtube.com/watch?v=wmRiZQ9IZfc](https://www.youtube.com/watch?v=wmRiZQ9IZfc)↗,
> 
> [https://www.linuxfordevices.com/tutorials/linux/install-use-distrobox](https://www.linuxfordevices.com/tutorials/linux/install-use-distrobox)↗,
> 
> [https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket](https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket)↗,
> 
> [https://github.com/intel/compute-runtime/releases](https://github.com/intel/compute-runtime/releases)↗,
> 
> [https://github.com/89luca89/distrobox](https://github.com/89luca89/distrobox)↗, and
> 
> [https://distrobox.it/](https://distrobox.it/)↗.

## An Introduction.

Distrobox lets me run any Linux distro from my Ubuntu terminal.

> The purpose of this post is to provide a process for hosting Distrobox on Ubuntu so Distrobox can run an Ubuntu container on which DaVinci Resolve will operate.

This tangled fix is a result of the limited, supported distros for DaVinci Resolve, i.e. the supported distros being CentOS, RHEL, and Rocky Linux.

## The Big Picture.

[Container technologies](https://solodev.app/the-magic-of-vms-and-containers) like [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) and [LXD/LXC](https://solodev.app/2-of-10-lxd-on-the-homelab) are very popular solutions that developers can use to "contain" their systems for portability or run isolated code that is easily disposable. In the case of DaVinci Resolve, I want to edit videos on the same system where the source files are created, i.e. Ubuntu. Distrobox is also a container technology that:

* [Runs *ON, at least*, 20 different distros](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#host-distros) (NOT including Windows or macOS), and
    
* [Can *RUN, at least*, 40 different distros](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros).
    

Unlike [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) and [LXD/LXC](https://solodev.app/2-of-10-lxd-on-the-homelab), Distrobox's default configuration allows containers to:

* Access the host file system, and
    
* Access the host hardware resources.
    

I've chosen the Ubuntu distro to differentiate this post from [its inspiration](https://www.youtube.com/watch?v=wmRiZQ9IZfc) and test the viability of installing DaVinci Resolve on my Ubuntu-based `workstation`.

## Prerequisites.

* A Linux-based distro (I use Ubuntu),
    
* [A Docker installation](https://solodev.app/installing-docker), and
    
* [A Distrobox installation](https://solodev.app/installing-distrobox).
    

## Installing Ubuntu on Distrobox.

* I list the installed containers:
    

```bash
distrobox list
```

> NOTE: This command will result in an empty list if Distrobox is newly installed.

* I create an Ubuntu distro and call it `ubuntu`:
    

```bash
distrobox create --image docker.io/library/ubuntu:22.04 --name ubuntu
```

> NOTE 1: A [full list of distros](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros) is available online.
> 
> NOTE 2: Answer \[y\]es when the installer asks to "pull the image".

* I list the installed containers again:
    

```bash
distrobox list
```

> NOTE: This time, a container called `ubuntu` is listed.

* I enter the `ubuntu` container:
    

```bash
distrobox enter ubuntu
```

> NOTE 1: Installing the basic distro packages may take up to 5 minutes.
> 
> NOTE 2: The installation will ask to setup a minimum 8-character password.
> 
> NOTE 3: I The command prompt is used to identify the distro name, e.g. `yt@ubuntu:~/Desktop$` is my prompt for the Ubuntu distro container.

## Installing the DaVinci Resolve Dependencies.

* From within the `ubuntu` container, I update the distro:
    

```bash
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt --fix-broken install && sudo apt autoremove -y
```

> <mark>WARNING === WARNING === WARNING</mark>
> 
> The DaVinci Resolve installer does NOT work with fuse3. The fuse command below will replace fuse3. After installing DaVinci Resolve, I needed to re-install my desktop (which includes fuse3) to get my desktop icons and right-click functionality to work again:
> 
> ```bash
> sudo apt install --reinstall ubuntu-desktop
> ```
> 
> <mark>YOU HAVE BEEN WARNED!!!</mark>

* I install the Fuse library:
    

```bash
sudo apt install -y fuse
```

* I install the rest of the required dependencies:
    

```bash
sudo apt install -y libapr1 libaprutil1 libglu1-mesa libnuma1 libxcb-composite0 libxcb-cursor0 libxcb-damage0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0 libxcb-util1 libxcb-xinerama0 libxcb-xinput0 libxcb-xkb1 libxkbcommon-x11-0 ocl-icd-libopencl1 libasound2 libxcb-shape0 libxtst6
```

* I install the NVIDIA device driver:
    

```bash
sudo apt install -y nvidia-driver-535
```

> NOTE 1: This device driver is proprietary and works with my GTX3060 graphics card. I must select the right driver for the GPU I have installed.
> 
> NOTE 2: Installing this device driver may take up to 5 minutes.

## Installing DaVinci Resolve.

* I download DaVinci Resolve:
    

```bash
https://www.blackmagicdesign.com/event/davinciresolvedownload
```

* From a terminal, I change to the Downloads directory:
    

```bash
cd ~/Downloads/
```

* I unzip the download file, for example:
    

```bash
unzip ./DaVinci_Resolve_18.6.3_Linux.zip
```

> NOTE: At the time of writing, 18.6.3 was the latest version.

* I change the mode of the `.run` file to an executable, for example:
    

```bash
chmod +x ./DaVinci_Resolve_18.6.3_Linux.run
```

* I install DaVinci Resolve:
    

```bash
sudo ./DaVinci_Resolve_18.6.3_Linux.run -i
```

> NOTE: Missing dependencies may be listed during the installation process. These dependencies will need to be installed before repeating the DaVinci Resolve installation.

* I run DaVinci Resolve:
    

```bash
/opt/resolve/bin/resolve
```

## DaVinci Resolve running on my Intel NUC 10.

Running DaVinci Resolve on my Intel NUC 10 presents the dreaded "Unsupported GPU Processing Mode" modal box. My solution to this error is as follows.

* I visit the GitHub repo for Intel and follow their instructions:
    

```bash
https://github.com/intel/compute-runtime/releases
```

* I add my account to the video group:
    

```bash
sudo gpasswd -a $USER video
```

* I run DaVinci Resolve:
    

```bash
/opt/resolve/bin/resolve
```

## The Results.

Openbox has advantages over Docker and LXD/LXC including:

* Direct access to the host file system,
    
* Direct access to the host hardware resources,
    
* It is easy to setup and use, and
    
* It is lightweight.
    

When it comes to installing (and running) DaVinci Resolve, each distro will require unique deployment tweaks depending on the following system components:

* Intel vs. AMD CPUs,
    
* NVIDIA vs. AMD GPUs, and
    
* Choice of Linux distro within each container.
    

Although my NUC doesn't use an NVIDIA chipset, I still had the option of using OpenCL. (The Internet exists to solve ALL my problems. Except...)

One major issue is that MP4 videos are not supported in the *free* version of DaVinci Resolve for Linux. This issue does NOT exist when using the *paid* version called DaVinci Resolve Studio (at least, that is my personal experience when running Studio on my Ubuntu system) or DaVinci Resolve for Windows. The ffmpeg utility can re-encode the audio and/or video from MP4 and there are many online resources that show this process.

Other *possible* solutions (which I haven't tried yet) is to run Rocky Linux or CentOS on Distrobox.

## In Conclusion.

Running DaVinci Resolve on Ubuntu using Distrobox on Ubuntu is a viable solution for testing this powerful video editor on unsupported distributions. By defining and following these installation and configuration steps, I can set up DaVinci Resolve in a containerized environment which allows me to evaluate if installation on my preferred Linux distribution is possible.

BTW, video editing is my *least* favourite media production activity. I suck at it. (Alright, I <s>suck</s> am not very good at a lot of *other* things, too.)

Until next time: Be safe, be kind, be awesome.