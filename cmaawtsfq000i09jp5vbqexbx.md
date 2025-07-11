---
title: "Local System Toolkit for Ubuntu."
seoTitle: "Local System Tools for Ubuntu Management"
seoDescription: "Set up Ubuntu 24.04 LTS with essential productivity, development, and media production tools that emphasise workflow productivity"
datePublished: Mon May 05 2025 10:00:32 GMT+0000 (Coordinated Universal Time)
cuid: cmaawtsfq000i09jp5vbqexbx
slug: local-system-toolkit-for-ubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746440588224/03f98290-7290-4d41-ae55-bda8523b31bf.png
tags: ubuntu, productivity, software-development, linux, docker, spotify, blender, vs-code, innovation, open-source, tech-community, tech-tools, ubuntu-studio, davinci-resolve-studio

---

## TL;DR.

This post provides a guide to setting up a personalised Ubuntu 24.04 LTS system with essential applications and utilities. It covers software installation for productivity, development, and media tasks, including package managers, partition tools, and specialised applications like VS Code and DaVinci Resolve Studio. This guide emphasises the importance of keeping my system updated while exploring new tools that optimise workflows, supports daily tasks, and helps to achieve long-term goals.

> **Attributions:**
> 
> ***Various ↗.***

---

## An Introduction.

Setting up a practical Ubuntu system requires a collection of apps and utilities that meet my needs. The applications and services I list below are used to adapt the Ubuntu 24.04 LTS distribution to my requirements.

> The purpose of this post is to identify some apps and utilities that I find useful.

---

## The Big Picture.

Software that is installed on my PC defines what I want to achieve with my computer. I run a dual-boot PC that allows me to boot into Ubuntu or Windows.

Ubuntu is my daily driver where I spend my time writing these blog posts, and practising my SysOps skills. It is also where I will develop my skills as a software developer and AI generalist.

I also run Windows-only programs like the Reason DAW (digital audio workstation) and the Anadigm Designer 2 computer-aided design tool.

A PC is a generic tool where the installed software defines what the user is capable of achieving.

---

## Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

## Deleting My Login Password.

* From the terminal, I delete my login password:
    

```nix
sudo passwd -d <account_name>
```

> Generally speaking, and in most situations, this command is NOT recommended. Use with CAUTION.

---

## Updating the System.

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

* I go to Settings &gt; System &gt; Software Updates to update my system.
    

---

## Activating Ubuntu Pro.

Ubuntu Pro is a subscription service that extends the Long Term Support (LTS) versions of Ubuntu from 5 years to 10 years (and soon to be 12 years).

* In the Apps Drawer, I click on the blue, `Additional Drivers` icon to start the utility.
    
* In the `Additional Drivers` window, I click on the `Ubuntu Pro` tab.
    
* I click on the `Enable Ubuntu Pro` button.
    
* I can create an account, or login to an existing Ubuntu One account.
    
* The `Enable Ubuntu Pro` window generates a token.
    
