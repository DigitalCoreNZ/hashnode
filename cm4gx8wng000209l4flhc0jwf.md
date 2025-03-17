---
title: "Apps & Utilities for Ubuntu 24.04 LTS."
datePublished: Mon Dec 09 2024 11:00:41 GMT+0000 (Coordinated Universal Time)
cuid: cm4gx8wng000209l4flhc0jwf
slug: apps-utilities-for-ubuntu-2404-lts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733475350292/669b644e-8ef2-43ae-ac4b-ac728de72135.png
tags: ubuntu, productivity, software-development, linux, docker, opensource, spotify, blender, vs-code, innovation, tech-community, tech-tools, ubuntu-studio, davinci-resolve-studio

---

# TL;DR.

This post provides a guide to setting up a personalized Ubuntu 24.04 LTS system with essential applications and utilities. It covers software installation for productivity, development, and media tasks, including package managers, partition tools, and specialized applications like VS Code and DaVinci Resolve Studio. This guide emphasizes the importance of keeping my system updated while exploring new tools that optimize workflows, supports daily tasks, and helps to achieve long-term goals.

> **Attributions:**
> 
> ***Various ↗.***

---

# An Introduction.

Setting up a practical Ubuntu system requires a collection of apps and utilities that meet my needs. The applications and services I list below are used to adapt the Ubuntu 24.04 LTS distribution to my requirements.

> The purpose of this post is to identify some apps and utilities that I find useful.

---

# The Big Picture.

Software that is installed on my PC defines what I want to achieve with my computer. I run a dual-boot PC that allows me to boot into Ubuntu or Windows.

Ubuntu is my daily driver where I spend my time writing these blog posts, and practising my SysOps skills. It is also where I will develop my skills as a software developer and AI generalist.

I also run Windows-only programs like the Reason DAW (digital audio workstation) and the Anadigm Designer 2 computer-aided design tool.

A PC is a generic tool where the installed software defines what the user is capable of achieving.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

# Updating the System.

APT (advanced package tool) handles the installation and removal of software on Debian and Debian-based Linux distributions. The following commands are used to keep my Ubuntu system (a Debian-based Linux distro) up-to-date.

* From the terminal, I update my system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

# My Terminal Settings.

A terminal is a text window where I can type commands that are executed by my system.

* I go to Preferences &gt; Unnamed &gt; Text tab,
    
* I set the `Initial terminal size` to 72 columns and 28 rows,
    
* I set the `Custom font` to Monospace at 20pt,
    
* I set the `Allow blinking text` to Never, and
    
* I set the `Cursor blinking` to Disabled.
    

> NOTE: These settings make it easier to see the commands I use.

---

# Connecting to the QNAP NAS.

