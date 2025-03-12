---
title: "Installing Miniconda."
datePublished: Mon Feb 26 2024 09:00:35 GMT+0000 (Coordinated Universal Time)
cuid: clt2pkz7w000n0al8hdxw77ur
slug: installing-miniconda
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708815628250/2c346f7c-d16f-4915-b40c-ddb25d2a8087.png
tags: ubuntu, python, data-science, coding, programming-ciovqvfcb008mb253jrczo9ye, python-development, miniconda, anaconda, miniconda-guide, environment-management, python-applications

---

Update: Thursday 2<sup>nd</sup> May 2024.  
Update: Wednesday 19<sup>th</sup> June 2024.

---

# TL;DR.

This post provides a comprehensive guide on how to install, use, and uninstall Miniconda, a compact version of Anaconda, on a Debian-based Linux distro. It explains the process of creating, renaming, and deleting environments in Miniconda, as well as how to test Python scripts. I also offer a brief introduction to Python and its advantages for application development.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗.***

.

> NOTE: Installing this utility will establish my Linux distribution as the (base) environment.

---

# An Introduction.

This post is a guide to installing Miniconda on Ubuntu. It is a tool for managing and deploying Python applications, environments, and packages.

> The purpose of this post is to introduce the Miniconda package manager, `conda`.

---

# The Big Picture.

This post provides step-by-step instructions on how to install, update, and uninstall Miniconda. It also covers how to manage Miniconda environments, including creating, renaming, and removing them, as well as changing the working directory within an environment. I want to emphasize the utility of Miniconda in Python development, likening it to Docker or Distrobox but specifically designed for Python.

Programs like [LXD](https://solodev.app/installing-lxd-and-using-lxcs), [Docker](https://solodev.app/installing-docker), or [Distrobox](https://solodev.app/installing-distrobox), download system images and run those images as containers. Miniconda is similar, but downloads a specific Python version (if defined) and specific packages (that are used within the environment.)

Miniconda includes a package manager called `conda`. Below is a description of how to install Miniconda, which is a free installer form the creators of [Anaconda](https://www.anaconda.com/).

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

# Updating the System.

* I update my system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

# What is Miniconda?

Miniconda is a free, small, bootstrap version of Anaconda that includes the conda package manager, Python, packages they both depend on, and a small number of other useful packages (like pip and zlib).

## Installing Miniconda.

* I make the Miniconda directory:
    

```bash
mkdir -p ~/miniconda3
```

* I download the installation payload:
    

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
```

* I run the installation:
    

```bash
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
```

* I remove the payload:
    

```bash
rm -rf ~/miniconda3/miniconda.sh
```

## Initialising Miniconda.

* I initialize `Miniconda`:
    

```bash
~/miniconda3/bin/conda init bash
```

## Updating Miniconda.

* I make my account the owner of the `Miniconda` directory:
    

```bash
sudo chown -R $USER:$USER $HOME/miniconda3
```

* I refresh the terminal:
    

```bash
. ~/.bashrc
```

* I update `Miniconda`:
    

```bash
conda update -n base -c defaults conda
```

## Setting the (base) Home Directory.

* I make new directories within the (`base`) environment:
    

```bash
mkdir -p ~/miniconda3/etc/conda/activate.d
```

* I use the Nano text editor to create the (`set_working_directory.sh`) shell script:
    

```bash
sudo nano ~/miniconda3/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the set\_working\_directory.sh script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~
```

> NOTE: I will now return to my `Home` directory whenever I run `conda activate`.

## Uninstalling Miniconda.

* I activate the `Miniconda` (base) environment:
    

```bash
conda activate
```

* I remove any `conda` initialization scripts:
    

```bash
conda init --reverse --all
```

* I remove `Miniconda` from the $HOME directory:
    

```bash
rm -rf $HOME/miniconda3
```

* I also remove `Miniconda` from the `/opt` directory, if required:
    

```bash
rm -rf $HOME/opt/miniconda3
```

---

# Miniconda Environment Commands.

* I display a list of Miniconda commands:
    

```bash
conda
```

* I display a list of Miniconda environment commands:
    

```bash
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
mkdir -p ~/miniconda3/envs/better-env/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/better-env/etc/conda/activate.d/set_working_directory.sh
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

---

# What is Python?

Python is an easy-to-understand programming language that is perfect for quickly creating applications and connecting different parts. It has built-in tools for organizing and reusing code. The Python interpreter and a large standard library are free for everyone on all major platforms. Programmers like Python because it speeds up our work. Since there's no need to compile my programs, editing, testing, and debugging is fast. Debugging Python programs is simple, as errors or bad inputs don't cause crashes. Instead, the interpreter shows an exception. If the program doesn't catch it, the interpreter displays a stack trace. A source level debugger lets me check variables, evaluate expressions, set breakpoints, and go through the code step by step. The debugger is even made in Python, showing its power. Sometimes, the quickest way to debug my code is to add print statements *to* my code. The fast edit-test-debug cycle makes this method very effective.

## Testing Python.

* I use Nano to create a module called `hello.py`:
    

```bash
sudo nano hello.py
```

* I copy the following, add (CTRL + SHIFT + V) it to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
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

---

# The Results.

Miniconda is a compact version of Anaconda that comes with Python and the conda package manager. It allows me to create separate environments for different projects, ensuring that I have the right versions of Python and any packages I need. By following the steps outlined in this post, I can smoothly install, use, and even uninstall Miniconda on a Debian-based Linux distro. Moreover, with a basic understanding of Python, I can start creating applications quickly and efficiently.

---

# In Conclusion.

Have I ever struggled with managing different versions of Python and packages for different projects? Am I looking to streamline the development of my Python projects? Miniconda could be the answer!

Miniconda is a compact version of Anaconda that includes Python, the conda package manager, and a few other useful tools. It is a lifesaver for Python developers! I can create separate environments for different projects, ensuring that I have the right versions of Python and any packages I need.

The best part? It's free and works perfectly on a Debian-based Linux distro, like Ubuntu.

This is a comprehensive post on how to install, use, and even uninstall Miniconda. I've also included how to create, rename, and delete environments. And for those new to Python, I've included a quick intro to this versatile programming language and how I tested my first Python module.

I use Miniconda to make my Python project management a breeze.

Has anyone else used Miniconda? What's been your experience? Share your thoughts below!

Until next time: Be safe, be kind, be awesome.

---

#Python #PythonDevelopment, #Miniconda #MinicondaGuide, #Programming, #Coding, #DataScience, #Ubuntu, #EnvironmentManagement, #Anaconda, #PythonApplications