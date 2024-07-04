---
title: "Installing Anaconda."
datePublished: Fri Dec 08 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpwecc6n000n08l794dhfn9u
slug: installing-anaconda
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702189135857/5111b05d-2436-4bbc-885e-b47414612a5e.png
tags: python, conda, anaconda, python-packages, anaconda-environments

---

Update: Sunday 4<sup>th</sup> January 2024.

# TL;DR.

This post serves as a guide on how to install, update, and uninstall Anaconda on Ubuntu. It provides detailed instructions on managing Anaconda environments, including creating, renaming, and removing them, and changing the working directory within an environment. It also explains how to test Python scripts within these environments. Anaconda, likened to Docker or Distrobox but specifically designed for Python, is presented as an essential tool for managing and deploying Python applications, environments, and packages.

> NOTE: [Businesses may need a license](https://www.anaconda.com/pricing/organizations/) (which includes me when I bootstrap my technology startup and begin generating a turnover.)

> Attributions:
> 
> [https://www.anaconda.com/](https://www.anaconda.com/). ***↗***

# An Introduction.

This post is a guide on installing Anaconda on Ubuntu, which is a tool for managing and deploying Python applications, environments, and packages.

> The purpose of this post is to introduce the Anaconda package manager, `conda`.

# The Big Picture.

This post provides step-by-step instructions on how to install, update, and uninstall Anaconda. It also covers how to manage Anaconda environments, including creating, renaming, and removing them, as well as changing the working directory within an environment. I want to emphasize the utility of Anaconda in Python development, likening it to Docker or Distrobox but specifically designed for Python.

Programs like [LXD](https://solodev.app/2-of-10-lxd-on-the-homelab), [Docker](https://solodev.app/installing-docker), or [Distrobox](https://solodev.app/installing-distrobox), download system images and run those images as containers. Anaconda is similar, but downloads a specific Python version (if defined) and specific packages (that are used within the environment.)

Anaconda includes a package manager called `conda`. Below is a description of how to install Anaconda yet I'm only interested in using the package manager. This is why I install [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/) instead, which is a free installer of *only* the `conda` package manager.

# **Prerequisites.**

* A Linux-based distro (I use Ubuntu).
    

# Installing Anaconda on Ubuntu.

* I update my system:
    

```python
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I install the following requirements:
    

```bash
sudo apt install -y libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6
```

* I download the installer:
    

```bash
curl -O https://repo.anaconda.com/archive/Anaconda3-2023.09-0-Linux-x86_64.sh
```

* I run the installer:
    

```bash
bash ./Anaconda3-2023.09-0-Linux-x86_64.sh
```

* I use the down arrow key to scroll through to the end of the license.
    
* I type 'yes' to accept the terms of the license.
    
* I use the ENTER key to accept the default installation path.
    

> NOTE: The installation may take a few minutes.

* When installed, the following message is shown:
    

```bash
Do you wish to update your shell profile to automatically initialize conda?
This will activate conda on startup and change the command prompt when activated.
If you'd prefer that conda's base environment not be activated on startup,
   run the following command when conda is activated:

conda config --set auto_activate_base false

You can undo this by running `conda init --reverse $SHELL`? [yes|no]
```

> NOTE: The default option is 'no' but I type 'yes' at the `>>>` prompt.

* The final message displays as shown:
    

```bash
no change     /home/brian/anaconda3/condabin/conda
no change     /home/brian/anaconda3/bin/conda
no change     /home/brian/anaconda3/bin/conda-env
no change     /home/brian/anaconda3/bin/activate
no change     /home/brian/anaconda3/bin/deactivate
no change     /home/brian/anaconda3/etc/profile.d/conda.sh
no change     /home/brian/anaconda3/etc/fish/conf.d/conda.fish
no change     /home/brian/anaconda3/shell/condabin/Conda.psm1
no change     /home/brian/anaconda3/shell/condabin/conda-hook.ps1
no change     /home/brian/anaconda3/lib/python3.11/site-packages/xontrib/conda.xsh
no change     /home/brian/anaconda3/etc/profile.d/conda.csh
modified      /home/brian/.bashrc

==> For changes to take effect, close and re-open your current shell. <==

Thank you for installing Anaconda3!
```

* I restart the terminal.
    

> NOTE: The prompt now indicates that I am in the (base) environment.

* I initialize `conda`, if needed:
    

```bash
source ~/anaconda3/bin/activate
```

* Here is another way to initialize `conda`:
    

```python
conda init
```

* I run this command to tell the base environment to activate by default:
    

```bash
conda config --set auto_activate_base True
```

* I run this command to tell the base environment *not* to activate by default:
    

```bash
conda config --set auto_activate_base False
```

# Updating Anaconda.

* I update Anaconda:
    

```python
conda update -n base -c defaults conda
```

# Uninstalling Anaconda.

* I activate the Anaconda (base) environment:
    

```bash
conda activate
```

* I remove any conda initialization scripts:
    

```bash
conda init --reverse --all
```

* I remove Anaconda from the $HOME directory:
    

```bash
rm -rf ~/anaconda3
```

* Alternatively, I remove Anaconda from the /opt directory in the $HOME directory:
    

```bash
rm -rf ~/opt/anaconda3
```

# Anaconda Environment Commands.

* I display a list of Anaconda commands:
    

```bash
conda
```

* I display a list of Anaconda environment commands:
    

```python
conda env
```

## Creating a New Environment.

* I create a new environment called `new-env` which uses Python 3.11 and includes a package called pandas:
    

```bash
conda create -n new-env python=3.11 pandas -y
```

> NOTE: The property after the `-n` or the `--name` flag is the name for the environment.

## Listing the Existing Environments.

* I list the existing environments:
    

```bash
conda env list
```

## Renaming an Environment.

* I rename the `new-env` environment to `better-env`:
    

```bash
conda rename -n new-env better-env
```

* I list the existing environments again:
    

```bash
conda env list
```

## Activating an Environment.

* I activate the `better-env` environment:
    

```bash
conda activate better-env
```

> NOTE: The environment will change from (base) to (better-env).

## Changing the `better-env` Home Directory.

> NOTE: I will define the home directory with settings in the environment directory.

* I create the `better-dir` home directory:
    

```bash
mkdir ~/better-dir
```

* I make new directories within the (better-env) environment:
    

```bash
mkdir -p ~/anaconda3/envs/better-env/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/anaconda3/envs/better-env/etc/conda/activate.d/set_working_directory.sh
```

* I add the following, save the changes (CTRL + S), and exit (CTRL + X) Nano:
    

```bash
cd ~/better-dir
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (better-env) environment:
    

```bash
conda activate better-env
```

> NOTE: I should now, by default, be in the `~/better-dir` home directory.

## Testing Python.

* I use Nano to create a module called `hello.py`:
    

```bash
sudo nano hello.py
```

* I add the following, save the changes, and exit Nano:
    

```python
print("Hello, World!")
```

* I run the hello.py module:
    

```bash
python3 hello.py
```

## Deleting an Environment.

* I return to the (base) environment.
    

```bash
conda activate
```

* I remove the `better-env` environment:
    

```bash
conda env remove -n better-env
```

# The Results.

With the installation of Anaconda, I am now equipped with a powerful tool for managing and deploying Python applications, environments, and packages. I can run multiple environments where they each have their own packages and run specific versions of Python. The `conda` command provides a lot of flexibility to Python developers. The `conda` command serves as a versatile tool for Python developers, providing me with a wide range of functionalities.

# **In Conclusion.**

I need Anaconda to elevate the development of my Python projects. It is a powerful tool for managing and deploying Python applications, environments, and packages. Think of it like Docker or Distrobox, but specifically for Python. I can run multiple environments, each equipped with their own packages and specific Python versions.

The best part? I have full control over the environments with the `conda` command, providing a lot of flexibility for Python development. Getting started with Anaconda is a breeze, especially because I'm on a Linux-based distro called Ubuntu. I update my system, install the necessary requirements, and download and run the installer. And voila! I'm ready to go! Updating, uninstalling, and managing my Anaconda environments is just as simple. Creating, renaming, and removing environments is a piece of cake. And I can even test my Python scripts and change my working directory right within my environment. Anaconda offers a versatile set of tools that can significantly boost my Python development process.

Share your thoughts and experiences with Python and Anaconda in the comments below. How has Anaconda made your Python development more efficient?

#Python #Anaconda #Programming #DataScience #Coding

Until next time: Be safe, be kind, be awesome.