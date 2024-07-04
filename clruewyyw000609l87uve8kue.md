---
title: "Installing Git."
datePublished: Fri Jan 26 2024 09:00:07 GMT+0000 (Coordinated Universal Time)
cuid: clruewyyw000609l87uve8kue
slug: installing-git
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705186335383/057a5ad7-46ff-4419-b2c5-085c4b646f65.png
tags: repository, ubuntu, software-development, linux, github, version-control, git, source-code, repo, installation-guide, programming-tools, tech-guide, ppa

---

# TL;DR.

This post provides a comprehensive guide on how to install Git, a popular version control system. It explains Git's functionalities and the various states that files can reside in when using Git. Then the guide moves the reader through installing Git on a Debian-based Linux distribution, covering multiple install methods, including building Git from source, installing it from a PPA repo, or using a modified APT command. This post also provides a way to check the installed version of Git.

> **Attributions:**
> 
> [https://git-scm.com/](https://git-scm.com/)***↗, and***
> 
> [https://www.geeksforgeeks.org/how-to-install-configure-and-use-git-on-ubuntu/](https://www.geeksforgeeks.org/how-to-install-configure-and-use-git-on-ubuntu/)***↗.***

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705218912034/3ecd6bd0-d9d7-4a3d-8253-c2696dda891a.png align="center")

# An Introduction.

Git is a version control system. During development, Git is responsible for managing changes to the source code of computer programs, large web sites, and documents.

> The purpose of this post is to present different ways of installing Git.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705218975675/e4d5194c-5b3c-4351-a4fe-dacc9fb430b3.png align="center")

# The Big Picture.

Git views its data as a series of snapshots. When I commit or save my project's state, Git takes a "picture" of how my files look at that moment and saves a reference to that snapshot. To save space, if files haven't changed, Git doesn't store the file again but links to the previous identical file it already saved.

Most Git actions only involve local files and don't require information from other computers on my network. Git seems incredibly fast since I usually have the whole project history on my local disk.

Git checks every file and folder and generates a unique checksum before saving everything. This checksum is then used to refer to the files and folders. This means I can't change the contents of any file without Git knowing because the checksums wouldn't match. This feature is a core part of Git's design, so I won't lose any data or have corrupted files without Git noticing.

When I perform actions in Git, almost all of them just *add* data to the Git database. It's difficult to make the system do something that can't be undone, or make it erase data without leaving a way back to a previous state. Yes, I can lose or mess up uncommitted changes, but once I commit to Git, it's hard to lose any changes, especially if I often push to another repository.

Git has three main states that my files can reside in:

* `Modified` means that I have changed the content of a file(s) but have not committed it/them to my database yet.
    
* `Staged` means that I have marked `modified` files in their current state to go into my next commit snapshot.
    
* `Committed` means that the `staged` data has been safely moved into my local database.
    

If a file is in the Git directory, it is `committed`. If the file has been changed and added to the staging area, it is `staged`. If the file was changed after being checked out but hasn't been staged yet, it is `modified`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219048320/8bb62c97-9147-4934-a577-50b7091c7040.png align="center")

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219084253/9c631530-17ad-478b-afcc-0a52e2ee4a85.png align="center")

# Installing Git: The Easiest Way.

* I update my base system:
    

```plaintext
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

* I use APT to install Git:
    

```plaintext
sudo apt install git
```

* There also exists [a slightly modified APT command](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) from the official docs:
    

```plaintext
sudo apt install git-all
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219288433/7efd66dc-e65f-47d1-9e62-ae3f66e687d8.png align="center")

# Installing Git: From the PPA Repo.

* I update my base system:
    

```plaintext
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

* I install the PPA (personal package archive) repo:
    

```plaintext
add-apt-repository ppa:git-core/ppa
```

* I update my system:
    

```bash
sudo apt update
```

* I install Git:
    

```plaintext
sudo apt install git
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219254106/6968b607-abdb-4f4a-9656-6bbc0dfc83ea.png align="center")

# Installing Git: From the Source Code.

* I update my base system:
    

```plaintext
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

* I visit the GitHub repo to find the latest version number:
    

```plaintext
https://github.com/git/git/tags
```

* I install the prerequisites:
    

```plaintext
sudo apt install -y libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev build-essential
```

* I install `wget`:
    

```plaintext
sudo apt install -y wget
```

* I install `autoconf`:
    

```plaintext
sudo apt install -y autoconf
```

* I use `wget` to download the latest version of Git:
    

```plaintext
wget https://github.com/git/git/archive/refs/tags/v2.44.0.tar.gz
```

* I use `tar` to extract the archive:
    

```plaintext
tar -xvf v2.44.0.tar.gz
```

* I list the name of the extracted directory:
    

```plaintext
ls
```

* I change to the new directory:
    

```plaintext
cd ./git-2.44.0
```

* I configure the build:
    

```plaintext
make configure
```

* I set up the script:
    

```plaintext
./configure --prefix=/usr/local
```

* I compile the source code:
    

```plaintext
make all
```

* I install Git:
    

```plaintext
sudo make install
```

* I check the version of Git:
    

```plaintext
git --version
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219203147/20d4ce0a-f29f-44e3-b449-be573fb4a0d2.png align="center")

# To Be Continued...

Installing Git is the start of a more important process: [Version control](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705219309436/7f4bce1e-b535-4dee-8b53-1aa7cd230d91.png align="center")

# The Results.

Git is an essential tool for managing changes in source code during development. Its unique design, which involves taking snapshots of files and generating checksums, ensures data integrity and makes it difficult to lose or corrupt data. This guide has walked through several ways to install Git on a Debian-based Linux distribution, including building from source, using a PPA repository, and using a modified APT command. Whichever method I choose, understanding and utilizing Git is the first step towards efficient version control. Git's power lies in its ability to track and manage changes, ensuring that nothing is lost during development.

# In Conclusion.

Are you looking to install a popular version control system called Git?

Git is a powerful tool that manages changes to my source code during development. Its ability to take "snapshots" of my files and generating checksums for data integrity, makes it nearly impossible to lose or corrupt my data. If you're in software development, you know how crucial version control is to an effective workflow.

Git is designed with three main states for my files: `Modified`, `Staged`, and `Committed`. Understanding these states is the first step towards mastering Git.

Regardless of the method you choose to install Git, remember that it is more than just a tool. It's the first step towards efficient version control.

Have you used Git before? How has it transformed your development process? Share your thoughts below.

Until next time: Be safe, be kind, be awesome.

#Git GitHub #Repository #Repo #VersionControl #SoftwareDevelopment #Linux #Ubuntu #PPA #SourceCode #ProgrammingTools #TechGuide #InstallationGuide

> NOTE: All images generated by [ComfyUI](https://github.com/comfyanonymous/ComfyUI) using the [sd\_xl\_base\_1.0](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/sd_xl_base_1.0.safetensors) checkpoint.