---
title: "Installing Pythagora and GPT Pilot for Ollama."
datePublished: Fri Mar 15 2024 09:00:53 GMT+0000 (Coordinated Universal Time)
cuid: cltsfipne000109l8gm6i9u8r
slug: installing-pythagora-and-gpt-pilot-for-ollama
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710493227096/bab83dd9-f14f-44b8-aa13-0bf3f35329a4.png
tags: app-development, python-development, miniconda, vscode-extensions, virtual-environments, venv, tech-guide, pythagora, gpt-pilot, software-innovation, coding-future

---

# TL;DR.

This post provides a detailed guide on installing and setting up Pythagora and GPT Pilot, two powerful tools for app development using large language models like GPT-4. The prerequisites include using a Debian-based Linux distro (I use Ubuntu) and building virtual environments with Miniconda and venv. I start with creating a Miniconda environment, setting up a Pythagora home directory, installing Pythagora through VS Code, and configuring GPT Pilot for use with Pythagora. I conclude by listing the potential benefits of using these tools for efficient app development.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗,***
> 
> [https://github.com/Pythagora-io/gpt-pilot](https://github.com/Pythagora-io/gpt-pilot)***↗, and***
> 
> [https://github.com/Pythagora-io/gpt-pilot/wiki/Using-GPT%E2%80%90Pilot-with-Local-LLMs](https://github.com/Pythagora-io/gpt-pilot/wiki/Using-GPT%E2%80%90Pilot-with-Local-LLMs)***↗.***

# An Introduction.

Pythagora (along with Devin) is the newest attempt to integrate large language models (LLMs) into the app development process.

> The purpose of this post is to show how to fuse a local LLM with Pythagora and GPT Pilot.

# The Big Picture.

Pythagora and Devin could be very handy when building the 12 Startups. Devin has not been released at the time of writing, but Pythagora looks extremely promising. (I'm usually an optimist, regardless of how many times I've been burned.)

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

* I use `conda` to `create`, and `activate`, a new environment named (-n) (Pythagora):
    

```bash
conda create -n Pythagora python=3.11 -y && conda activate Pythagora
```

> NOTE: This command creates the (Pythagora) environment, then activates the (Pythagora) environment.

## Creating the Pythagora Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the Pythagora home directory:
    

```bash
mkdir ~/Pythagora
```

* I make new directories within the (Pythagora) environment:
    

```bash
mkdir -p ~/miniconda3/envs/Pythagora/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/Pythagora/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Pythagora
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (Pythagora) environment:
    

```bash
conda activate Pythagora
```

> NOTE: I should now, by default, be in the `~/Pythagora` home directory.

# What is Pythagora?

Pythagora is a tool that creates apps, from the ground up, by utilising the power of LLMs (large language models). It is an extension for VS Code and runs on GPT Pilot, one of the best code generators around. While designed around GPT-4, I have adjusted the GPT Pilot settings so Pythagora can work with local LLMs.

## Installing Pythagora.

* I open VS Code.
    
* I open the Extensions panel.
    
* I search for "Pythagora".
    
* I click on the blue "Install" button for "Pythagora (GPT Pilot) Beta" from Pythagora Technologies.
    
* I select the installation directory for GPT Pilot, i.e. `~/Pythagora`.
    
* I apply for an account, if required.
    
* I click the purple "Create New App" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710459788164/5d34341c-0494-4239-bc41-dff5f5bfa1d7.png align="center")

> NOTE: The rest of this post involves fixing this RuntimeError.

* I exit VS Code.
    

# What is GPT Pilot?

GPT Pilot is the main engine that powers the Pythagora VS Code extension. (The developers of Pythagora want it to be the first, *true* AI assistant for developers.) Together, GPT Pilot and Pythagora do more than just fill in missing code or help with pull request messages. GPT Pilot helps Pythagora act like a *real* AI developer that can write complete features, fix bugs, discuss problems, request reviews, and perform many other code-related tasks.

## Installing GPT Pilot.

* From the (Pythagora) terminal, I update the Ollama utility:
    

```plaintext
curl https://ollama.ai/install.sh | sh
```

* I use the Nano text editor to open the `.env` file:
    

```plaintext
sudo nano ~/Pythagora/gpt-pilot/pilot/.env
```

* I make the following changes, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```plaintext
OPENAI_ENDPOINT=http://localhost:11434/v1/chat/completions
OPENAI_API_KEY=1111

MODEL_NAME=codellama
```

> NOTE: I ensure Ollama has local access to CodeLlama, e.g. `ollama pull codellama`.

## Settings for Pythagora.

> NOTE: Whenever the Pythagora extension is updated within VS Code, these steps will enable its' functionality in the newly-deployed `gpt-pilot` directory.

* I change to the `gpt-pilot` directory:
    

```plaintext
cd ~/Pythagora/gpt-pilot
```

* I install venv:
    

```plaintext
sudo apt install python3.11-venv
```

* I create a new venv (virtual environment):
    

```plaintext
python -m venv --without-pip ~/Pythagora/gpt-pilot/pilot-env
```

* I activate the venv:
    

```plaintext
source ~/Pythagora/gpt-pilot/pilot-env/bin/activate
```

* From the (pilot-env) environment, I install pip:
    

```plaintext
curl https://bootstrap.pypa.io/get-pip.py | python
```

* I check pip:
    

```plaintext
which pip
```

* I upgrade pip:
    

```plaintext
pip install --upgrade pip
```

* I install the requirements:
    

```plaintext
pip install -r ~/Pythagora/gpt-pilot/requirements.txt
```

* I deactivate the (pilot-env) environment:
    

```plaintext
deactivate
```

* I deactivate the (Pythagora) environment:
    

```plaintext
conda deactivate
```

## Testing VS Code.

* I open VS Code.
    
* I click the Pythagora icon in the left pane:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710449204965/e4123c5e-74d9-4361-bfee-85f359a6741f.png align="center")

* I click the purple "Create New App" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710449275656/ed04c606-12eb-4e12-b582-55164aec5816.png align="center")

* I start developing an app.
    

# The Results.

The advent of Pythagora and GPT Pilot marks a significant leap forward in the development of applications using the power of large language models. By leveraging the capabilities of GPT-4 through Pythagora, developers are empowered to create sophisticated applications with an unprecedented level of efficiency and creativity. The installation process, although intricate, opens up a world of possibilities for customization and optimization, allowing for a tailored development experience. As I continue to explore the potential of these tools, it's clear that they represent a new frontier in coding, where the boundaries of what can be achieved are continually expanding. The future of software development is bright, and Pythagora and GPT Pilot are leading the charge towards a more innovative, and automated, era.

# In Conclusion.

I can now dive into the future of app development with Pythagora and GPT Pilot. I can also discover how these powerful tools are revolutionizing the way I create software.

Pythagora is a VS Code extension that uses the might of GPT Pilot, enabling me to efficiently build applications from scratch. But before I leapt into this installation, I ensured my system was ready. I used a Linux distro called Ubuntu and virtual environment managers called Miniconda and venv. A virtual environment is key to many Python projects.

Setting up Pythagora involved creating a dedicated environment and home directory. I navigated through this involved installation by following this step-by-step guide. GPT Pilot enhances Pythagora by powering it with GPT-4 capabilities. However, I tweaked the configurations to use local LLMs instead. Sadly, there was a RuntimeError that stopped Pythagora from running, so I spent the rest of the day tweaking the settings that eventually lead to a running installation.

The combination of Pythagora and GPT Pilot signifies a major leap in the application development cycle. I wholly embrace a future where coding meets efficiency.

I am now ready to start developing my own apps with Pythagora. This detailed guide ensured I had all the tools and knowledge for a clean installation. Join me on my journey as I explore how Pythagora and GPT Pilot are shaping the future of code generation. Don't miss out on unlocking the full potential of these groundbreaking tools. I plan to transform my software development process from "not coding" to "some coding". Eventually.

Until next time: Be safe, be kind, be awesome.

#Pythagora #GPTPilot #PythonDevelopment  
#VSCodeExtensions #AppDevelopment  
#SoftwareInnovation #CodingFuture  
#TechGuide #Miniconda #venv  
#VirtualEnvironments