* I use a utility called [Qfinder Pro](https://www.qnap.com/en/software/qfinder-pro) that helps connect my PC to my NAS.
    
* Once access to my NAS is established, I edit the following file so the default system directories point to the equivalent NAS directories:
    

```bash
sudo nano $HOME/.config/user-dirs.dirs
```

> NOTE: The details of this process is beyond the scope of this post.

---

# Installing GNOME Tweaks.

* From the terminal, I install GNOME Tweaks:
    

```bash
sudo apt install -y gnome-tweaks
```

* I run GNOME Tweaks:
    

```bash
gnome-tweaks
```

* I right-click the icon in the Dock and select “Pin to Dash” from the popup menu.
    

---

# Installing the Package Managers.

There are numerous package managers, including APT (advanced package tool is the default package manager), Snap, and Flatpak.

> NOTE: A developer might also package their app as an AppImage.

## Installing the Snap Package Manager.

* From the terminal, I use `APT` to `install` the Snap daemon:
    

```plaintext
sudo apt install -y snapd
```

* I use `Snap` to `install` the `Snap` package manager `core`:
    

```plaintext
sudo snap install core
```

## Installing the Flatpak Package Manager.

* From the terminal, I use the `APT` to `install` the `Flatpak` package manager:
    

```plaintext
sudo apt install -y flatpak
```

* I reboot my system.
    

---

# Installing the Partition Managers.

GNOME Disks and GParted are popular partition managers. The following describes how to install these utilities, and add support for creating an exFAT file system.

## Installing GNOME Disks.

GNOME Disks is the default, graphical, partition management tool on all the GNOME-based desktop environments. The following describes how to install the GNOME Disks utility, if required.

* From the terminal, I install GNOME Disks utility (if required):
    

```bash
sudo apt -y install gnome-disk-utility
```

## Installing GParted.

GParted, or GNOME Partition Editor, is an alternative to GNOME Disks. It is a free, graphical, partition management tool. The following describes how to install the GParted utility.

* From the terminal, I install the GParted utility:
    

```bash
sudo apt -y install gparted
```

GParted can also be [installed on a USB thumb drive](https://gparted.org/liveusb.php)***↗***.

## Installing exfatprogs.

exfatprogs allows partition management tools, like GNOME Disks and GParted, to use the exFAT file system when formatting partitions. exFAT is a proprietary file system from Microsoft, was released in 2006, and is the successor to FAT32.

* From the terminal, I install the exfatprogs library:
    

```bash
sudo apt -y install exfatprogs
```

---

# Installing UNZIP.

UNZIP is a utility that is used to unpack compressed packages.

* From the terminal, I install UNZIP:
    

```bash
sudo apt install unzip
```

---

# Installing Curl.

curl is a command-line utility for transferring data to, or from, a remote server.

* From the terminal, I install Curl:
    

```bash
sudo apt install -y apt-transport-https curl
```

---

# Installing Wget.

Wget is a command-line utility for retrieving files using the HTTP or FTP protocols.

* From the terminal, I install Wget:
    

```bash
sudo apt install wget
```

---

# Installing NodeJS.

NodeJS is a server-side runtime that uses the V8 JavaScript engine.

* From the terminal, I install NodeJS:
    

```bash
sudo apt install -y nodejs
```

* I verify the NodeJS installation:
    

```bash
node -v
```

---

# Installing the NodeJS Package Managers.

NPM (NodeJS Package Manager) is a software registry, package manager, and installer for NodeJS packages.

NVM (Node Version Manager) manages NodeJS versions on my system.

PNPM (Performant Node Package Manager) is another JavaScript package manager.

NPX (Node Package Executor) is used to execute NPM packages.

## Installing NPM.

* I install NPM:
    

```bash
sudo apt install -y npm
```

* I verify the NPM installation:
    

```bash
npm -v
```

## Installing NVM.

* I download, and run, the NVM installation script:
    

```bash
wget -q -O- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

* I refresh the current terminal:
    

```bash
. ~/.bashrc
```

* I verify the NVM installation:
    

```bash
nvm -v
```

## Installing PNPM.

* I install PNPM:
    

```bash
sudo npm install -g pnpm
```

* I verify the PNPM installation:
    

```bash
pnpm -v
```

## Installing NPX.

> NOTE: [NPX](https://www.npmjs.com/package/npx) is now part of the NPM CLI.

---

# Installing Miniconda.

* Check out this post to see how [to install Miniconda](https://solodev.app/installing-miniconda).
    

---

# Installing LXD and Using LXCs.

* Check out these posts to see how [to install LXD](https://solodev.app/installing-lxd-and-using-lxcs) and [create an LXC](https://solodev.app/creating-a-local-linux-container).
    

---

# Installing Ollama.

Ollama is used to download, set up, and run large language models on a local PC.

* From the terminal, I install Ollama:
    

```bash
curl https://ollama.ai/install.sh | sh
```

* I list the LLMs downloaded by Ollama:
    

```bash
ollama list
```

* If the above command fails, I run Ollama as a background service:
    

```bash
ollama serve &
```

* If the following error displays when Ollama is *already* running as a background service:
    

```bash
Error: listen tcp 127.0.0.1:11434: bind: address already in use
```

## Updating Ollama.

* I update Ollama:
    

```bash
curl https://ollama.ai/install.sh | sh
```

## Uninstalling Ollama.

* I stop the Ollama service:
    

```bash
sudo systemctl stop ollama
```

* I disable the Ollama service:
    

```bash
sudo systemctl disable ollama
```

* I remove the Ollama service:
    

```bash
sudo rm /etc/systemd/system/ollama.service
```

* I remove the Ollama binary from my bin directory:
    

```bash
sudo rm $(which ollama)
```

* I remove the models downloaded by Ollama:
    

```bash
sudo rm -r /usr/share/ollama
```

* I delete the Ollama service user:
    

```bash
sudo userdel ollama
```

* I delete the Ollama service group:
    

```bash
sudo groupdel ollama
```

---

# Installing Pinokio.

**Pinokio** **is** a browser that lets me install, run, and programmatically control ANY application, automatically. I can run chatbots, image generators, and music AI on my PC at the click of a button.

* I visit the download page:
    

```bash
https://github.com/pinokiocomputer/pinokio/releases/tag/3.6.23
```

> NOTE: In this example, I am referencing Pinokio v3.6.23.

* At the bottom of the page, I download the Debian package for AMD64 processors.
    
* From the terminal, I install Pinokio:
    

```bash
sudo apt install -y ~/Downloads/Pinokio*
```

* I run Pinokio from the Apps drawer.
    

---

# Installing Docker.

> **Attribution:**
> 
> [https://linuxiac.com/how-to-install-docker-on-ubuntu-24-04-lts/](https://linuxiac.com/how-to-install-docker-on-ubuntu-24-04-lts/) ***↗.***

* From the terminal, I add HTTPS and the Curl utility:
    

```bash
sudo apt install -y apt-transport-https curl
```

* I import the Docker GPG repository key:
    

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I add the official Docker repository to my system:
    

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I refresh my local repo list:
    

```bash
sudo apt update
```

* I install Docker:
    

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

* I check to see if Docker is active:
    

```bash
sudo systemctl is-active docker
```

* I test the installation:
    

```bash
sudo docker run hello-world
```

## Uninstalling Docker.

> **Attributions:**
> 
> [https://learnubuntu.com/uninstall-docker/](https://learnubuntu.com/uninstall-docker/) ***↗.***

* From the terminal, I stop the running Docker containers:
    

```bash
docker stop $(docker ps -a -q)
```

* I remove the Docker containers:
    

```bash
docker rm $(docker ps -a -q)
```

* I remove the Docker images:
    

```bash
docker rmi $(docker images -a -q)
```

* I prune the custom Docker networks:
    

```bash
docker network prune
```

* I prune the Docker containers, networks, images, cache and volumes:
    

```bash
docker system prune -a
```

* I purge every Docker package:
    

```bash
sudo apt purge docker-* containerd.io --auto-remove
```

* I remove the Docker files:
    

```bash
sudo rm -rf /var/lib/docker
```

* I remove the Docker group:
    

```bash
sudo groupdel docker
```

* I remove the Docker socket:
    

```bash
sudo rm -rf /var/run/docker.sock
```

* I remove Docker Compose:
    

```bash
sudo rm -rf /usr/local/bin/docker-compose && sudo rm -rf /etc/docker && sudo rm -rf ~/.docker
```

---

# Installing Docker Desktop.

> **Attributions:**
> 
> [https://docs.docker.com/desktop/setup/install/linux/ubuntu/](https://docs.docker.com/desktop/setup/install/linux/ubuntu/) ***↗,***
> 
> [https://dev.to/chandrashekhar/docker-desktop-is-not-working-on-ubuntu-2404-lts--2kpa](https://dev.to/chandrashekhar/docker-desktop-is-not-working-on-ubuntu-2404-lts--2kpa) ***↗.***

* I download the latest version of Docker Desktop:
    

[https://docs.docker.com/desktop/release-notes/](https://docs.docker.com/desktop/release-notes/)

* From the terminal, I change to the `Downloads` directory:
    

```bash
cd ~/Downloads
```

* I install the DEB package:
    

```bash
sudo apt install -y ./docker-desktop*.deb
```

> NOTE: Ignore the error message after installation.

* I fix the permissions issue:
    

```bash
echo 'kernel.apparmor_restrict_unprivileged_userns = 0' | sudo tee /etc/sysctl.d/20-apparmor-donotrestrict.conf
```

* I reboot my system:
    

```bash
reboot
```

* After the reboot, I return to a terminal and launch Docker Desktop:
    

```bash
systemctl --user start docker-desktop
```

* From the Apps Drawer, I pin the Docker Desktop icon to the Dock.
    

## Uninstall Docker Desktop.

* From the terminal, I remove Docker Desktop from my system:
    

```bash
sudo apt remove docker-desktop
```

* I remove the configuration and data files:
    

```bash
sudo apt remove docker-desktop && sudo rm /usr/local/bin/com.docker.cli && sudo apt purge docker-desktop
```

---

# Installing Open WebUI.

* From the terminal, I use Docker to pull Open WebUI:
    

```bash
docker pull ghcr.io/open-webui/open-webui:main
```

* Now I can run Open WebUI on port 3000 from within the Docker container:
    

```bash
docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
```

---

# Updating Blender.

Blender is a 3D modelling, rendering, animation, and simulation application.

* From the terminal, I update Blender:
    

```bash
sudo apt purge -y --auto-remove blender && sudo snap install blender --classic
```

## Removing Blender.

* I use the following command to remove Blender:
    

```bash
sudo snap remove blender
```

---

# Installing VS Code.

VS Code (Visual Studio Code) **is** a free and versatile code editor that supports almost every major programming language.

* From the terminal, I install VS Code:
    

```bash
sudo snap install code --classic
```

## Removing VS Code.

I use the following command to remove VS Code:

```bash
sudo snap remove code
```

## VS Code Extensions.

I find the following VS Code extensions useful:

* Live Server,
    
* Geo Data Viewer,
    
* Code Spell Checker,
    
* JavaScript (ES6) Code Snippets,
    
* Prettier - Code formatter,
    
* Markdown All in One,
    
* rust-analyzer, and
    
* C/C++
    

These optional VS Code extensions are also handy:

* Ayu,
    
* ES Lint,
    
* Beautify,
    
* Colorize,
    
* Rainbow Tags,
    
* Auto Rename Tag,
    
* Markdown Table Prettifier,
    

---

# Installing Spotify.

Spotify is an audio streaming and media service provider.

* From the terminal, I install Spotify:
    

```bash
sudo snap install spotify
```

## Removing Spotify.

* I use the following command to remove Spotify:
    

```bash
sudo snap remove spotify
```

---

# Installing Screenkey.

Screenkey is used to display each key press on the monitor.

* From the terminal, I install Screenkey:
    

```bash
sudo apt install -y screenkey
```

---

# Installing Inkscape.

* From the terminal, I add the repo:
    

```bash
sudo add-apt-repository ppa:inkscape.dev/stable
```

* I update my system:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt -y dist-upgrade && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt -y autoremove
```

* I install Inkscape:
    

```bash
sudo apt install -y inkscape
```

---

# Installing Krita.

* From the terminal, I install Krita:
    

```bash
sudo snap install krita
```

---

# Installing the Brave Browser.

Brave is a Chromium-based web browser.

* From the terminal, I install the Brave browser:
    

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg && echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list && sudo apt update && sudo apt install -y brave-browser
```

---

# Installing Rust.

Rust is a general-purpose, memory-safe, programming language that emphasises performance, type safety, concurrency, and does not require garbage collection.

* From the terminal, I install Rust:
    

```bash
sudo apt install build-essential && curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh && source "$HOME/.cargo/env"
```

* I check to version:
    

```bash
rustup --version
```

* I open the docs:
    

```bash
rustup doc
```

## Uninstalling Rust.

* I use the following command to uninstall Rust:
    

```bash
rustup self uninstall
```

---

# Installing DaVinci Resolve Studio 19.

DaVinci Resolve is a video editing, colour grading, and sound mixing program released by Blackmagic Design. The Studio version of this product requires the purchase of a license.

* I download the latest Linux copy of DaVinci Resolve 19 Studio:
    

[https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion](https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion)

* From the terminal, I install the following packages:
    

```bash
sudo apt install -y libqt5x11extras5
```

* I go to the Downloads directory:
    

```bash
cd ~/Downloads
```

* I extract the contents of the downloaded ZIP file:
    

```bash
sudo unzip ./DaVinci_Resolve_*_Linux.zip
```

* I change the mode of the extracted RUN file to an executable:
    

```bash
sudo chmod +x ./DaVinci_Resolve_*_Linux.run
```

* I install the unzipped `run` file:
    

```bash
sudo SKIP_PACKAGE_CHECK=1 ./DaVinci_Resolve_*_Linux.run -i
```

> NOTE: This command does not check for missing libraries during the installation.

* I change to the `libs` directory:
    

```bash
cd /opt/resolve/libs
```

* I make a new directory called `disabled_libs`:
    

```bash
sudo mkdir ./disabled_libs
```

* I move the `libglib`, `libgio`, and `libgmodule` into the `disabled_libs` directory:
    

```bash
sudo mv libglib-2.0.so* libgio-2.0.so* libgmodule-2.0.so* disabled_libs/
```

> NOTE: Moving these libraries forces Resolve to use the Ubuntu libraries.

* I update my NVIDIA drivers, if required:
    

```bash
sudo apt install -y nvidia-driver-550
```

> NOTE: Resolve requires the 550 drivers or later.

* I run the application using the Desktop icon (in the App Drawer), or as a terminal session:
    

```bash
/opt/resolve/bin/resolve
```

## Fixing the Resolve Scaling Issue.

* Open a project.
    
* Go to `DaVinci Resolve` (top left) &gt; `Preferences` &gt; `User`.
    
* Set the `UI Display Scale` to `200%`.
    

---

# Installing Fusion Studio 19.

* I download the latest Linux copy of Fusion Studio 19:
    

[https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion](https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion)

* I go to the Downloads directory:
    

```bash
cd ~/Downloads
```

* I extract the contents of the downloaded ZIP file:
    

```bash
sudo unzip ./Blackmagic_Fusion_Studio_*_installer.zip
```

* I change the mode of the extracted RUN file to an executable:
    

```bash
sudo chmod +x ./Blackmagic_Fusion_Studio_*_installer.run
```

* I install the unzipped `run` file:
    

```bash
sudo SKIP_PACKAGE_CHECK=1 ./Blackmagic_Fusion_Studio_*_installer.run -i
```

* I update my NVIDIA drivers, if required:
    

```bash
sudo apt install -y nvidia-driver-550
```

> NOTE: Fusion requires the 550 drivers or later.

* I run the application using the Desktop icon (in the App Drawer), or as a terminal session:
    

```bash
/opt/BlackmagicDesign/Fusion19/Fusion
```

---

# OPTIONAL: Running a `.bashrc` PS1 Command.

* I use the Nano text editor to open the `.bashrc` file:
    

```bash
sudo nano ~/.bashrc
```

* I scroll to the bottom of the `.bashrc` file.
    
* I add the following:
    

```bash
PS1="(\$CONDA_DEFAULT_ENV) \e[0;32m\u@WorkLab01\e[0m:\e[0;34m\w\e[0m\$ "
```

* I save (CTRL + S) the changes to the `.bashrc` file, and exit (CTRL + X) the Nano text editor.
    

---

# The Results.

Setting up a personalized Ubuntu 24.04 LTS system involves selecting and installing a variety of applications and utilities that cater to my specific needs. From essential software like package managers and partition tools to specialized applications for development, media, and productivity, each component plays a crucial role in enhancing my computing experience. By carefully choosing and configuring these tools, I can create a versatile and efficient environment that supports my daily tasks and long-term goals. I keep my system updated while exploring new tools that can further optimize my workflow.

---

# In Conclusion.

I’ve improved my Ubuntu experience with these essential apps & utilities.

Over the past 10 years, I’ve discovered these must-have applications and utilities that let me tailor my system to my requirements. As a developer, a creative, and someone who loves a well-organized digital workspace, this guide includes a minimum set of tools that I find essential.

From package managers like APT, Snap, and Flatpak, to partition managers like GNOME Disks and GParted, and the media utilities that ship in Ubuntu Studio, I have a standard set of tools that meets most of my daily needs.

With tools like Blender for 3D modelling, DaVinci Resolve Studio for video editing, and VS Code for app development, I can easily achieve any outcome that comes to mind.

I can stream my favourite tunes with Spotify while compiling new software using the Rust compiler. I can even enhance my app development with tools like Docker Desktop and Miniconda.

Keeping my system updated and exploring new tools will significantly optimize my workflow and support my daily tasks as well as my long-term goals.

What are your go-to applications? Share your favourites in the comments below!

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#Ubuntu #Linux #OpenSource #Productivity #SoftwareDevelopment #TechTools #Innovation #UbuntuStudio #Blender #DaVinciResolveStudio #VSCode #Docker #Spotify #TechCommunity