* I take the token to [https://ubuntu.com/pro/attach](https://ubuntu.com/pro/attach).
    
* It takes a moment to successfully apply the subscription.
    

> NOTE: Canonical provides up to five (5) FREE tokens.

---

## My Terminal Settings.

A terminal is a text window where system commands are issued.

* I go to Preferences &gt; Unnamed &gt; Text tab,
    
* I set the `Initial terminal size` to 72 columns and 21 rows,
    
* I set the `Custom font` to Monospace at 22pt,
    
* I set the `Allow blinking text` to Never, and
    
* I set the `Cursor blinking` to Disabled.
    

> NOTE: These settings make it easier to see the commands I use.

---

## Connecting to the QNAP NAS.

QNAP is a company, and brand of NAS (network attacked storage) devices.

* I use a utility called [Qfinder Pro](https://www.qnap.com/en/software/qfinder-pro) that helps connect my PC to my NAS.
    
* Once access to my NAS is established, I edit the following file so the default system directories point to the equivalent NAS directories:
    

```bash
sudo nano $HOME/.config/user-dirs.dirs
```

> NOTE: The details of this process is beyond the scope of this post.

---

## Installing GNOME Tweaks.

GNOME Tweaks is a system utility for the GNOME desktop environment GUI.

* From the terminal, I install GNOME Tweaks:
    

```bash
sudo apt install -y gnome-tweaks
```

* I run GNOME Tweaks:
    

```bash
gnome-tweaks
```

* I right-click the icon in the Dock and select “Pin to Dash” from the pop-up menu.
    

---

## Installing the Package Managers.

Package managers are used to distribute apps and utilities.

> NOTE: A developer might also package their app as an AppImage.

### Installing the Snap Package Manager.

* From the terminal, I use `APT` to `install` the Snap daemon:
    

```plaintext
sudo apt install -y snapd
```

* I use `Snap` to `install` the `Snap` package manager `core`:
    

```plaintext
sudo snap install core
```

### Installing the Flatpak Package Manager.

* From the terminal, I refresh the terminal:
    

```bash
. ~/.bashrc
```

* I use the `APT` to `install` the `Flatpak` package manager:
    

```plaintext
sudo apt install -y flatpak
```

---

## Installing the Partition Managers.

Partition managers are system utilities for HDDs and SSDs.

### Installing GNOME Disks.

GNOME Disks is the default, graphical, partition management tool on all the GNOME-based desktop environments. The following describes how to install the GNOME Disks utility, if required.

* From the terminal, I install GNOME Disks utility (if required):
    

```bash
sudo apt -y install gnome-disk-utility
```

### Installing GParted.

GParted, or GNOME Partition Editor, is an alternative to GNOME Disks. It is a free, graphical, partition management tool. The following describes how to install the GParted utility.

* From the terminal, I install the GParted utility:
    

```bash
sudo apt -y install gparted
```

GParted can also be [installed onto a USB thumb drive](https://gparted.org/liveusb.php)***↗***.

### Installing exfatprogs.

exfatprogs allows partition management tools, like GNOME Disks and GParted, to use the exFAT file system when formatting partitions.

> NOTE: exFAT is a proprietary file system from Microsoft, was released in 2006, and is the successor to FAT32.

* From the terminal, I install the exfatprogs library:
    

```bash
sudo apt -y install exfatprogs
```

---

## Installing UNZIP.

UNZIP is a utility that is used to unpack compressed packages.

* From the terminal, I install UNZIP:
    

```bash
sudo apt install unzip
```

---

## Installing Curl.

curl is a command-line utility for transferring data to, or from, a remote server.

* From the terminal, I install Curl:
    

```bash
sudo apt install -y apt-transport-https curl
```

---

## Installing Wget.

Wget is a command-line utility for retrieving files using the HTTP or FTP protocols.

* From the terminal, I install Wget:
    

```bash
sudo apt install wget
```

---

## Installing NodeJS.

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

## Installing the NodeJS Package Managers.

Package managers are used to bundle code for distribution.

### Installing NPM.

* I install NPM:
    

```bash
sudo apt install -y npm
```

* I verify the NPM installation:
    

```bash
npm -v
```

### Installing NVM.

* I download, and run, the NVM installation script:
    

```bash
wget -q -O- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

* I refresh my terminal:
    

```bash
. ~/.bashrc
```

* I verify the NVM installation:
    

```bash
nvm -v
```

### Installing PNPM.

* I install PNPM:
    

```bash
sudo npm install -g pnpm
```

* I verify the PNPM installation:
    

```bash
pnpm -v
```

### Installing NPX.

> NOTE: [NPX](https://www.npmjs.com/package/npx) is now part of the NPM CLI.

---

## Installing Git.

Git is a version control utility.

* From the terminal, I install Git:
    

```bash
sudo apt install -y git-all
```

* I verify the installation:
    

```bash
git -v
```

---

## Installing the GitHub Utility.

GitHub CLI is a tool that extends the capabilities of Git. Developers can interact with GitHub repositories, pull requests, issues, and workflows directly from their terminal.

### Installing GitHub CLI.

* From the terminal, I install GitHub CLI:
    

```python
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
    && out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
    && cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& sudo apt update \
	&& sudo apt install gh -y
```

### Upgrading GitHub CLI.

* I upgrade GitHub CLI:
    

```python
sudo apt update && sudo apt install gh
```

### Authorising GitHub CLI.

* I authorise GitLab CLI:
    

```python
gh auth login
```

---

## Installing Miniconda.

* Check out this post to see [how to install Miniconda](https://solodev.app/installing-miniconda).
    

---

## Installing LXD and Using LXCs.

* Check out these posts to see how [to install LXD](https://solodev.app/installing-lxd-and-using-lxcs) and [create an LXC](https://solodev.app/creating-a-local-linux-container).
    

---

## Installing Docker.

Docker is a container manager for app development and distribution.

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
sudo apt update && sudo apt upgrade
```

* I install Docker:
    

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

* I check to see if Docker is active:
    

```bash
sudo systemctl is-active docker
```

* I create the Docker group:
    

```bash
sudo groupadd docker
```

* I add my account to the group:
    

```bash
sudo usermod -aG docker $USER
```

* I test the installation:
    

```bash
sudo docker run hello-world
```

### Uninstalling Docker.

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

## Installing Docker Desktop.

Docker Desktop is a GUI for Docker.

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
    

### Uninstall Docker Desktop.

* From the terminal, I remove Docker Desktop from my system:
    

```bash
sudo apt remove docker-desktop
```

* I remove the configuration and data files:
    

```bash
sudo apt remove docker-desktop && sudo rm /usr/local/bin/com.docker.cli && sudo apt purge docker-desktop
```

---

## Updating Blender.

Blender is a 3D modelling, rendering, animation, and simulation app.

* From the terminal, I update Blender:
    

```bash
sudo apt purge -y --auto-remove blender && sudo snap install blender --classic
```

### Removing Blender.

* I use the following command to remove Blender:
    

```bash
sudo snap remove blender
```

---

## Installing VS Code.

VS Code (Visual Studio Code) **is** a free, versatile code editor.

* From the terminal, I install VS Code:
    

```bash
sudo snap install code --classic
```

### Removing VS Code.

I use the following command to remove VS Code:

```bash
sudo snap remove code
```

### Printing an AsciiDoc File as a PDF.

* I install the AsciiDoc extension from Asciidoctor for VS Code.
    
* From the terminal, I install Ruby:
    

```bash
sudo apt install -y ruby-full
```

* I install the AsciiDoctor PDF Gem:
    

```bash
sudo gem install asciidoctor-pdf
```

* Within VS Code, I open the `Settings` tab and search for `asciidoc-pdf`.
    
* I set the `Asciidoc > Pdf: Engine` to `asciidoctor-pdf`.
    
* I set the `Asciidoc > Pdf: Asciidoctor Pdf Command Path` to `asciidoctor-pdf`.
    
* I open an AsciiDoc (example.ad) file.
    
* I open the Command Palette (CTRL + SHIFT + P) and search for `AsciiDoc: Export Document as PDF`.
    
* I use this feature to generate a PDF file based on my my `example.ad` file.
    

### Removing Ruby.

* I use the following command to remove Ruby:
    

```bash
sudo apt remove ruby -y
```

### Useful VS Code Extensions when using AsciiDoc.

Here is a list of other VS Code extensions I find useful when creating an `example.ad` file or generating a PDF file from the `example.ad` file:

* Code Spell Checker from Street Side Software let’s me check for spelling mistakes in my `example.ad` file, and
    
* vscode-pdf from tomoki1207 let’s me view PDF files within VS Code. This is useful when I use AsciiDoc to generate PDF files because the view automatically updates on when I export an update to the `example.ad` content.
    

---

## Installing Spotify.

Spotify is an app and streaming service.

* From the terminal, I install Spotify:
    

```bash
sudo snap install spotify
```

### Removing Spotify.

* I use the following command to remove Spotify:
    

```bash
sudo snap remove spotify
```

---

## Installing Screenkey.

Screenkey displays keystrokes on a monitor.

* From the terminal, I install Screenkey:
    

```bash
sudo apt install -y screenkey
```

---

## Installing Inkscape.

Inkscape is a vector-based image editor.

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

## Installing Krita.

Krita is a pixel-based image editor.

* From the terminal, I install Krita:
    

```bash
sudo snap install krita
```

## Installing Krita Manually.

* From a browser, I download the AppImage file from the [Krita.org](https://krita.org/en/download/) website.
    
* From the file manager, I move the Krita app to it’s own directory.
    
* I copy the Krita logo to the Krita directory:
    

> NOTE: I downloaded the Krita logo from the Internet.

* From the Krita directory, I make the AppImage executable:
    

```bash
chmod +x krita-5.2.10-x86_64.AppImage
```

* I use the Nano text editor to create a desktop entry:
    

```bash
nano ~/.local/share/applications/krita.desktop
```

* I paste (CTRL + SHIFT + V) the following into the desktop entry:
    

```bash
[Desktop Entry]
Name=Krita
Exec=/media/brian/Downloads/Ubuntu/Krita/krita-5.2.10-x86_64.AppImage
Icon=/media/brian/Downloads/Ubuntu/Krita/krita-logo.png
Type=Application
Categories=Graphics;Images
```

* I save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor.
    
* I create a symlink to start Cursor from the terminal:
    

```bash
sudo ln -s /media/brian/Downloads/Ubuntu/Krita/krita-5.2.10-x86_64.AppImage /usr/local/bin/krita
```

* I restart my system.
    
* From the terminal, I run the Cursor IDE:
    

```bash
krita
```

---

## Installing the Brave Browser.

Brave is a Chromium-based web browser.

* From the terminal, I install the Brave browser:
    

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg && echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list && sudo apt update && sudo apt install -y brave-browser
```

---

## Installing Rust.

Rust is a general-purpose, memory-safe, programming language.

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

### Uninstalling Rust.

* I use the following command to uninstall Rust:
    

```bash
rustup self uninstall
```

---

## Installing OBS Studio.

OBS Studio is a screen casting and streaming app.

* From the terminal, I install the repository:
    

```bash
sudo add-apt-repository ppa:obsproject/obs-studio
```

* I update, and upgrade, my system:
    

```bash
sudo apt update && sudo apt -y upgrade
```

* I install OBS Studio:
    

```bash
sudo apt install -y obs-studio
```

---

## Installing DaVinci Resolve Studio 19.

DaVinci Resolve is a video editing, colour grading, and sound mixing app.

> NOTE: DaVinci Resolve Studio requires a user license.

* I download the latest Linux copy of DaVinci Resolve 19 Studio:
    

[https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion](https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion)

* From the terminal, I install the following packages:
    

```bash
sudo apt install -y libqt5x11extras5 libfuse2
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

> NOTE: The `SKIP_PACKAGE_CHECK=1` command bypasses the check system that looks for missing libraries during the installation.

* I make a new directory called `disabled_libs`:
    

```bash
sudo mkdir /opt/resolve/libs/disabled_libs
```

* I move the `libglib`, `libgio`, and `libgmodule` into the `disabled_libs` directory:
    

```bash
sudo mv /opt/resolve/libs/libglib-2.0.so* /opt/resolve/libs/libgio-2.0.so* /opt/resolve/libs/libgmodule-2.0.so* /opt/resolve/libs/disabled_libs/
```

> NOTE: Moving these libraries forces Resolve to use the Ubuntu libraries.

* I update my NVIDIA drivers, if required:
    

```bash
sudo apt install -y nvidia-driver-550
```

> NOTE: Resolve requires the 550 drivers or later.

* I run the application using the Desktop icon (in the Apps Drawer), or as a terminal session:
    

```bash
/opt/resolve/bin/resolve
```

### Fixing the Resolve Scaling Issue.

* Open a project.
    
* Go to `DaVinci Resolve` (top left) &gt; `Preferences` &gt; `User`.
    
* Set the `UI Display Scale` to `200%`.
    

---

## Installing Fusion Studio 19.

Fusion Studio is a visual effects, 3D animation, and motion graphics app.

> NOTE: Fusion Studio uses the same license that activates DaVinci Resolve Studio.

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

* I run the application using the Desktop icon (in the Apps Drawer), or as a terminal session:
    

```bash
/opt/BlackmagicDesign/Fusion19/Fusion
```

---

## One Final Update.

* From the terminal, I update my system one last time:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

## The Results.

Setting up a personalised Ubuntu 24.04 LTS system involves selecting and installing a variety of applications and utilities that cater to my specific needs. From essential software like package managers and partition tools to specialised applications for development, media, and productivity, each component plays a crucial role in enhancing my computing experience. By carefully choosing and configuring these tools, I can create a versatile and efficient environment that supports my daily tasks and long-term goals. I keep my system updated while exploring new tools that can further optimise my workflow.

---

## In Conclusion.

I’ve improved my Ubuntu experience with these essential apps & utilities.

Over the past 10 years, I’ve discovered these must-have applications and utilities that let me tailor my system to my requirements. As a developer, a creative, and someone who loves a well-ordered digital workspace, this guide includes a minimum set of tools that I find essential.

From package managers like APT, Snap, and Flatpak, to partition managers like GNOME Disks and GParted, and the media utilities that ship in Ubuntu Studio, I have a standard set of tools that meets most of my daily needs.

With tools like Blender for 3D modelling, DaVinci Resolve Studio for video editing, and VS Code for app development, I can easily achieve any outcome that comes to mind.

I can stream my favourite tunes with Spotify while compiling new software using the Rust compiler. I can even enhance my app development with tools like Docker Desktop and Miniconda.

Keeping my system updated and exploring new tools will significantly optimise my workflow and support my daily tasks as well as my long-term goals.

What are your go-to applications? Share your favourites in the comments below!

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#Ubuntu #Ubuntu-Studio #Linux #Open-Source #Productivity #Software-Development #Blender #DaVinci-Resolve-Studio #VS-Code #Docker #Spotify #Innovation #Tech-Community #Tech-Tools