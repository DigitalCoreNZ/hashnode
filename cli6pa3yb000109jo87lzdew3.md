---
title: "3/3: Hardening the Remote Container."
datePublished: Sun May 21 2023 20:29:11 GMT+0000 (Coordinated Universal Time)
cuid: cli6pa3yb000109jo87lzdew3
slug: 3-of-3-hardening-the-remote-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701641403448/f8e60f85-253d-45cb-a581-8b02c072cf56.png
tags: snippets, fail2ban, hardening, iptables, ufw

---

Firewalls and intrusion prevention servers are used to defend my systems from attacks. The following tools, and others like [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container), are foundational to protecting my systems from the barrage of targeted, brute-force, ddos aggression.

> NOTE: It is best practice to also use other layers of protection like [Cloudflare](https://one.dash.cloudflare.com/).

## Prerequisites.

* A Linux-based distro (I use Ubuntu), and
    
* [An LXD installation](https://solodev.app/2-of-10-lxd-on-the-homelab), if required.
    

## Enabling, and Setting Up, UFW.

![firewall](https://images.pexels.com/photos/241028/pexels-photo-241028.jpeg?cs=srgb&dl=pexels-pew-nguyen-241028.jpg&fm=jpg&w=640&h=427 align="left")

Yes, the Uncomplicated FireWall was [installed on the `homelab` system](https://solodev.app/2-of-8-lxd-on-the-homelab#heading-enabling-and-setting-up-ufw). This time, I am installing the "hardening" tools within this container.

* From the `homelab` terminal (`CTRL` + `ALT` + `T`) connected to the container, I check the UFW status:
    

```plaintext
sudo ufw status
```

* I enable the UFW:
    

```bash
sudo ufw enable
```

* I install a UFW rule:
    

```plaintext
sudo ufw allow from 192.168.?.?
```

> NOTE: I use `ip a` in my workstation terminal to find my IP address. ***I replace the IP address above with the actual address for the*** `workstation`***, e.g. 192.168.188.41.***

* I check the status of the UFW and list the rules by number:
    

```plaintext
sudo ufw status numbered
```

> NOTE 1: UFW will, by default, block all incoming traffic, including SSH and HTTP.

> NOTE 2: I will update the UFW rules as I deploy other services to the container.

* I delete a UFW rule by number if needed:
    

```plaintext
sudo ufw delete 1
```

* I disable UFW if needed:
    

```plaintext
sudo ufw disable
```

Now that the UFW is setup, let's install another tool for hardening a system: Fail2Ban.

> **Attribution:**  
> [digitalocean.com](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

## Installing, and Setting Up, Fail2Ban.

![stop](https://images.pexels.com/photos/9166266/pexels-photo-9166266.jpeg?cs=srgb&dl=pexels-jan-van-der-wolf-9166266.jpg&fm=jpg&w=640&h=427 align="left")

Fail2Ban protects Linux systems against many security threats, such as dictionary, DoS, DDoS, and brute-force attacks.

* From the `homelab` terminal (`CTRL` + `ALT` + `T`) connected to the container, I install Fail2Ban:
    

```bash
sudo apt install fail2ban -y
```

* I copy the `jail.conf` file as `jail.local`:
    

```plaintext
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

* I open the `jail.local` file in Nano:
    

```plaintext
sudo nano /etc/fail2ban/jail.local
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
    

```javascript
sudo systemctl status fail2ban
```

* I enable Fail2Ban to autostart on boot:
    

```plaintext
sudo systemctl enable fail2ban
```

Now that I have hardened the container, it is time to return to the original post.

And remember: Be safe, be kind, be awesome.