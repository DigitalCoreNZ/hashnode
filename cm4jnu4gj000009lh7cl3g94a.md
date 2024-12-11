---
title: "SSH Setup for Ubuntu 24.04 LTS."
datePublished: Wed Dec 11 2024 09:00:33 GMT+0000 (Coordinated Universal Time)
cuid: cm4jnu4gj000009lh7cl3g94a
slug: ssh-setup-for-ubuntu-2404-lts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733637189811/b3195f86-04fc-4c22-82a3-3c02d9b71844.png
tags: ssh, remote-work, cyber-security, ssh-keygen, remote-server, passwordless-authentication, server-management, tech-guide, ubuntu-2404, linux-setup, tech-tips, secure-connection

---

# TL;DR.

SSH Setup for Ubuntu 24.04 LTS involves installing and configuring OpenSSH Server on the remote server, generating an RSA key pair on the local system, and uploading the local, public key to the remote system for secure, password-less authentication.

> **Attributions:**
> 
> [https://linuxconfig.org/quick-guide-to-enabling-ssh-on-ubuntu-24-04](https://linuxconfig.org/quick-guide-to-enabling-ssh-on-ubuntu-24-04) ***↗.***

---

# An Introduction.

Setting up SSH on Ubuntu 24.04 is a crucial task for anyone looking to manage remote servers securely and efficiently. SSH, or Secure Shell, provides a secure channel over an unsecured network, allowing remote command executions, remote server management, and file transfers. These steps will configure SSH on both my local system and remote server, ensuring a seamless and secure connection. This post establishes a robust SSH setup, enabling password-less authentication and enhancing my overall workflow.

> The purpose of this post is to describe security between systems and servers.

---

# The Big Picture.

SSH is widely used in app development for securely accessing and managing remote servers, deploying applications, and transferring files. It allows developers to execute commands on remote machines, manage version control systems, and automate deployment processes, ensuring a secure and efficient workflow.

---

# Prerequisites.

* Two Debian-based Linux distros (I use Ubuntu), either virtual or actual.
    

---

# Updating my Base System.

* From the (base) terminal, I update my (base) system:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

> NOTE: The Ollama LLM manager is already installed on my (base) system.

---

# What is SSH?

The Secure Shell (SSH) protocol is a way to safely send commands to a computer over an unsecured network. SSH uses special codes to check and protect connections between devices. It also allows for tunnelling, or port forwarding, which lets data packets go through networks they couldn't before. SSH is often used to control servers from a distance, manage infrastructure, and transfer files. It lets administrators manage servers and devices remotely. Older methods like Telnet sent commands that anyone could see. But SSH uses a secure connection, which is why it's called Secure Shell.

[https://www.cloudflare.com/learning/access-management/what-is-ssh/](https://www.cloudflare.com/learning/access-management/what-is-ssh/)***↗.***

## Installing SSH on the Client.

SSH is used to safely send commands to a computer over an unsecured network.

* From the terminal, I install SSH:
    

```bash
sudo apt install -y ssh
```

* I make a copy of the existing SSH settings:
    

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```

* I open the SSH configuration file in the Nano text editor:
    

```bash
sudo nano /etc/ssh/sshd_config
```

* I change the following directives:
    
    * LoginGraceTime 20
        
    * PermitRootLogin no
        
    * MaxAuthTries 3
        
    * ⋮
        
    * PasswordAuthentication no
        
* I save the changes (CTRL + S) and exit (CTRL + X) the Nano text editor.
    
* I create a privilege separation directory:
    

```bash
sudo mkdir /run/sshd
```

* I test the SSH configuration for syntax errors:
    

```bash
sudo sshd -t
```

> NOTE: If I do not get any output after running this command, then the changes I made are using valid syntax.

* I reload the daemon:
    

```bash
sudo systemctl daemon-reload
```

* I restart the SSH socket:
    

```bash
sudo systemctl restart ssh.socket
```

* I check the status of the SSH socket:
    

```bash
sudo systemctl status ssh.socket
```

> NOTE: SSH is running when the Active status is active (listening).

* I exit the status command (CTRL + C).
    

## Creating an RSA Key Pair on the Client.

* From the terminal, I start the ssh-agent:
    

```bash
eval "$(ssh-agent -s)"
```

* I generate a pair of RSA (Rivest-Shami-Adleman) keys and call the `/home/brian/.ssh/key-name` (where I replace "key-name" with the name of the remote server):
    

```bash
ssh-keygen -b 4096
```

> NOTE: It is my convention to name the RSA keys after the remote server on which they will be applied.

* I add the SSH private key to my local system:
    

```bash
ssh-add /home/brian/.ssh/key-name
```

---

## Uploading the Client Public Key to the Server.

* From the `local` terminal (`CTRL` + `ALT` + `T`), I use the `ssh-copy-id` command to upload the locally-generated public key to the remote server:
    

```bash
ssh-copy-id -i /home/brian/.ssh/key-name.pub account-name@192.168.?.?
```

> NOTE: I replace the "?" with the actual IP address of the remote server.

## Using RSA to Connect to the Server.

* From the `local` terminal (`CTRL` + `ALT` + `T`), I connect to the remote server:
    

```bash
ssh 'user-account@192.168.?.?'
```

## Preparing the Server.

* From the `remote` terminal (`CTRL` + `ALT` + `T`), I update the remote server:
    

```bash
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

* I install OpenSSH Server:
    

```bash
sudo apt install -y ssh
```

* I set the SSH Server to start on boot:
    

```bash
sudo systemctl enable ssh
```

* I check the status of the SSH Server:
    

```bash
sudo systemctl status ssh
```

* I start the SSH Server if it is not running:
    

```bash
sudo systemctl start ssh
```

* I add an entry to the UFW (Uncomplicated Firewall):
    

```bash
sudo ufw allow ssh
```

* I set the UFW to start on boot:
    

```bash
sudo ufw enable
```

---

# Basic Server Security.

Security is an attitude, not a process.

## Checking the Unattended Upgrades Settings.

* From the terminal, I install unattended upgrades:
    

```bash
sudo apt install -y unattended-upgrades
```

* I check if the upgrades are properly configured:
    

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

> NOTE: The system will automatically update the package lists and perform unattended upgrades each day as long as Update-Package-Lists and Unattended-Upgrade are both set to ‘1’.

## Configuring UFW.

* From the terminal, I check the UFW status:
    

```bash
sudo ufw status verbose
```

* I allow SSH:
    

```bash
sudo ufw allow ssh
```

* I allow port 80:
    

```bash
sudo ufw allow 80/tcp
```

* I allow port 443:
    

```bash
sudo ufw allow 443/tcp
```

* I enable UFW:
    

```bash
sudo ufw enable
```

> NOTE: When setting up a remote server, I ensure SSH is setup on both the client and the server before enabling UFW.

* I check the UFW status:
    

```bash
sudo ufw status verbose
```

> NOTE: There are [other UFW commands](https://solodev.app/3-of-3-hardening-the-remote-container#heading-enabling-and-setting-up-ufw) that may be useful.

## Installing Fail2Ban.

* From the terminal, I install Fail2Ban:
    

```bash
sudo apt install -y fail2ban
```

* I copy the `jail.conf` file as `jail.local`:
    

```bash
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

* I open the `jail.local` file in the Nano text editor:
    

```bash
sudo nano /etc/fail2ban/jail.local
```

* I change a few (SSH-centric) settings in the `jail.local` file:
    

```bash
[DEFAULT]
⋮
bantime = 1d
maxretry = 3
⋮
[sshd]
enabled = true
port = ssh,22
```

* I save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor.
    
* I restart Fail2Ban:
    

```bash
sudo systemctl restart fail2ban
```

* I check the status of Fail2Ban:
    

```bash
sudo systemctl status fail2ban
```

* I enable Fail2Ban to autostart on boot:
    

```bash
sudo systemctl enable fail2ban
```

## Checking the AppArmor Status.

AppArmor, a Linux kernel security module, restricts per-program application capabilities like network access, raw socket access, and the permissions to read, write, or execute files.

* From the terminal, I check the AppArmor status:
    

```bash
sudo aa-status --verbose
```

## Installing the Lynis Auditing Tool.

Lynis is a flexible security auditing tool for systems running Linux, FreeBSD, macOS, OpenBSD, Solaris, and other Unix-like operating systems, helping administrators and security professionals scan and strengthen system security.

* From the terminal, I install Lynis:
    

```bash
sudo apt install -y lynis
```

* I check the installation:
    

```bash
lynis -V
```

* I run a basic scan:
    

```bash
sudo lynis audit system --quick
```

> NOTE: The log file, which is purged every scan, is `/var/log/lynis.log` and the report file is `/var/log/lynis-report.dat`.

* I check if Lynis is up-to-date:
    

```bash
lynis update check
```

> **Attribution:**
> 
> [https://cisofy.com/lynis/](https://cisofy.com/lynis/) ***↗.***

---

# The Results.

Setting up SSH on Ubuntu 24.04 LTS is an essential process for ensuring secure and efficient remote server management. By following the steps outlined, I can establish a robust SSH configuration that enhances my workflow with password-less authentication. This setup not only secures my connections but also streamlines my ability to manage and deploy applications remotely. I keep my systems updated and maintain security best practices to protect my infrastructure.

---

# In Conclusion.

Discover how I set up SSH on Ubuntu 24.04 LTS for secure, password-less authentication!

Setting up SSH is crucial for anyone managing remote servers. It provides a secure channel over unsecured networks, allowing for remote command executions, server management, and file transfers.

Here's a quick overview of the process:

1. **Update My System**: Ensure my base system is up-to-date for optimal performance.
    
2. **Generate RSA Key Pair**: Create a secure key pair on my local system to facilitate password-less authentication.
    
3. **Upload Public Key**: Use `ssh-copy-id` to transfer my public key to the remote system.
    
4. **Install OpenSSH Server**: On the remote system, install and configure OpenSSH Server for secure connections.
    
5. **Configure Firewall**: Set up UFW to allow SSH connections and ensure it starts on boot.
    

By following these steps, I can establish a robust SSH setup that enhances my workflow and secures my connections. I keep my systems updated and adhere to security best practices.

How do you ensure secure remote server management in your workflow? Share your tips below!

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#Ubuntu-2404 #SSH #SSH-Keygen #ServerManagement #RemoteServer #RemoteWork #CyberSecurity #SecureConnection #PasswordlessAuthentication #LinuxSetup #TechTips #TechGuide