---
title: "4 of 10: Installing Docker Desktop."
datePublished: Wed Jun 28 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljfffwp307fa8hnvdv9lfgxp
slug: 4-of-10-installing-docker-desktop
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703828461921/7060e096-ed1e-457a-8eb1-89dce244fe99.png
tags: docker, ssh, docker-desktop, rsa-keys, local-area-network

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | Docker Desktop | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

Setting up Docker Desktop on a local Ubuntu system, and preparing a remote Docker container, enables benefits like isolation, portability, and scalability. Utilizing technologies like Docker, Docker Desktop, and Portainer within an LXC environment provides a versatile platform for running "12 Startups" experiments.

## An Introduction.

My previous post in this 8-part mini-series covered [how I installed Docker within a remote container](https://solodev.app/3-of-8-docker-in-a-linux-container). This time, I'm going to show *how* I install a local Docker Desktop that connects to the remote Docker container.

> ***The purpose of this post is to present a process for connecting*** the Docker Desktop to a remote Docker container.

The ["12 Startups in 12 Months"](https://solodev.app/the-12-startups-in-12-months-challenge) challenge has helped me focus on my ambitions. As someone who enjoys SysOps, I'm happy to tinker away on my PC and NUC in my "office" (which is, technically, a hallway). As someone who only has 10 Months left on his "12 Months" challenge, I'd better make my dabbling count.

## The Big Picture.

When I look at what I want to achieve from a high-altitude perspective, I've noticed discrepancies between what I want to achieve and my current efforts. The reality is: I don't see Docker Desktop playing a significant part in my stack. However, this post may help others to achieve their goals.

Anyway, the first step to connecting to the Docker container is to set up an SSH (<mark>S</mark>ecure <mark>SH</mark>ell) connection.

## Creating, and Using, RSA Keys.

These steps will enable the local `workstation` to create an SSH connection to the remote Docker container. The purpose of this setup is to do away with username and password combinations and replace them with public key encryption.

### 1/4 - Creating an RSA Key Pair on the Workstation.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I start the ssh-agent:
    

```plaintext
eval "$(ssh-agent -s)"
```

* I generate an RSA key pair called "/home/brian/.ssh/docker":
    

```plaintext
ssh-keygen -b 4096
```

* I add my SSH private key to the ssh-agent:
    

```plaintext
ssh-add /home/brian/.ssh/docker
```

### 2/4 - Uploading a Public Key to the Remote Container.

* From the `workstation` terminal, I use "ssh-copy-id" to upload the locally-generated public key to the Docker container:
    

```plaintext
ssh-copy-id -i /home/brian/.ssh/docker.pub yt@192.168.?.?
```

> NOTE: I replace the "?" with the actual octet for the container.

### 3/4 - Logging In to the Remote Container.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I log in to the “yt” account of the Docker container:
    

```plaintext
ssh 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

### 4/4 - Disabling Password Authentication.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`) connected to the Docker container, I open the "sshd\_config" file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

I edit, and save, the following "sshd\_config" settings:

```plaintext
PasswordAuthentication no
PermitRootLogin no
Protocol 2
```

> NOTE: Another change I typically make is switching out the default port number of 22 for something less obvious, e.g. 4444 (which is also very obvious so don't use port 4444):
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

> NOTE: Running the `exit`, `sudo reboot`, or `sudo poweroff` commands will close the connection to the remote host.

* Finally, I test the connection to the remote container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

Now that I have an SSH connection to the remote container, the next step is to set up the Docker Desktop repository on my `workstation` system.

## Installing Docker Desktop from the Repo.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I run the updates and upgrades:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the prerequisites:
    

```plaintext
sudo apt install -y ca-certificates curl gnupg lsb-release
```

* I make a keyrings directory:
    

```plaintext
sudo mkdir -p /etc/apt/keyrings
```

* I download the Docker key to the keyrings directory:
    

```plaintext
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I download the Docker repository entry:
    

```plaintext
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update my local repo entries:
    

```plaintext
sudo apt update
```

* I install Docker:
    

```plaintext
sudo apt install docker
```

## Deleting Docker Desktop.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I use the `apt` command to remove docker-desktop:
    

```plaintext
sudo apt remove docker-desktop
```

* I recursively remove the hidden Docker Desktop directory (while leaving the Docker directory intact):
    

```plaintext
rm -r $HOME/.docker/desktop
```

* I remove the Docker CLI:
    

```plaintext
sudo rm /usr/local/bin/com.docker.cli
```

I use the apt command to purge Docker Desktop from the system:

```plaintext
sudo apt purge docker-desktop
```

## ALTERNATE INSTALL: Downloading the Docker Desktop File.

* From a browser, I download the Docker Desktop `deb` file to the Download directory:
    

```plaintext
https://www.docker.com/products/docker-desktop/
```

* For non-Gnome desktops, from the `workstation` terminal (`CTRL` + `ALT` + `T`), I install the following:
    

```plaintext
sudo apt install gnome-terminal
```

## ALTERNATE INSTALL: Installing Docker Desktop.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I change to the Download directory:
    

```plaintext
cd ~/Download
```

* I update the repo list:
    

```plaintext
sudo apt update
```

* I install Docker Desktop:
    

```plaintext
sudo apt install ./docker-desktop-<version>-<arch>.deb
```

> NOTE: I ignore the error message after `APT` completes the installation:  
> `N: Download is performed unsandboxed as root, as file '/home/user/Downloads/docker-desktop.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)`

## Post-Docker Desktop Installation.

* I launch Docker Desktop from the Applications menu, or by running the following command in a terminal (`CTRL` + `ALT` + `T`):
    

```plaintext
sudo systemctl --user start docker-desktop
```

I check the local Docker installation with these two commands:

```plaintext
docker compose version
docker --version
```

* I enable Docker Desktop to start on boot (Settings &gt; General &gt; Start Docker Desktop when you log in):
    

```plaintext
systemctl --user enable docker-desktop
```

* I stop Docker Desktop from the Docker menu (select Quit Docker Desktop) by running the following:
    

```plaintext
systemctl --user stop docker-desktop
```

> NOTE: When a new version of Docker Desktop is released, all of these steps will need to be re-run.

## Preparing the Remote Docker Container for Docker Desktop.

Thanks to the private keys I installed on my `workstation` and pushed across the LAN, I now have a password-less connection to the Docker container running on my remote `homelab`. This opens the way for exploring multiple deployment options, remote access solutions, and distant distribution practices.

### Preparing the Remote Docker Service.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I log in to the Docker container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

* I add a new group (which probably already exists):
    

```plaintext
sudo groupadd docker
```

* I add my (current, logged-in) account to the group:
    

```plaintext
sudo usermod -aG docker ${USER}
```

* I reboot the remote container:
    

```plaintext
sudo reboot
```

### Running the "hello-world" App.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I log back into the Docker container (which now recognises my account as a member of the docker group):
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

* I run the "hello-world" app without the `sudo` command, ensuring everything works:
    

```plaintext
docker run hello-world
```

* One way of fixing a "permission denied" error is to delete the hidden `.docker` directory (which will rebuild itself with the correct permissions):
    

```plaintext
sudo rm -R /home/${USER}/.docker
```

### Running the "getting-started" App.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`) connected to the Docker container, I run the "getting-started" app:
    

```plaintext
docker run -d -p 80:80 docker/getting-started
```

* I open a browser and visit the "getting-started" app that is now running within the Docker container on port 80:
    

```plaintext
http://192.168.?.?:80
```

> NOTE: I replace the "?" with the actual IP address for the container.

If the tutorial successfully loads in a browser, then it's time to install Portainer within the remote container.

### Installing Portainer in the Remote Container.

Portainer is a web-based user interface for managing Docker environments. It can be used to manage Docker containers, images, networks and volumes.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I log in to the Docker container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

* I create a Docker volume to store the Portainer configuration data:
    

```plaintext
docker volume create portainer_data
```

* I pull the Portainer image from Docker Hub:
    

```plaintext
docker pull portainer/portainer-ce
```

* I run the Portainer container with the following command:
    

```plaintext
docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

### Accessing Portainer Locally.

* I open a browser on my local `workstation` system, point it to the IP address for the remote container, and access Portainer on port 9000:
    

```plaintext
http://192.168.?.?:9000
```

> NOTE: I replace the "?" with the actual IP address for the container.

After setting up the remote Portainer account, I now need to enable the API. This API is what Docker Desktop will use to connect to the remote container.

### Enabling the Docker API.

* From the `Workstation` terminal (`CTRL` + `ALT` + `T`), I log in to the remote container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

* I use Nano to open the `docker.service` file:
    

```plaintext
sudo nano /lib/systemd/system/docker.service
```

* I comment out (#) the existing `ExecStart` line, replace it with the following, save the changes, and exit Nano:
    

```plaintext
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://192.168.?.?:2375
```

> NOTE: I replace the "?" with the actual IP address for the container.

* I reload the Docker daemon:
    

```plaintext
systemctl daemon-reload
```

* I stop Docker:
    

```plaintext
sudo systemctl stop docker.service
```

* I start Docker:
    

```plaintext
sudo systemctl start docker.service
```

* And I check the status:
    

```plaintext
service docker status
```

Once Docker successfully boots, I will connect the local Docker Desktop app to the remote Docker service running in the remote container.

### Installing the Portainer Extension in Docker Desktop.

* On the `workstation` system, I run Docker Desktop.
    
* In the left panel, I click the `⊕ Add Extensions` button.
    
* In the Browse tab I `Search` for, and install, the Portainer extension.
    
* I open the Potainer extension.
    

> NOTE: A local instance of Docker, the one associated with Docker Workbench, will be listed here.

* I click the `Environments` logo in the middle console (immediately under the `Home` logo near the top. I can expand the middle panel by clicking the right-pointing chevron (&gt;&gt;) at the top, the one that looks like a fast-forward icon.)
    
* I click the blue `+ Add environment` button.
    
* I select the `Docker Standalone` option and click the blue `Start Wizard` button at the bottom of the window.
    
* I select the `API` option, `Name` the environment "docker", specify the `Docker API URL` as "192.168.188.\[?\]:2375", and click the blue `Connect` button at the bottom of the page.
    
* The remote `docker` environment loads into the main panel, and can be closed with the `x` symbol of the new panel that has loaded into the middle console.
    
* To re-connect to my remote container, I click the Portainer extension on the left, and click the blue `Live connect` button for the `docker` environment.
    

## The Results.

This post demonstrates the process of setting up Docker Desktop on an Ubuntu system and preparing a remote Docker container for its use. By utilizing technologies like Docker, Docker Desktop, and Portainer within an LXC environment, I can achieve benefits such as isolation, portability, and scalability. As I continue building my 12 Startups challenge, these components will come together to form a cohesive tapestry, enabling me to create versatile and efficient applications.

## In Conclusion.

The advantages of building, and running, a Docker service within a container are numerous: Isolation and separation, portability and scalability, versioning and security, but most importantly, the services that run in containers are still accessible from the outside world.

I'm gradually assembling the components that I'll need to build "12 Startups". Each element in my constellation resembles an individual jigsaw puzzle piece. Docker, Docker Desktop, Portainer, and the technologies I've covered (and will cover) in other posts should eventually coalesce around the gravitational force of my code. As the pieces come together, I'll see a tapestry of coherence slowly unfold before my eyes. I'm looking forward to sharing more of my process with you, and I'm excited about, and look forward to, these pieces coming together.

Be sure to check out my next post in this series where

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | Docker Desktop | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)