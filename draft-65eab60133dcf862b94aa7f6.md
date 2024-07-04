---
title: "Pair Programming with AI Agents."
slug: pair-programming-with-ai-agents

---

# TL;DR.

\[pending\]

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗.***

# An Introduction.

\[pending\]

# The Big Picture.

> "Always two there are..." - Yoda.

\[pending\]

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

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

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments while avoiding version conflicts.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the `conda` package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the `conda` package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/](http://www.anaconda.com/)***↗,***

[https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

I ensure [Miniconda is installed](https://solodev.app/installing-miniconda) (`conda -V`) before continuing with this post.

## Creating a Miniconda Environment.

* I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (Default):
    

```bash
conda create -n Default python=3.11 -y && conda activate Default
```

> NOTE: This command creates the (Default) environment, then activates the (Default) environment.

## Creating the `Default` Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the `Default` home directory:
    

```bash
mkdir ~/Default
```

* I make new directories within the (Default) environment:
    

```bash
mkdir -p ~/anaconda3/envs/Default/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/anaconda3/envs/Default/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Default
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (Default) environment:
    

```bash
conda activate Default
```

> NOTE: I should now, by default, be in the `~/Default` home directory.

# What is \[pending\]?

\[pending\]

# The Results.

\[pending\]

# In Conclusion.

\[pending\]