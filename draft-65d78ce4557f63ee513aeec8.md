---
title: "12S: Building the Accounts Microservice with Docker and Node."
slug: 12s-using-docker-desktop-to-build-microservices

---

# TL;DR.

\[pending\]

> **Attributions:**
> 
> [https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗.***
> 
> [https://ubuntu.com/server/docs/containers-lxd](https://ubuntu.com/server/docs/containers-lxd)***↗,***
> 
> [https://ubuntu.com/server/docs/containers-lxc](https://ubuntu.com/server/docs/containers-lxc)***↗,***
> 
> [https://solodev.app/installing-lxd-and-using-lxcs](https://solodev.app/installing-lxd-and-using-lxcs),
> 
> [https://solodev.app/installing-docker](https://solodev.app/installing-docker),
> 
> [https://www.docker.com/](https://www.docker.com/)***↗,***
> 
> [https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)↗,
> 
> [https://docs.npmjs.com/about-npm/](https://docs.npmjs.com/about-npm/)↗,
> 
> [https://github.com/nvm-sh/nvm#intro](https://github.com/nvm-sh/nvm#intro)↗, and
> 
> [https://solodev.app/installing-node-and-npm-with-nvm](https://solodev.app/installing-node-and-npm-with-nvm).

# An Introduction.

\[pending\]

# The Big Picture.

\[pending\]

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

# Updating my Base System.

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

# What is LXD and LXC?

The LXD (LinuX Daemon) is the container manager that is used to create, and manage, LXCs (LinuX Containers). It is a background service that can automatically start LXCs when the host system boots, or stop any container from starting at all.

An LXC (LinuX Container) is an isolated, OS-level virtualization which, for efficiency, uses the Linux kernel of the host system. It is a virtual environment where system processes within the LXC can not affect other containers, or the host system, without specifically running certain commands.

[https://ubuntu.com/server/docs/containers-lxd](https://ubuntu.com/server/docs/containers-lxd)***↗,***

[https://ubuntu.com/server/docs/containers-lxc](https://ubuntu.com/server/docs/containers-lxc)***↗, and***

[https://solodev.app/installing-lxd-and-using-lxcs](https://solodev.app/installing-lxd-and-using-lxcs).

I ensure [LXD is installed](https://solodev.app/installing-lxd-and-using-lxcs) (`lxc --version`) before continuing with this post.

## Setting Up an LXC.

* I list the existing containers:
    

```plaintext
lxc ls
```

> NOTE: [LXD must be installed](https://solodev.app/installing-lxd-and-using-lxcs) for this command to succeed.

* I launch a new container called Startups:
    

```plaintext
lxc launch ubuntu:22.04 Startups
```

* I bash into the container:
    

```plaintext
lxc exec Startups -- bash
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

## Adding a User Account to the LXC.

* From within the container, I add a new user:
    

```plaintext
adduser yt
```

* I add the new user to the `sudo` group:
    

```plaintext
usermod -aG sudo yt
```

> NOTE: usermod let's me (-a)ppend the sudo (-G)roup to the yt account.

* I exit the container:
    

```plaintext
exit
```

> NOTE: I exit the `root` account to use the `yt` account.

## Setting the LXC Home Directory.

* From the (base) terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec Startups -- su yt
```

> NOTE: At the moment, the home directory is `/root`. This section will address the issue by changing the home directory to `~`.

* I use the Nano text editor to open the `.bashrc` file:
    

```plaintext
sudo nano ~/.bashrc
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `.bashrc` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
cd ~
```

## Hardening the Container.

* From within the container, I use the `Nano` text editor to open the `sshd_config` file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I copy the following, add it (CTRL + SHIFT + V) to the bottom of the `sshd_config` file, save (CTRL +S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
PasswordAuthentication no
PermitRootLogin no
Protocol 2
Port = 2424
```

* I `restart` the `SSH` service:
    

```plaintext
sudo systemctl restart ssh
```

* I reboot the container:
    

```plaintext
sudo reboot
```

> NOTE: Within the container, I can also install (or enable) [UFW](https://solodev.app/creating-a-local-linux-container#heading-optional-enabling-and-setting-up-ufw), [Fail2Ban](https://solodev.app/creating-a-local-linux-container#heading-optional-installing-and-setting-up-fail2ban), and [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container).

# What is Docker?

`Docker` is a free tool that helps me develop, ship, and run my applications in containers. Unlike LXCs (LinuX Containers that require a Linux distro to work), `Docker` containers are lightweight bundles that package my application source code, infrastructure, libraries, and dependencies into one file that can run on any PC.

[https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers](https://ubuntu.com/tutorials/how-to-run-docker-inside-lxd-containers)***↗,***

[https://solodev.app/installing-docker](https://solodev.app/installing-docker), and

[https://www.docker.com/](https://www.docker.com/)***↗.***

I ensure [Docker is installed](https://solodev.app/installing-docker) (docker -v) before continuing with this post.

## Updating the Container for Docker.

* From the (base) terminal, I create a `btrfs` storage pool called `docker`, if required.
    

```plaintext
lxc storage create docker btrfs
```

* In the `docker` pool, I create a new storage volume called `StartupsVol`:
    

```plaintext
lxc storage volume create docker StartupsVol
```

* I attach the `Startups` container to the `StartupsVol` volume:
    

```plaintext
lxc config device add Startups docker disk pool=docker source=StartupsVol path=/var/lib/docker
```

* I change the nested containers setting to true:
    

```plaintext
lxc config set Startups security.nesting=true
```

* I change the intercept system calls setting to true:
    

```plaintext
lxc config set Startups security.syscalls.intercept.mknod=true
```

* I change the emulate system calls setting to true:
    

```plaintext
lxc config set Startups security.syscalls.intercept.setxattr=true
```

* I `restart` the container:
    

```plaintext
lxc restart Startups
```

## Installing Docker.

* From the (base) terminal, I log in to the container with the `yt` account:
    

```plaintext
lxc exec Startups -- su yt
```

> NOTE: The home directory (`~`) for my account was [set in the .bashrc file](https://solodev.app/1-of-2-installing-gitlab-ce-using-docker-in-an-lxc#heading-setting-the-lxc-home-directory) earlier in this post.

* I install the following requirements:
    

```plaintext
sudo apt install -y ca-certificates curl gnupg lsb-release
```

* I make a `keyrings` directory:
    

```plaintext
mkdir -m 0755 -p /etc/apt/keyrings
```

* I add `Docker`’s official GPG key:
    

```plaintext
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I change the mode of the `docker.gpg` file:
    

```plaintext
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

* I install the `Docker` repository:
    

```plaintext
echo "deb [arch="$(dpkg --print-architecture)" \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update the repo list:
    

```plaintext
sudo apt update
```

* I install `Docker` and its requirements:
    

```plaintext
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Checking the Docker Installation.

* I check if `Docker` is active:
    

```plaintext
systemctl is-active docker
```

* I check the status of `Docker`:
    

```plaintext
service docker status
```

* I check the `Docker` version:
    

```plaintext
sudo docker version
```

* I list the information for `Docker`:
    

```plaintext
sudo docker info
```

## Setting the Docker Privileges.

* I create the `Docker` group, if required:
    

```plaintext
sudo groupadd docker
```

* I add my account to the `Docker` group:
    

```plaintext
sudo usermod -aG docker $USER
```

* I log in to the new `Docker` group (or reboot the container):
    

```plaintext
newgrp docker
```

* I verify the `Docker` installation by running this command without a `sudo` prefix:
    

```plaintext
docker run hello-world
```

> NOTE: When [Docker is properly installed](https://solodev.app/installing-docker), the screen will show 'Hello from Docker!'.

# What are Microservices?

Microservices are small, independent servers that communicate over well-defined APIs. They are usually developed, and maintained, by small teams of programmers. Each microservice is:

* Small,
    
* Autonomous,
    
* Loosely coupled,
    
* Focused on one task,
    
* Independently deployable,
    
* Aligned with a bounded context, and
    
* An abstraction at the level of the problem domain.
    

The microservice architecture enables an organization to deliver large, complex applications rapidly, frequently, reliably, and sustainably - a necessity for deploying my 12 Startups.

[https://www.ibm.com/topics/microservices](https://www.ibm.com/topics/microservices).

## Creating the Accounts Directory.

* I make, and change to, the Accounts directory:
    

```bash
mkdir ~/Accounts && cd ~/Accounts
```

## Installing SQLite3.

* I install SQLite3:
    

```bash
sudo apt install sqlite3
```

## Starting SQLite3.

* I start SQLite3:
    

```bash
sqlite3
```

## Creating a Table.

* I copy the following and paste (CTRL + SHIFT + V) it to the "sqlite&gt;" prompt:
    

```sql
CREATE TABLE IF NOT EXISTS people (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    job TEXT NOT NULL
);
```

* I display the table:
    

```sql
SELECT * FROM people;
```

> NOTE: Nothing displays because the table is empty.

## Adding Some Records.

* I add some content into the people table:
    

```sql
INSERT INTO people (name, job) VALUES ('John Doe', 'Homemaker'), ('Jane Doe', 'Lumberjack');
```

* I display the table a second time:
    

```sql
SELECT * FROM people;
```

## Formatting the Output.

* I display the SQLite3 commands:
    

```sql
.help
```

* I display the headers:
    

```sql
.header on
```

* I change the mode to column:
    

```sql
.mode column
```

* I display the timer:
    

```sql
.timer on
```

* I display the table a third time:
    

```sql
SELECT * FROM people;
```

## Deleting the Table.

* I delete the table:
    

```sql
DROP TABLE people;
```

* I display the table a forth, and final, time:
    

```sql
SELECT * FROM people;
```

> NOTE: The error message is expected because I dropped the people table.

* I quit SQLite3:
    

```sql
.quit
```

# What is Node.js, NPM, and NVM?

Node.js is a free, JavaScript (JS) server runtime. It runs JS code as single-threaded, non-blocking, asynchronous programs, which makes it very memory efficient. Node.js performs many system-level tasks, but is commonly used to run JS servers.

NPM (Node Package Manager) is the world's largest software registry. Open source developers use it to share packages with each other. Many organizations use NPM to manage private development as well. Most developers interact with NPM using the CLI (Command Line Interface), and usually ships with Node.js (which is a JavaScript server runtime).

NVM (Node Version Manager) is used to switch between versions of Node.js (which is a JavaScript server runtime). NVM works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash) and runs on Linux distros, macOS, and Windows WSL.

[https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)↗,

[https://docs.npmjs.com/about-npm/](https://docs.npmjs.com/about-npm/)↗,

[https://github.com/nvm-sh/nvm#intro](https://github.com/nvm-sh/nvm#intro)↗, and

[https://solodev.app/installing-node-and-npm-with-nvm](https://solodev.app/installing-node-and-npm-with-nvm).

After [installing Node](https://solodev.app/installing-node-and-npm-with-nvm), I can continue with this post.

## Creating a Docker Image.

* I use the Nano text editor to create the `Dockerfile` in the Accounts directory:
    

```bash
sudo nano Dockerfile
```

> NOTE: The `Dockerfile` contains the instructions to build the image that `Docker` uses to run the container.

* I copy the following, paste (CTRL + SHIFT + V) it into `Dockerfile`, save (CTRL + S) the changes, and exit (CTRL + X) Nano.
    

```dockerfile
# Download the latest version of
# Alpine Linux to use as a base image
FROM alpine:latest
# Copy the working directory content to
# the '/app' directory in the container
COPY . /app
# Set '/app' as the working
# directory in the container
WORKDIR /app
# Update the system and install SQLite3
RUN apt update && apt install -y sqlite3
# Run SQLite3
RUN sqlite3
# Save the volume (more research needed re: Docker Compose)
VOLUME /app
# Define the port on which the container listens
EXPOSE 6000
```

# The Results.

\[pending\]

# In Conclusion.

\[pending\]