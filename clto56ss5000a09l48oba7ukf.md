---
title: "Installing AutoGen Studio."
datePublished: Tue Mar 12 2024 09:00:37 GMT+0000 (Coordinated Universal Time)
cuid: clto56ss5000a09l48oba7ukf
slug: installing-autogen-studio
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710120551470/cd789399-8f19-47f8-b43d-2ba27e5b34f0.png
tags: ai, technology, innovation, miniconda, python-projects, ai-agents, llama2, ollama, litellm, autogen-studio, ai-collaboration, ai-problem-solving, ai-creativity

---

# TL;DR.

This post is a guide through installing and setting up Microsoft AutoGen Studio, a tool for orchestrating collaborative AI agents. It covers prerequisites like setting up Ubuntu with Miniconda, Ollama and Llama2, and LiteLLM. The process includes updating my system, running Llama2 models with Ollama, using LiteLLM as a proxy, and creating a Miniconda environment. I then delve into installing AutoGen Studio, connecting new models, creating new agents, building new workflows, and defining new skills. AutoGen Studio enhances AI collaboration, decision-making, and creativity, and transforms how AI agents collectively tackle complex problems.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗,***
> 
> [https://ollama.com](https://ollama.com)↗,
> 
> [https://litellm.ai](https://litellm.ai)↗, and
> 
> [https://microsoft.github.io/autogen/blog/2023/12/01/AutoGenStudio/](https://microsoft.github.io/autogen/blog/2023/12/01/AutoGenStudio/)***↗.***

# An Introduction.

AutoGen Studio is the browser-based GUI (graphical use interface) for AutoGen, the *actual* multi-agent orchestrator. AutoGen Studio takes all the user-generated inputs and places them in the configuration and settings files that are used by AutoGen.

> The purpose of this post is to install, setup, and prepare AutoGen Studio for use.

# The Big Picture.

Over the last 10-months, I've been quietly publishing to my blog. Now that many of the basic technology posts are out there, I can start referring to them as I build more complex solutions for the 12 Startups challenge. I will still publish basic technology posts, as needed, but this will be the last of the easy articles. After this post, my topics will start getting complicated. I hope you enjoy this final, simple walk-through.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda),
    
* [Ollama](https://solodev.app/installing-ollama), and
    
* [LiteLLM](https://solodev.app/installing-litellm).
    

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

# What is Ollama?

Ollama is a tool for downloading, setting up, and running LLMs (large language models). It lets me access powerful models like Llama 2 and Mistral and helps me run them on my local Linux, macOS, and Windows systems.

[https://ollama.com/](https://ollama.com/)↗.

[Miniconda must be installed](https://solodev.app/installing-miniconda) (`conda --version`) before continuing with this post.

[Ollama must be installed](https://solodev.app/installing-ollama) (`ollama -v`) before continuing with this post.

## Running the Llama2 Model.

> NOTE: [Miniconda](https://solodev.app/installing-miniconda) and [Ollama](https://solodev.app/installing-ollama) were installed in previous posts.

* From the (base) terminal, I switch to the Ollama environment:
    

```bash
conda activate Ollama
```

> NOTE: [Install Miniconda](https://solodev.app/installing-miniconda) to successfully run this command.

* In the Ollama environment, I run the Llama2 model:
    

```bash
ollama run llama2
```

> NOTE: [Install Ollama](https://solodev.app/installing-ollama) to successfully run this command.

# What is LiteLLM?

LiteLLM is a proxy that provides LLMs with IP addresses. It is a unified interface that calls 100+ LLMs using the same Input/Output format, supporting OpenAI, Huggingface, Anthropic, vLLM, Cohere, and even custom LLM API services.

[https://litellm.ai/](https://litellm.ai/%E2%86%97)↗.

[LiteLLM must be installed](https://solodev.app/installing-litellm) (`litellm -v`) before continuing with this post.

## Running the LiteLLM Proxy.

> NOTE: [Miniconda](https://solodev.app/installing-miniconda) and [LiteLLM](https://solodev.app/installing-litellm) were installed in previous posts.

* I open a *second* (base) terminal and switch to the LiteLLM environment:
    

```bash
conda activate LiteLLM
```

> NOTE: [Install Miniconda](https://solodev.app/installing-miniconda) to successfully run this command.

* In the LiteLLM environment, I proxy the Llama2 model:
    

```bash
litellm --port 6000 --model ollama/llama2
```

> NOTE: [Install LiteLLM](https://solodev.app/installing-litellm) to successfully run this command.

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments specifically to avoid any conflicts between these versions.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the conda package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the conda package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/↗](http://www.anaconda.com/%E2%86%97),

[https://docs.anaconda.com/free/miniconda/index.html↗](https://docs.anaconda.com/free/miniconda/index.html%E2%86%97), and

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

[Miniconda must be installed](https://solodev.app/installing-miniconda) (`conda -V`) before continuing with this post.

## Creating the AutoGen Environment.

* I open a *third* (base) terminal and use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (AutoGen):
    

```bash
conda create -n AutoGen python=3.11 -y && conda activate AutoGen
```

> NOTE: This command creates the (AutoGen) environment, then activates the (AutoGen) environment.

## Creating the AutoGen Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the AutoGen home directory:
    

```bash
mkdir ~/AutoGen
```

* I make new directories within the (AutoGen) environment:
    

```bash
mkdir -p ~/miniconda3/envs/AutoGen/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/AutoGen/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/AutoGen
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (AutoGen) environment:
    

```bash
conda activate AutoGen
```

> NOTE: I should now, by default, be in the `~/AutoGen` home directory.

# What is AutoGen Studio?

AutoGen Studio is a cutting-edge, GUI-based, multi-agent framework from Microsoft. It orchestrates role-playing, autonomous AI agents by introducing a new approach to collaborative decision-making, enhanced creativity, and solving complex problems. AutoGen Studio empowers AI agents to work together so they can, collectively, tackle complex tasks. AI agents are quickly emerging as problem-solving partners, creativity colleagues, and innovation initiators.

[https://microsoft.github.io/autogen/blog/2023/12/01/AutoGenStudio/](https://microsoft.github.io/autogen/blog/2023/12/01/AutoGenStudio/)***↗.***

A similar tool to AutoGen Studio is CrewAI.

## Installing, and Running, AutoGen Studio.

* I install AutoGen Studio:
    

```bash
pip install autogenstudio
```

> NOTE: AutoGen is automatically installed with AutoGen Studio.

* I check the installation:
    

```bash
autogenstudio version
```

* I add an OpenAPI key:
    

```plaintext
export OPENAI_API_KEY='1111'
```

* I check the key:
    

```plaintext
echo $OPENAI_API_KEY
```

* I run AutoGen Studio:
    

```bash
autogenstudio ui --host 0.0.0.0 --port 7000
```

> NOTE: Although LiteLLM and AutoGen Studio are using the same host IP address (0.0.0.0), LiteLLM is on port 6000 and AutoGen Studio is on port 7000.

## Connecting a New Model.

* I open AutoGen Studio in a browser:
    

```bash
localhost:7000
```

* At the top, I click the Build tab.
    
* On the left, I click the Models tab.
    
* At the top-right, I click the green "+ New Model" button and fill out the details.
    
* After using them as examples, I delete the default Models.
    

## Creating a New Agent.

* On the left, I click the Agents tab.
    
* At the top-right, I click the green "+ New Agent" button and fill out the details.
    
* After using them as examples, I delete the default Agents.
    

```plaintext
You are a helpful AI assistant. Solve tasks using your coding
and language skills. In the following cases, suggest python code
(in a python coding block) or shell script (in a sh coding block)
for the user to execute.

1. When you need to collect info, use the code to output the info
you need, for example, browse or search the web, download/read a file,
print the content of a webpage or a file, get the current date/time,
check the operating system. After sufficient info is printed and the
task is ready to be solved based on your language skill, you can solve
the task by yourself.

2. When you need to perform some task with code, use the code to
perform the task and output the result. Finish the task smartly.
Solve the task step by step if you need to. If a plan is not provided,
explain your plan first. Be clear which step uses code, and which
step uses your language skill. When using code, you must indicate
the script type in the code block. The user cannot provide any other
feedback or perform any other action beyond executing the code you
suggest. The user can't modify your code. So do not suggest incomplete
code which requires users to modify. Don't use a code block if it's
not intended to be executed by the user. If you want the user to save
the code in a file before executing it, put # filename: <filename>
inside the code block as the first line. Don't include multiple code
blocks in one response. Do not ask users to copy and paste the result.
Instead, use 'print' function for the output when relevant. Check the
execution result returned by the user. If the result indicates there is
an error, fix the error and output the code again. Suggest the full
code instead of partial code or code changes. If the error can't be
fixed or if the task is not solved even after the code is executed
successfully, analyze the problem, revisit your assumption, collect
additional info you need, and think of a different approach to try.
When you find an answer, verify the answer carefully. Include
verifiable evidence in your response if possible. Reply
'TERMINATE' in the end when everything is done.
```

## Creating a New Workflow.

* On the left, I click the Workflows tab.
    
* At the top-right, I click the green "+ New Workflow" button and fill out the details.
    
* After using them as examples, I delete the default Workflows.
    

## Creating a New Skill.

* On the left, I click the Skills tab.
    
* At the top-right, I click the green "+ New Skills" button and fill out the details.
    
* After using them as examples, I delete the default Skills.
    

# The Results.

In this post, I covered the installation and setting up of AutoGen Studio. This is a Microsoft tool that is designed to enhance collaborative AI engagement and problem-solving. I started with the prerequisites needed to set up my environment, including the installation of Miniconda, Ollama running Llama2, and LiteLLM. I then delved into AutoGen Studio itself, where I walked through the installation, and setup, process. I looked at how to connect new models, create new agents, develop new workflows, and design new skills AutoGen Studio is a versatile tool and has the potential to transform AI collaboration. AutoGen Studio, like CrewAI, offers a platform for orchestrating AI agents that solve complex problems, fosters creativity, and promotes innovation.

# In Conclusion.

I recently dived into the world of AutoGen Studio, a Microsoft tool designed to enhance the way AI agents work together. It introduces a new approach to collaborative decision-making, creativity, and tackling complex challenges.

In my journey, I started with setting up the essentials:

* A Debian-based Linux distro called Ubuntu.
    
* The installations of Miniconda, Ollama, and LiteLLM.
    

After updating my (base) system, I used my understanding of Miniconda, Ollama and Llama2, and LiteLLM to deploy AutoGen Studio as a contained Python project.

AutoGen Studio is a multi-agent framework that orchestrates role-playing, autonomous, AI agents that work together to solve complex problems and generate creative results.

I walked through the installation process and set up new models, new agents, new workflows, and new skills. AutoGen Studio (like CrewAI) has the potential to transform AI collaboration. Further exploration into this tool will reveal the future of collaborative AI, a future where agents become partners in creativity and innovation.

What do you think the impact of such collaborative AI tools will be on the future of technology and innovation?

Until next time: Be safe, be kind, be awesome.

#AutoGenStudio #AI #AICollaboration #AIagents #AIproblemSolving #AIcreativity #PythonProjects #Technology #Innovation #Miniconda #Ollama #Llama2 #LiteLLM