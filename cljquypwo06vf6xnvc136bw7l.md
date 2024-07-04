---
title: "6 of 10: Installing MariaDB and MySQL Workbench."
datePublished: Thu Jul 06 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljquypwo06vf6xnvc136bw7l
slug: 6-of-10-installing-mariadb-and-mysql-workbench
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999425907/36c1da93-19be-4a3e-ae23-0c91527d74e7.png
tags: databases, sql, mariadb, rdbms, mysql-workbench

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | MariaDB | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

Installing the MariaDB manager in a container on a remote system, setting up MySQL Workbench on a local system, connecting them securely using SSH, OpenSSH, and RSA key pairs, and managing the databases efficiently while conducting software experiments.

## An Introduction.

The purpose of my `homelab` is to provide a space where I can conduct software experiments. By installing LXD on my `homelab`, I can utilize containers to:

* Isolate these experiments,
    
* Protect the underlying OS from contamination, and
    
* Easily delete these experiments once I have collected my results.
    

> ***The purpose of this post is to present a way of connecting MySQL Workbench to a remote installation of MariaDB.***

The following operations demonstrate how I:

* Deploy a MariaDB manager in a container,
    
* Install MySQL Workbench on my homelab, and
    
* Connect MySQL Workbench to the MariaDB manager running in a container.
    

Additionally, there are sections on setting up and using SSH, the OpenSSH server, and RSA.

## The Big Picture.

When I'm high enough, I can see everything. For instance, even with my head in the clouds (because I'm "cloud" computing), I can see the need for data storage mechanisms.

This operation is simple to understand, easy to execute, and results in a deployed relational database that I can access with a GUI (that *isn't* phpMyAdmin) across my LAN.

## **Setting Up a Container for the MariaDB Service.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684115919133/9ac63b05-c400-4f59-bb76-263491aefa7f.png align="center")

* The first step is to set up a remote container. Click the following embedded link to open a new tab, follow the instructions, and then return to this post:
    

%[https://solodev.app/1-of-3-setting-up-a-remote-container] 

* The next step is to set up a remote connection. Click the following embedded link to open a new tab, follow the instructions, and then return to this post:
    

%[https://solodev.app/2-of-3-setting-up-a-remote-connection] 

* The last step is to harden the remote container. Click the following embedded link to open a new tab, follow the instructions, and then return to this post:
    

%[https://solodev.app/3-of-3-hardening-the-remote-container] 

Now that I have a secure connection to a remote and hardened container, the next step is to install a relational database management system within the container.

## Installing MariaDB Within the Container.

* I ensure the newly-created container is up-to-date:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the MariaDB database:
    

```plaintext
sudo apt install mariadb-server
```

* I start the MariaDB service:
    

```plaintext
sudo systemctl start mariadb
```

* I enable MariaDB to automatically run when the container boots:
    

```plaintext
sudo systemctl enable mariadb
```

* With MariaDB now installed and running, it's crucial to secure the installation by running the security script provided. Execute the following command and follow the on-screen prompts:
    

```plaintext
sudo mysql_secure_installation
```

* I verify that MariaDB is functioning correctly by logging in as the root user:
    

```plaintext
sudo mysql -u root -p
```

> Enter the root password when prompted, and I should now have access to the MariaDB command prompt.

* Run the MariaDB security script:
    

```plaintext
sudo mysql_secure_installation
```

Now that I have a relational database management system installed, the next step is to install MySQL Workbench on my local `workstation` system.

## Installing MySQL Workbench on My Workstation.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684114555123/64feb628-5949-403c-ad70-627f4543e662.png align="center")

* From the `workstation` terminal (`CTRL`+`ALT`+`T`), I update and upgrade the `workstation` system:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the Snap package manager:
    

```plaintext
sudo apt install snapd
```

* I install MySQL Workbench:
    

```plaintext
sudo snap install mysql-workbench-community
```

* I allow MySQL Workbench to connect to the .ssh directory:
    

```plaintext
sudo snap connect mysql-workbench-community:ssh-keys
```

The Snap package manager will download and install MySQL Workbench.

* Once the installation is complete, I can launch MySQL Workbench by searching for it in the applications menu, or by running the following command in the terminal:
    

```plaintext
mysql-workbench
```

Once MySQL Workbench has launched, I can start using it to manage my MariaDB (and/or MySQL) databases and tables.

## Preparing the Remote MariaDB Manager.

* On the remote `homelab` system, I make sure that the MariaDB manager is running on my LAN and that I know the IP address and port number of the container:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685256728213/cbdfde30-4246-457d-af23-eeabe2f6907f.png align="center")

* I log in to mariadb container.
    
* I login to the mariadb manager:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685259323387/abd2026e-fb36-43d0-a378-7f6037239ac1.png align="center")

* I run the following query command:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685259638942/819bddad-1142-40e6-ad89-2e5337f5951c.png align="center")

## Setting Up the Local MySQL Workbench.

* On my local `workstation` system, I open MySQL Workbench and click on the + icon next to MySQL Connections, located on the Home tab of the application.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685256768730/1ae700ca-fec2-47f8-bbb5-938289565574.png align="center")

* In the “Set up a New Connection” window, I change the "Connection Method:" to "Standard TCP/IP over SSH":
    
* I enter the following details:
    
* Connection Name: The name for a new connection, for example, "MariaDB".
    
* SSH Hostname: The IP address or hostname of the MariaDB container and the SSH port number that the container is listening on.
    
* SSH Username: The username that I use to connect to the container:
    
* SSH Password: The password for "SSH Username".
    
* SSH Key File: The secret "mariadb" key file in the "/home/user/.ssh" directory.
    
* MySQL Hostname: 127.0.0.1
    
* MySQL Server Port: 3306
    
* Username: brian
    
* Password: \*\*\*\*
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685259814441/bec576ce-ccaf-431e-9ac4-9ca8e1e01a1f.png align="center")

* I click on "Test Connection" to check if the information I entered is correct. If the connection is successful, I will see a message saying "Successfully made the MySQL connection" (although I had a "Connection Warning" dialog box, something about MariaDB compatibility issues, but I clicked the "Continue Anyway" button).
    
* Once successfully tested, I click the "OK" button. The MySQL Workbench dashboard displays the MariaDB manager:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685260266099/33ede60e-ec87-49f1-9060-84b48395683e.png align="center")

* I can now use MySQL Workbench locally to connect to the remote MariaDB manager:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1685260482845/45b3fd65-31ea-46c1-b04f-673e0725d8d3.png align="center")

## The Results.

This post shows the process of deploying a MariaDB manager in a remote container, installing MySQL Workbench on a local system, and connecting the two securely using SSH, OpenSSH, and RSA key pairs. This setup allows for efficient database management while isolating software experiments within a container, ensuring the underlying operating system remains unaffected.

## In Conclusion.

I'm not very good at using a terminal on relational database management systems. Don't get me wrong: I *love* working in a terminal. It's just that I have a MAJOR disconnect when trying to picture tables and their relationships, running queries, and working with inner joins. I can't form a mental picture of the queries I write in a terminal. But thanks to GUIs like MySQL Workbench and PhpMyAdmin, I can work with RDBMS without missing a beat.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | MariaDB | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)