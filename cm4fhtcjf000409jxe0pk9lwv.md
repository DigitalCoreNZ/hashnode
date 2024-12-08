---
title: "Security and Hardening for Ubuntu 24.04 LTS."
datePublished: Sun Dec 08 2024 11:00:54 GMT+0000 (Coordinated Universal Time)
cuid: cm4fhtcjf000409jxe0pk9lwv
slug: security-and-hardening-for-ubuntu-2404-lts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733308461870/d5e6ce25-f4e4-4aee-8ee3-8ac07141dbb0.png
tags: cyber-security, apparmor, fail2ban, ufw, techtips, linux-hardening, stay-secure, ubuntu-2404-lts, ubuntu-security, system-security, lynis

---

# TL;DR.

This post provides a comprehensive guide to securing and hardening an Ubuntu 24.04 LTS system. It covers essential steps such as updating the system, configuring unattended upgrades, setting up a firewall with UFW, installing Fail2Ban to prevent brute-force attacks, checking AppArmor status for application permissions, and using the Lynis auditing tool for vulnerability assessments. Regular updates and reviews of these configurations are emphasized to maintain system security and resilience against potential threats.

> **Attributions:**
> 
> ***None ↗.***

---

# An Introduction.

In an era where cyber threats are increasingly sophisticated, securing an Ubuntu system is more important than ever. This guide walks through the essential steps to harden my system, from updating and automating upgrades to configuring firewalls and using security tools like Fail2Ban, AppArmor, and Lynis. By following these practices, I can enhance your system's resilience against potential threats and ensure my data remains protected.

> The purpose of this post is to promote simple, cybersecurity practices.

---

# The Big Picture.

Cybersecurity is the practice of protecting systems, networks, and programs from digital attacks. These cyberattacks are usually aimed at accessing, changing, or destroying sensitive information, extorting money from users, or interrupting normal business processes. As technology evolves, so do the tactics of cybercriminals, making it crucial for individuals and organizations to implement robust security measures. This involves a combination of technology, processes, and practices designed to safeguard networks, devices, programs, and data from attack, damage, or unauthorized access. A comprehensive cybersecurity strategy includes regular updates, threat assessments, and user education to ensure resilience against potential threats.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

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

---

# Checking the Unattended Upgrades Settings.

* From the terminal, I install unattended upgrades:
    

```bash
sudo apt install -y unattended-upgrades
```

* I check if the upgrades are properly configured:
    

```bash
cat /etc/apt/apt.conf.d/20auto-upgrades
```

> NOTE: The system will automatically update the package lists and perform unattended upgrades each day as long as Update-Package-Lists and Unattended-Upgrade are both set to ‘1’.

---

# Configuring UFW.

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

> NOTE: When setting up a remote server, ensure SSH is setup on both the client and the server before enabling UFW.

* I check the UFW status:
    

```bash
sudo ufw status verbose
```

> NOTE: There are [other UFW commands](https://solodev.app/3-of-3-hardening-the-remote-container#heading-enabling-and-setting-up-ufw) that may be useful.

---

# Installing Fail2Ban.

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

* I save (CTRL + S) the configuration changes, and exit (CTRL + X) the Nano text editor.
    
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

---

# Checking the AppArmor Status.

AppArmor, a Linux kernel security module, restricts per-program application capabilities like network access, raw socket access, and the permissions to read, write, or execute files.

* From the terminal, I check the AppArmor status:
    

```bash
sudo aa-status --verbose
```

---

# Installing the Lynis Auditing Tool.

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

Securing and hardening my Ubuntu 24.04 LTS system is a crucial step in protecting my data and maintaining system integrity. By following the outlined steps, such as updating my system, configuring unattended upgrades, setting up UFW, installing Fail2Ban, checking AppArmor status, and utilizing the Lynis auditing tool, I can significantly enhance my system's security posture. Regularly reviewing and updating these configurations will help ensure that my system remains resilient against potential threats.

---

# In Conclusion.

Is my Ubuntu 24.04 LTS system as secure as it could be?

In today's digital landscape, securing my system is more crucial than ever.

Here's a quick guide to hardening my Ubuntu system:

1. **Update My System**: Regular updates are my first line of defence.
    
2. **Unattended Upgrades**: Automate my updates to ensure I’m always protected.
    
3. **Configure UFW**: Set up my firewall to control incoming and outgoing traffic.
    
4. **Install Fail2Ban**: Protect against brute-force attacks by banning suspicious IPs.
    
5. **Check AppArmor Status**: Ensure my applications have the right permissions.
    
6. **Use Lynis Auditing Tool**: Regularly audit my system for vulnerabilities.
    

By following these steps, I can significantly enhance my system's security posture.

Remember, regular reviews and updates are key to staying resilient against potential threats.

🔍 How do you ensure your systems are secure? Share your tips below!

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#UbuntuSecurity #LinuxHardening #SystemSecurity #CyberSecurity #Fail2Ban #UFW #AppArmor #Lynis #StaySecure #Ubuntu2404LTS #TechTips