---
title: "Installing Twinny for VS Code."
datePublished: Wed Apr 24 2024 10:00:47 GMT+0000 (Coordinated Universal Time)
cuid: clvdn9t4m000209jt2clb0xtl
slug: installing-twinny-for-vs-code
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713951098640/0823da41-3049-48be-be63-782490a41650.png
tags: ai, software-development, coding, vscode, innovation, miniconda, developer-productivity, code-completion, ai-integration, llms, ollama, litellm, twinny, python-environments, coding-assistant

---

# TL;DR.

Installing Twinny for VS Code involves creating two Miniconda environments to run different variations of Code Llama using LiteLLM, which provides accessible IP addresses and ports for local LLMs. Twinny, an AI code completion tool, is integrated into this setup, enhancing coding efficiency by using these local models. This configuration not only boosts coding productivity but also allows for easy model upgrades and integration with other tools, like AutoGen Studio.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗.***

# An Introduction.

Twinny is a code assistant for VS Code. LiteLLM provides Ollama managed LLMs (large language models) with LAN-based IP addresses and ports. Twinny is powered by these LLMs:

> The purpose of this post is to show how to setup Twinny for practical use.

# The Big Picture.

I was unable to run Twinny with the default settings (where Twinny has direct access to Ollama, and the models it manages). This post describes how I will use a potential alternative, where:

* Two LiteLLM environments are used, and
    
* Substitute settings are applied to Twinny.
    

As a bonus, I will also end up with two Miniconda environments where I can run two models that may be used by other tools, like AutoGen Studio. Another perk is that, due to Twinny supporting LiteLLM, the current models can be easily replaced because new models are usually, and quickly, supported by the Ollama team.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my Base System.

* From the (base) Terminal, I update my (base) system:
    

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

## Creating the 1st Miniconda Environment.

* I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (`CodeLlamaInstruct`):
    

```bash
conda create -n CodeLlamaInstruct python=3.11 -y && conda activate CodeLlamaInstruct
```

> NOTE: This command creates the (`CodeLlamaInstruct`) environment, then activates the (`CodeLlamaInstruct`) environment.

## Creating the CodeLlamaInstruct Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the `CodeLlamaInstruct` home directory:
    

```bash
mkdir ~/CodeLlamaInstruct
```

* I make new directories within the (`CodeLlamaInstruct`) environment:
    

```bash
mkdir -p ~/miniconda3/envs/CodeLlamaInstruct/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/CodeLlamaInstruct/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/CodeLlamaInstruct
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (`CodeLlamaInstruct`) environment:
    

```bash
conda activate CodeLlamaInstruct
```

> NOTE: I should now, by default, be in the `~/CodeLlamaInstruct` home directory.

## Creating the 2nd Miniconda Environment.

* I open a 2nd Terminal tab.
    
* I use the `conda` command to display a `list` of Miniconda `env`ironments (`CodeLlamaInstruct` should now be in that list):
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (`CodeLlamaCode`):
    

```bash
conda create -n CodeLlamaCode python=3.11 -y && conda activate CodeLlamaCode
```

> NOTE: This command creates the (`CodeLlamaCode`) environment, then activates the (`CodeLlamaCode`) environment.

## Creating the CodeLlamaCode Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the `CodeLlamaCode` home directory:
    

```bash
mkdir ~/CodeLlamaCode
```

* I make new directories within the (`CodeLlamaCode`) environment:
    

```bash
mkdir -p ~/miniconda3/envs/CodeLlamaCode/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/CodeLlamaCode/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/CodeLlamaCode
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (`CodeLlamaCode`) environment:
    

```bash
conda activate CodeLlamaCode
```

> NOTE: I should now, by default, be in the `~/CodeLlamaCode` home directory.

# What is Ollama?

Ollama is a tool for downloading, setting up, and running LLMs (large language models). It helps me access powerful models like Llama 2 and Mistral and lets me run them on my local Linux, macOS, and Windows systems.

