---
title: "2/3: Setting Up a Remote Connection."
datePublished: Sat May 20 2023 20:29:39 GMT+0000 (Coordinated Universal Time)
cuid: cli76kh9u000109mgftl0ebbz
slug: 2-of-3-setting-up-a-remote-connection
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701641379832/a1340c0d-1fa6-41bc-b929-8cc3f8632e52.png
tags: public-key, private-key, sshdconfig, rsa-keys, remote-connection

---

Containers are used to emulate operating systems and, unlike virtual machines, are lightweight because they can use resources from the host system and run processes that *don't* affect the host or other containers.

## Prerequisites.

* A Linux-based distro (I use Ubuntu), and
    
* [An LXD installation](https://solodev.app/2-of-10-lxd-on-the-homelab), if required.
    

## Creating, and Using, RSA Keys.

These steps will enable SSH connections to the remote container, across the LAN, without a username/password.

## Creating an RSA Key Pair on the Local Workstation.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I start the ssh-agent:
    

```plaintext
eval "$(ssh-agent -s)"
```

* I generate a pair of RSA keys called "/home/brian/.ssh/key-name" (where I replace "key-name" with the name of the remote container):
    

```plaintext
ssh-keygen -b 4096
```

> NOTE: It is my convention to name RSA keys after the container or system on which they will be used.

* I add the SSH key to my workstation account (where I replace "key-name" with the *actual* name of the ssh key):
    

```plaintext
ssh-add /home/brian/.ssh/key-name
```

## Uploading a Public Key to the Remote Container.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I use "ssh-copy-id" to upload the locally-generated public key to the remote container (where I replace "container-name" with the *actual* name of the container):
    

```plaintext
ssh-copy-id -i /home/brian/.ssh/container-name.pub yt@192.168.?.?
```

> NOTE: I replace the "?" with the actual IP address for the container.

## Logging In to the Remote Container.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`), I login to the “brian” account of the remote container:
    

```plaintext
ssh 'yt@192.168.?.?'
```

> NOTE: I replace the "?" with the actual IP address for the container.

## 'Hardening' the Container.

In the previous lab, I purposely ['softened' this container](https://solodev.app/1-of-3-setting-up-a-remote-container#heading-softening-the-container). It's not an ideal state, so this section deals with 'hardening up' the container again.

* From the `workstation` terminal (`CTRL` + `ALT` + `T`) connected to the container, I open the "sshd\_config" file:
    

```plaintext
sudo nano /etc/ssh/sshd_config
```

* I add, and save, the following to the bottom of the "sshd\_config" page:
    

```plaintext
PasswordAuthentication no
PermitRootLogin no
Protocol 2
```

> NOTE: Another change I typically make is switching out the default port number of 22 for something less obvious, e.g. 4444 (which is also very obvious so don't use port 4444):
> 
> ```plaintext
> Port 4444
> ```

* I restart the "ssh" service:
    

```plaintext
sudo systemctl restart ssh.service
```

* I reboot the remote container:
    

```plaintext
sudo reboot
```

> NOTE: Running the `exit`, `sudo reboot`, or `sudo poweroff` commands will close the connection to the remote `homelab` host.

* Finally, I test the connection to the remote container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> NOTE: I replace the -p(ort) number with the actual port defined in the "sshd\_config" file, and replace the "?" with the IP address for the container.

Now that I have a local connection to the remote container, the last step is to [harden the remote container](https://solodev.app/3-of-3-hardening-the-remote-container).

And remember: Be safe, be kind, be awesome.