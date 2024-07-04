---
title: "Installing LiteLLM."
datePublished: Mon Mar 11 2024 09:00:56 GMT+0000 (Coordinated Universal Time)
cuid: cltmprcvt00030ajufrupe5jq
slug: installing-litellm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710060169539/fa901a01-2918-4819-bef7-cbb94cc8c7f1.png
tags: artificial-intelligence, python, programming-ciovqvfcb008mb253jrczo9ye, miniconda, virtual-environments, ai-models, llms, ollama, litellm, tech-tools

---

# TL;DR.

This post is a guide to installing, and using, LiteLLM. It is a tool for accessing a large language model (LLM), like Llama 2 and Mistral, using an IP address and port number. I also cover Miniconda, Ollama, and Llama2. I share my experience with creating virtual environments, managing Python projects, by demonstrating how LiteLLM is used to access to LLMs across a local network, showing the potential of using this tool in AI projects and applications.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)↗,
> 
> [https://ollama.com](https://ollama.com)↗.
> 
> [https://litellm.ai/](https://litellm.ai/)***↗.***
> 
> [https://solodev.app/installing-ollama](https://solodev.app/installing-ollama), and
> 
> [https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

# An Introduction.

LiteLLM is a tool for making LLMs accessible across networks.

> The purpose of this post is to show how to make LLMs accessible.

# The Big Picture.

LLMs are not usually reachable using IP addresses and port numbers. However, such a feature would make LLM accessibility more convenient. Thankfully, LiteLLM is able to act as a proxy so that LLMs are usable across my LAN.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my Base System.

* In the (base) terminal, I update my base system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is Ollama?

Ollama is a tool for downloading, setting up, and running LLMs (large language models). It helps me access powerful models like Llama 2 and Mistral and lets me run them on my local Linux, macOS, and Windows systems.

[https://ollama.com/↗](https://ollama.com/%E2%86%97).

[Ollama must be installed](https://solodev.app/installing-ollama) (`ollama -v`) before continuing with this post.

## Running the Llama2 Model.

* In the (base) terminal, I change to the Ollama environment:
    

```bash
conda activate Ollama
```

> NOTE: [Install Ollama](https://solodev.app/installing-ollama) to successfully run this command.

* I run the Llama2 model:
    

```bash
ollama run llama2
```

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments while avoiding version conflicts.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the `conda` package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the `conda` package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/](http://www.anaconda.com/)***↗,***

[https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

[Miniconda must be installed](https://solodev.app/installing-miniconda) (`conda -V`) before continuing with this post.

## Creating a Miniconda Environment.

* In the second (base) environment, I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (LiteLLM):
    

```bash
conda create -n LiteLLM python=3.11 -y && conda activate LiteLLM
```

> NOTE: This command creates the (LiteLLM) environment, then activates the (LiteLLM) environment.

## Creating the LiteLLM Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the LiteLLM home directory:
    

```bash
mkdir ~/LiteLLM
```

* I make new directories within the (LiteLLM) environment:
    

```bash
mkdir -p ~/miniconda3/envs/LiteLLM/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/LiteLLM/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/LiteLLM
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (LiteLLM) environment:
    

```bash
conda activate LiteLLM
```

> NOTE: I should now, by default, be in the `~/LiteLLM` home directory.

# What is LiteLLM?

LiteLLM provides LLMs with IP addresses. It is a unified interface that calls 100+ LLMs using the same Input/Output format, supporting OpenAI, Huggingface, Anthropic, vLLM, Cohere, and even custom LLM API services.

[https://litellm.ai/](https://litellm.ai/)***↗.***

## Installing, and Using, LiteLLM.

* I install LiteLLM:
    

```bash
pip install litellm 'litellm[proxy]'
```

* I use LiteLLM to run Llama2:
    

```bash
litellm --port 6000 --model ollama/llama2
```

> NOTE: The Llama2 model is now accessible from `http://localhost:6000`.

# The Results.

LiteLLM helps me set up environments that harness the power of large language models (LLMs). This tool provides a unified interface for accessing many LLMs. I also used Miniconda to manage my Python environments and Ollama to download, and run, LLMs like Llama 2. This exploration used virtual environments to manage project dependencies but also highlighted AI tools that make LLM technologies more accessible. My successful setup, and use, of LiteLLM shows how LLMs can be easily integrated into various AI projects and applications.

# In Conclusion.

I dived into setting up LiteLLM. It is used to access an LLM, like Llama 2 and Mistral, using an IP address and port number. LiteLLM is a unified interface that simplifies the integration of many LLMs, making them accessible across my LAN. I also used tools like Miniconda and Ollama.

The results show that Miniconda, Ollama, and LiteLLM make LLM technologies more accessible, and also shows the potential of using these tools in LLM projects. This was a deep dive into the future of AI technologies and their integration into my projects and applications.

What's your experience with LLMs? Have you used tools like Miniconda, Ollama, and/or LiteLLM in your projects? Let's share insights and learn from each other's experiences in harnessing the power of large language models.

Until next time: Be safe, be kind, be awesome.

#LiteLLM #Miniconda #Ollama #LLMs #Python #ArtificialIntelligence #AIModels #TechTools #VirtualEnvironments #Programming