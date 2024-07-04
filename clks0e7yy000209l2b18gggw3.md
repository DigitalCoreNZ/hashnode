---
title: "Installing Terraform."
datePublished: Tue Aug 01 2023 08:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clks0e7yy000209l2b18gggw3
slug: installing-terraform
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699656746997/34cd4fce-4303-4dda-a7e2-f3a90658f23b.png
tags: automation, devops, terraform, infrastructure-as-code, iac

---

## TL;DR.

I can install Terraform on my homelab by following these steps:

* Log into my homelab,
    
* Update and upgrade the homelab,
    
* Install dependencies,
    
* Import the GPG key,
    
* Add the HashiCorp repo,
    
* Update package list, and
    
* Install Terraform.
    

I can also upgrade Terraform as needed.

## An Introduction.

Terraform is an infrastructure as code (IaC) tool that helps me manage, and provision, resources in a consistent and declarative manner. It helps streamline the process of managing my infrastructure by enabling efficient collaboration, version control, and automation.

> NOTE: It is my normal practice to create a system image with Clonezilla Live before I make any significant changes to an installation.

By using Terraform, I can optimize my workflow and improve my developer experience.

> The purpose of this post is to formalise the process of installing Terraform on my homelab.

## The Big Picture.

Up until this point, I have been manually creating containers but now is the time to adopt an automated approach. I'll be using Terraform and Ansible as the basis for my Infrastructure as Code deployment.

There is some overlap between what these technologies do. Even so, each utility is slightly better at completing specific tasks.

## Preparing the Workstation.

I can install the [LXD container manager](https://solodev.app/2-of-8-lxd-on-the-homelab#heading-installing-the-lxd-manager) if needed.

## Installing Terraform.

After logging in to the homelab, I install a utility called Terraform.

* I open a terminal (CTRL + ALT + T), then update and upgrade my homelab:
    

```javascript
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the dependencies:
    

```javascript
sudo apt install -y software-properties-common gnupg2 curl
```

* I import the GPG key:
    

```javascript
curl https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/hashicorp.gpg
```

* I add the HashiCorp repo:
    

```javascript
sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

* I update the repo list:
    

```javascript
sudo apt update
```

* I install Terraform:
    

```javascript
sudo apt install terraform
```

* I verify the installation:
    

```javascript
terraform --version
```

## Upgrading Terraform.

* I update the repos:
    

```javascript
sudo apt update
```

* I upgrade Terraform:
    

```javascript
sudo apt upgrade terraform
```

## The Results.

Terraform is an Infrastructure as Code utility that improves my version control and system implementation processes. By following the steps above, I can set up Terraform on my homelab which I will use to enhance my infrastructure management abilities.

## In Conclusion.

IaC is new to me and I'm really excited to give it a go. Terraform and Ansible are the tools I'll adopt but there are other utilities too, like Puppet and Chef. I have no idea how any of these tools work but I'm ready to poke and prod these services. (I lose a metaphorical finger when I poke stuff, but that's OK. They're only virtual fingers and it doesn't hurt when I loose one.)

Until next time: Be safe, be kind, be awesome.