[https://ollama.com/↗](https://ollama.com/%E2%86%97).

[Ollama must be installed](https://solodev.app/installing-ollama) (`ollama -v`) before continuing with this post.

> NOTE: I installed Ollama into my (base) system so it can run in any environment without independently installing it into every environment where it's needed.

# What is LiteLLM?

LiteLLM provides LLMs with IP addresses. It is a unified interface that calls 100+ LLMs using the same Input/Output format, supporting OpenAI, Huggingface, Anthropic, vLLM, Cohere, and even custom LLM API services.

[https://litellm.ai/](https://litellm.ai/)***↗.***

## Using LiteLLM to Run Code Llama: Instruct.

* I return to the 1st Terminal tab.
    
* I install LiteLLM:
    

```bash
pip install litellm 'litellm[proxy]'
```

* I use LiteLLM to run Code Llama: Instruct:
    

```bash
litellm --port 5000 --model ollama/codellama:13b-instruct
```

> NOTE: Code Llama: Instruct is now accessible from `http://localhost:5000`.

## Using LiteLLM to Run Code Llama: Code.

* I switch to the 2nd Terminal tab.
    
* I install LiteLLM:
    

```bash
pip install litellm 'litellm[proxy]'
```

* I use LiteLLM to run Code Llama: Code:
    

```bash
litellm --port 6000 --model ollama/codellama:13b-code
```

> NOTE: Code Llama: Code is now accessible from `http://localhost:6000`.

# What is VS Code?

Visual Studio Code (VS Code) is a simple, yet powerful, code editor that works on my computer with versions for Windows, macOS, and Linux. It natively supports JavaScript, TypeScript, and Node.js. Other programming languages and technical abilities are available to VS Code through the use of appropriate Extensions.

[https://code.visualstudio.com/](https://code.visualstudio.com/%E2%86%97)***↗.***

# What is Twinny?

Twinny is an AI code completion plugin for VS Code. It is also compatible with the VSCodium editor. Twinny is designed to seamlessly work with locally-hosted LLMs (large language models), frameworks, and tools. It supports FIM (fill in the middle) code completion by providing real-time, AI-based suggestions that help as I type my code. I can also discuss my code with an LLM via the sidebar, where I can:

* Get explanations for how a function works,
    
* Ask the LLM to generate tests,
    
* Request code refactoring,
    
* and more.
    

[https://marketplace.visualstudio.com/items?itemName=rjmacarthy.twinny](https://marketplace.visualstudio.com/items?itemName=rjmacarthy.twinny)***↗.***

## Installing Twinny.

* I click the Extensions icon in the left sidebar to open the Extensions tab:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713772602975/d3c1eaaf-1ace-4f92-a899-4b2f8c8bd817.png align="left")

> NOTE: In the menu bar, I can also click `View > Extensions` to open the Extensions tab, or I can use the quick key combo: `CTRL + SHIFT + X`.

* I type `twinny` in the `Search...` dialogue box.
    
* I install the `twinny - AI Code...` Extension from `rjmacarthy`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713775424294/78798ec8-c193-4a72-8d49-fff8105d1339.png align="left")

## Setting Up Twinny.

> NOTE: There are currently two instances of LiteLLM running slight variations of Code Llama. This section of the post changes the default settings so that Twinny can access these LiteLLM instances.
> 
> Also, the original settings used 7B models. I've switched to using 13B versions.

* I click the Twinny icon in the left sidebar to open the Twinny tab:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713775976871/05e7d8b3-c2f9-4765-bd5b-1111e10ca68d.png align="left")

* At the top of the Twinny tab, I click the left-most `Manage twinny...` icon (which looks like a power plug):
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713776280767/af1f3c44-8156-499b-b1e7-09cb8b83d2da.png align="left")

> NOTE: Clicking the `Manage twinny...` icon displays two providers by default: The Instruct (Chat) Provider and the Code (FIM) Provider.

* In the Providers tab, I click the pencil icon for the `codellama:7b-instruct` (Chat) Provider:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713939065891/dfe01583-80a0-4683-8e36-6e3baf827315.png align="left")

* I make the following changes to the Instruct (Chat) Provider, as per the image below, and then I click the blue `Save` button after the changes are made:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713934984445/9249a128-c751-4366-8823-8592eec960af.png align="center")

> NOTE: Clicking the blue Save button returns me to the two Providers listed. Notice the changes that have been saved to the Instruct (Chat) Provider.

* In the Providers tab, I click the pencil icon for the `codellama:7b-code` (FIM) Provider:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713939092225/94c89772-c638-49ef-93ea-cb2e22862b3d.png align="left")

* I make the following changes to the Code (FIM) Provider, as per the image below, and then I click the blue `Save` button after the changes are made:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713935013005/f66f4413-1dc6-4fe7-906c-39dc0ad53fe9.png align="center")

# The Results.

In this post, I explored the process of setting up Twinny, a powerful AI code completion tool for VS Code, using LiteLLM environments to manage different large language models. I created two separate Miniconda environments and configured them to run Code Llama: Instruct and Code Llama: Code. This install demonstrates a flexible setup that enhances coding efficiency and leverages the capabilities of local LLMs. This setup facilitates seamless model integration with VS Code through the use of Twinny. Using LiteLLM also offers the flexibility of switching between different language models and upgrading the models as needed. The potential to extend these models to other tools, like AutoGen Studio, further underscores the versatility of using LiteLLM with the Ollama LLM manager. Ultimately, this configuration allows me to harness AI-assisted coding within my local development environment.

# In Conclusion.

I've supercharged VS Code thanks to Twinny, LiteLLM, and Ollama.

I desperately needed a new coding experience. To achieve this goal, I installed a VS Code extension called Twinny, which is a dynamic, AI-based, code completion tool.

**Setting Up the Environment:** I started by creating two Miniconda environments to run different variations of Code Llama. This boosts efficiency but also prepares my system for future upgrades and integrations with other tools, like AutoGen Studio.

**Integrating LiteLLM:** LiteLLM acts as a bridge, providing accessible IP addresses for accessing local LLMs across my LAN. With LiteLLM, I can easily switch between various language models or upgrade them without hassle.

**Harnessing Twinny:** Twinny leverages LLMs and offers real-time, AI-based coding suggestions. I've tailored Twinny to connect to my local LLMs, enhancing its functionality while providing more precise, and context-aware, coding assistance.

**Results:** The resulting setup provides a more intuitive, AI-enhanced coding environment that adapts to my needs, right within VS Code. This setup simplifies my management of large language models and also magnifies my coding productivity.

Have you considered integrating AI into your coding environment? What tools are you excited to explore? What's your experience with AI-assisted coding?

Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

#VisualStudioCode #Twinny #LiteLLM #Ollama #AI #LLMs #Miniconda #AIIntegration #PythonEnvironments #Coding Assistant #Innovation #Coding #CodeCompletion #SoftwareDevelopment #DeveloperProductivity #TechInnovation #TechTools