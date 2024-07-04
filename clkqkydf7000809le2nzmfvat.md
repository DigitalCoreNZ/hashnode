---
title: "Wake-on LAN."
datePublished: Mon Jul 31 2023 08:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clkqkydf7000809le2nzmfvat
slug: wake-on-lan
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699656728677/8bd6c88b-10ed-4e0d-89cc-c4b4b1719d70.png
tags: wakeonlan, magic-packet, wol, wake-on-lan, magic-packets

---

## TL;DR.

Wake-on LAN (WoL), where LAN stands for Local Area Network, allows me to power up a remote computer using a network command. This is possible thanks to a "Magic Packet". To enable this feature, I need to configure the BIOS/UEFI, install a few tools, and create a persistent WoL service on the remote PC.

## An Introduction.

Modern network cards support a feature called Wake-on LAN, sometimes known as WoL. There is also *some* support for WoWLAN, or Wake-on Wireless LAN.

> Wireless LAN is commonly called WiFi.

Wake-on LAN is the process of, under specific conditions, causing a PC to turn on when commanded to do so by another PC. Wake-on LAN uses a Magic Packet that the remote NIC recognises as the Wake-on command. When the Magic Packet is received, the remote NIC tells the attached PC to begin its boot process. Although generating a Wake-on Magic Packet is commonly thought of as an Ethernet LAN feature, it is also possible to execute this command over WiFi or the Internet. These options are only possible under very specific conditions, e.g. the Internet option needs a router that supports Port 7 or Port 9 UDP forwarding of the Magic Packet, as well as settings that are beyond the scope of this post.

> The purpose of this post is to present the process of setting up, and using the WoL (Wake-on LAN) and WoWLAN (Wake-on Wireless LAN) features available over Ethernet and WiFi LANs - Local Area Networks.

## The Big Picture.

Most people are lazy, but programmers are *also* motivated by automation. This combination of "using machines to do the heavy lifting" (figuratively *and* literally) while expending the *least* amount of energy is what separates your common dawdler from a consummate developer.

Computer programmers are lazy, but we also get things done. Or, more precisely, we build the automated processes that are used to get things done *on command*.

Case in point: I will deploy a service that lets me turn on a LAN-connected computer without needing to stand up, cross the room, and press a power button.

## Wired vs WiFi.

Personally, I'd prefer running CAT-6a cables to every PC. However, I've started my company in a rental flat (where a flat is called *an apartment* in other parts of the world) so there are hard limits to what I can alter in someone else's property. I run Ethernet cables where I can. Otherwise, I resort to WiFi as a (poor) substitute.

### Enabling the WoL Service on a Remote PC.

> NOTE: This procedure automatically deletes itself when the remote PC reboots.

* I enable the 'Wake-on LAN' setting in the BIOS/UEFI.
    
* I update and upgrade the remote PC:
    

```javascript
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the `ethtool` on the remote PC:
    

```javascript
sudo apt install ethtool
```

* I display the NIC name (e.g. eno1, enp6s0, etc.):
    

```javascript
ip a
```

> NOTE: I typically have two entries. The 'lo' entry is the local loopback with the 127.0.0.1 IP address. The name of the other entry is what I need, e.g. eno1.

* I check the network card settings (to determine the status of 'Supports Wake-on' and 'Wake-on') given the NIC is called `eno1`:
    

```javascript
sudo ethtool eno1
```

> NOTE: 'pumbg' means that using a Magic Packet is supported, 'g' means Wake-on is enabled, and 'd' means Wake-on is disabled.

* I enable the Wake-on LAN feature:
    

```javascript
sudo ethtool --change eno1 wol g
```

* I can also disable the Wake-on LAN feature if required:
    

```javascript
sudo ethtool --change eno1 wol d
```

### Persisting the WoL Service on a Remote PC.

> NOTE: This procedure persists the WoL settings between PC reboots.

* I check if, and where, the `ethtool` is installed:
    

```javascript
which ethtool
```

* I install the `ethtool` on the remote PC if required:
    

```javascript
sudo apt install ethtool
```

* I create a `wol.service` file:
    

```javascript
sudo touch /etc/systemd/system/wol.service
```

* I open the `wol.service` file in Nano:
    

```javascript
sudo nano /etc/systemd/system/wol.service
```

* I add the following into the `wol.service` file:
    

```javascript
[Unit]
Description=Enable Wake On Lan
 
[Service]
Type=oneshot
ExecStart = /usr/sbin/ethtool --change eno1 wol g
 
[Install]
WantedBy=basic.target
```

* I save (CTRL+S) the changes to the `wol.service` file and exit (CTRL + X) the Nano editor.
    
* I change the `wol.service` file permissions if required:
    

```javascript
sudo chmod 600 /etc/systemd/system/wol.service
```

* I restart the daemon:
    

```javascript
sudo systemctl daemon-reload
```

* I enable the `wol.service`:
    

```javascript
sudo systemctl enable wol.service
```

> NOTE: The `wol.service` will now start on boot.

* I reboot the PC:
    

```javascript
sudo reboot
```

* After the remote PC reboots, I check the network card settings to ensure the 'Supports Wake-on' and 'Wake-on' are both set to 'g':
    

```javascript
sudo ethtool eno1
```

I display the MAC address of the remote NIC (which I'll use in the next section):

```javascript
ip a
```

> NOTE: The MAC address is displayed in the 'link/ether' setting.

* I power down the system:
    

```javascript
sudo poweroff
```

### Waking a PC over Ethernet.

> NOTE: This procedure only works over ethernet connections across the same LAN.

* I update and upgrade the local PC:
    

```javascript
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* On the local PC, within the same LAN, I install `etherwake`:
    

```javascript
sudo apt install etherwake
```

* I send a WoL Magic Packet to the MAC address of the remote NIC:
    

```javascript
wakeonlan 01:23:89:ab:cd:ef
```

## The Results.

Wake-on LAN is a fantastic tool for powering on remote computers, which saves me time and minimises my efforts. By enabling WoL on a remote PC, I can control the power state of that device using an Ethernet or WiFi connection. With the right configuration, WoL and WoWLAN can be valuable assets to my LAN.

## In Conclusion.

Here's what I know: A good programmer:

* Is lazy,
    
* Automates whatever he can, and
    
* Solves any problems that happen to pop up.
    

I'm not a great programmer, but I'm SUPER-QUALIFIED for any position where laziness is a requirement.

Until next time: Be safe, be kind, be awesome.