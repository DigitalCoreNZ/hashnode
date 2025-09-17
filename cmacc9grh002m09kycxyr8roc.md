---
title: "Local AI Toolkit for Ubuntu."
seoTitle: "AI Toolkit for Local Use"
seoDescription: "Guide to setting up a local AI toolkit on Ubuntu, including installation and management of various AI tools and frameworks"
datePublished: Tue May 06 2025 10:00:24 GMT+0000 (Coordinated Universal Time)
cuid: cmacc9grh002m09kycxyr8roc
slug: local-ai-toolkit-for-ubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746921051526/d469b47f-6f93-4f61-b561-fd72aa6fcce1.png
tags: ai, artificial-intelligence, ubuntu, linux, machine-learning, coding, deep-learning, innovation, ai-development, ai-community, open-source, ai-models, future-tech, tech-guide, tech-tools

---

Last update: Wednesday 17th September 2025

## TL;DR.

This post is a guide to setting up a local AI toolkit on a Debian-based Linux distribution, specifically Ubuntu. It covers the installation and management of various AI tools and frameworks, including:

* Ollama,
    
* CrewAI,
    
* Crawl4AI,
    
* LLM Axe,
    
* AI Extensions for VS Code,
    
* OpenRouter.ai,
    
* Cursor,
    
* Windsurf,
    
* LM Studio,
    
* Open WebUI,
    
* Pinokio, and
    
* Ngrok.
    

This guide includes step-by-step instructions for installing, updating, and uninstalling these tools, as well as promoting virtual environments (specifically [Conda](https://solodev.app/installing-miniconda)) for best practices. Also, this post occasionally offers insights into these tools and how they are utilised during AI development.

Although this post contains many AI tools, the only ones I actually use are Ollama, CrewAI, Crawl4AI, the LLM Axe toolkit, the AI extensions for VS Code, and the OpenRouter.ai website.

> **Attributions:**
> 
> ***various ↗.***

---

## An Introduction.

This post highlights the tools I find useful as an AI enthusiast. I want to share my insights into these tools and explain why they are beneficial to AI developers:

> The purpose of this post is to describe the tools that I, as an AI enthusiast, find useful.

---

## The Big Picture.

November 30th 2022 saw the launch of AI’s first killer app: ChatGPT (Generative Pre-trained Transformer). Three months later, in February 2023, someone “leaked“ the first, open LLM (Large Language Model) which was built by Meta, the corporation that owns Facebook. Since then, many open models have dropped and Hugging Face has become the de facto centre for these AI machines.

> NOTE: From here on, I will refer to LLMs as models.

It is now early 2025 and, over the last two and-a-bit years, there has been an explosion of tools and workflows hitting the Internet. The continued growth of commercial, frontier models (e.g. OpenAI models such as GPT-4o, GPT-4o mini, and the GPT-4.1 series) has easily matched, and usually surpassed, the power of my favourite open models (DeepSeek-R1, Phi4, Qwen3, etc.) However, thanks to the rise of MoE (Mixture of Experts) models, reasoning models, agents, agentic tasks and tools, RAG (Retrieval-Augmented Generation) processes, and AI-specific scraping tools, AI enthusiasts can easily develop vibe coding skills *on local PCs* using open models, frontier models, or a combination of both types of systems.

---

## Prerequisites.

* A Debian-based Linux distribution (I use Ubuntu),
    
* Python 3.11+.
    

---

## Updating my Base System.

* From the (base) terminal, I update my (base) system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

## What is Ollama?

Ollama is a local, large language model manager that facilitates the installation, management, and operation of AI models on personal computers.

### Installing Ollama.

* From the terminal, I install Ollama:
    

```bash
curl https://ollama.com/install.sh | sh
```

* I run Ollama as a background service:
    

```bash
ollama serve &
```

> NOTE: An error typically displays (see below) because Ollama, by default, *already* runs as a background service. Also, by default, Ollama runs on port 11434.
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1745578527337/acba5663-7582-4eba-8f4b-6475a7bcba16.png align="center")

### Updating Ollama.

* I update Ollama:
    

```bash
curl https://ollama.com/install.sh | sh
```

> NOTE: The update command is the same as the install command.

### Pulling Models from Ollama.

* I pull the following models from Ollama (it will take time for these downloads to complete):
    

```bash
ollama pull nomic-embed-text:v1.5 &&
ollama pull qwen2.5-coder:14b &&
ollama pull deepcoder:14b &&
ollama pull codellama:13b &&
ollama pull opencoder:8b &&
ollama pull falcon3:10b &&
ollama pull dolphin3:8b &&
ollama pull gemma3:12b &&
ollama pull cogito:14b &&
ollama pull tulu3:8b &&
ollama pull olmo2:13b &&
ollama pull marco-o1:7b &&
ollama pull openthinker:7b &&
ollama pull smallthinker:3b &&
ollama pull granite3.2-vision:2b &&
ollama pull granite3.3:8b &&
ollama pull exaone3.5:7.8b &&
ollama pull exaone-deep:7.8b
```

```bash
ollama pull llama3.1:8b &&
ollama pull llama3.2-vision:11b &&
ollama pull llama3.2:3b &&
ollama pull qwen2.5vl:7b &&
ollama pull qwen2.5-coder:14b &&
ollama pull qwen3:14b &&
ollama pull phi4:14b &&
ollama pull phi4-mini:3.8b &&
ollama pull phi4-reasoning:14b &&
ollama pull phi4-mini-reasoning:3.8b &&
ollama pull deepseek-coder-v2:16b &&
ollama pull deepseek-r1:14b
```

> NOTE: Theses models are perfect for running on my GTX3060 GPU with 12GB VRAM. Also, this list is continually updated. If a newer version of a model is released, I remove the old listing above, replace it with the new listing, run the pull commands, list the installed models (`ollama ls`), and remove (`ollama rm <model-name>`) the older model.

* I list the models downloaded by Ollama:
    

```bash
ollama list
```

### Uninstalling Ollama.

* I stop the Ollama service:
    

```bash
sudo systemctl stop ollama
```

* I disable the Ollama service:
    

```bash
sudo systemctl disable ollama
```

* I remove the Ollama service:
    

```bash
sudo rm /etc/systemd/system/ollama.service
```

* I remove the Ollama binary from my bin directory:
    

```bash
sudo rm $(which ollama)
```

* I remove the models downloaded by Ollama:
    

```bash
sudo rm -r /usr/share/ollama
```

* I delete the Ollama service user:
    

```bash
sudo userdel ollama
```

* I delete the Ollama service group:
    

```bash
sudo groupdel ollama
```

---

## What is CrewAI?

CrewAI is a framework that is used to build AI crews, agents, tasks, and tools.

### Installing CrewAI.

> NOTE: Best practice involves installing this app in a virtual environment, using either venv or [Conda](https://solodev.app/installing-miniconda).

* From the terminal, I use the pip command to install CrewAI and its’ tools:
    

```bash
pip install crewai 'crewai[tools]'
```

---

## What is Crawl4AI?

Crawl4AI is a web-scraping tool that can conform website data into a format that can be understood by AI models, or the data can be prepared for uploading to a vector database (pending).

### Installing Crawl4AI.

> NOTE: Best practice involves installing this app in a virtual environment, using either venv or [Conda](https://solodev.app/installing-miniconda).

* I use the pip command to install the updated version of Crawl4AI:
    

```python
pip install -U crawl4ai
```

* I setup Crawl4AI:
    

```python
crawl4ai-setup
```

* I verify the Crawl4AI installation:
    

```python
crawl4ai-doctor
```

---

## What is LLM Axe?

LLM Axe is a toolkit that provides simple abstractions for commonly used LLM functions.

### Installing LLM Axe.

* I use pip to install LLM Axe:
    

```bash
pip install llm-axe
```

---

## What are AI Extensions for VS Code?

VS Code is a FREE, open-source IDE (integrated development environment) from Microsoft. Extensions are add-ons that are installed within VS Code. These extensions provide extra functionality without having to make changes to the VS Code source code. AI extensions for VS Code are tools and integrations that connect to local, and remote, AI models.

### Some Popular AI Extensions for VS Code.

Some of my favourite AI Extensions for VS Code include:

* Twinny,
    
* Roo Code,
    
* Cline, and
    
* Continue.
    

Other Extensions I find useful include:

* AsciiDoc from AsciiDoctor,
    
* AsciiDoctor PDF from AsciiDoctor,
    
* vscode-pdf from tomoki1207, and
    
* Code Spell Checker from Street Side Software.
    

> NOTE: I have a post that covers the installation of [VS Code and some of its’ Extensions](https://solodev.app/local-system-toolkit-for-ubuntu#heading-installing-vs-code).

---

## What is OpenRouter.ai?

[OpenRouter](https://openrouter.ai/) ***↗*** provides a single API for accessing numerous models from multiple providers.

### Open Models vs. OpenRouter.

I prefer downloading open models to my local system, and then using these models on my personal computer. Using local models ensures my data does not leak, and my constructs are not used to train other models. Sometimes, however, I need to run complex inference. In those cases, I will use better models that run on powerful hardware. This is why I sometimes switch to using OpenRouter.

Choosing to use OpenRouter over open models depends on my requirements at each stage of a project.

---

## What is Cursor?

Cursor is a VS Code fork that provides an improved AI development experience.

> NOTE: The following process can be used to install any AppImage app.

### Installing Cursor.

> ATTRIBUTION: [https://forum.cursor.com/t/tutorial-install-cursor-permanently-when-appimage-install-didnt-work-on-linux/7712](https://forum.cursor.com/t/tutorial-install-cursor-permanently-when-appimage-install-didnt-work-on-linux/7712)

* From a browser, I download the AppImage file from the [cursor.com](https://www.cursor.com) website.
    
* From the file manager, I move the Cursor app to the NAS (network attached storage) server.
    
* From the terminal, I create the Apps/Cursor directory:
    

```bash
mkdir ~/Apps/Cursor
```

* I copy the Cursor download to the the Apps/Cursor directory:
    

```bash
cp ~/Downloads/Ubuntu/Cursor/Cursor*.AppImage ~/Apps/Cursor/Cursor.AppImage
```

> NOTE: This copy command changes the download name to Cursor.AppImage.

* OPTIONAL:
    
* OPTIONAL: I copy the 128px by 128px logo to the ~/Apps/Cursor directory:
    

```bash
cp /media/brian/Drawings/logos/cursor/Images/Cursor-icon.png ~/Apps/Cursor/Cursor-icon.png
```

> NOTE: I downloaded this image from the Internet.

* I make the AppImage executable:
    

```bash
chmod +x ~/Apps/Cursor/Cursor.AppImage
```

* I use the Nano text editor to create a desktop entry:
    

```bash
nano ~/.local/share/applications/cursor.desktop
```

* I paste (CTRL + SHIFT + V) the following into the desktop entry:
    

```bash
[Desktop Entry]
Name=Cursor
Exec=~/Apps/Cursor/Cursor.AppImage
Icon=~/Apps/Cursor/Cursor-icon.png
Type=Application
Categories=Utility;Development;
```

* I save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor.
    
* I create a symlink to start Cursor from the terminal:
    

```bash
sudo ln -s ~/Apps/Cursor/Cursor.AppImage /usr/local/bin/cursor
```

* I restart my system.
    
* From the terminal, I run the Cursor IDE:
    

```bash
cursor
```

---

## What is Windsurf?

Windsurf is an AI-powered code editor designed to enhance the coding experience with features like automatic context analysis, AI-driven autocompletion, and an intuitive user interface.

### Installing Windsurf.

* I add the Windsurf repo to my local system:
    

```bash
curl -fsSL "https://windsurf-stable.codeiumdata.com/wVxQEIWkwPUEAGf3/windsurf.gpg" | sudo gpg --dearmor -o /usr/share/keyrings/windsurf-stable-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/windsurf-stable-archive-keyring.gpg arch=amd64] https://windsurf-stable.codeiumdata.com/wVxQEIWkwPUEAGf3/apt stable main" | sudo tee /etc/apt/sources.list.d/windsurf.list > /dev/null
```

* I update my system:
    

```bash
sudo apt update
```

* I upgrade Windsurf:
    

```bash
sudo apt upgrade windsurf
```

---

## What is LM Studio?

LM Studio is an AI application for running local AI models.

> NOTE: The following process can be used to install any AppImage app.

### Installing LM Studio.

* I use a browser to download the AppImage file from the [https://lmstudio.ai/download](https://lmstudio.ai/download) website.
    
* From the file manager, I move the LMStudio app to the NAS (network attached storage) server.
    
* From the terminal, I create the Apps/LMStudio directory:
    

```bash
mkdir ~/Apps/LMStudio
```

* I copy the LMStudio download to the the Apps/LMStudio directory:
    

```bash
cp /media/brian/Downloads/Ubuntu/'LM Studio'/LM*.AppImage ~/Apps/LMStudio/LMStudio.AppImage
```

> NOTE: This copy command changes the download name to LMStudio.AppImage.

* I copy the 128px by 128px logo from the NAS to the ~/Apps/LMStudio directory:
    

```bash
cp /media/brian/Drawings/logos/lmstudio/Images/LMStudio-icon.png ~/Apps/LMStudio/LMStudio-icon.png
```

> NOTE: I downloaded this image from the Internet.

* I make the AppImage executable:
    

```bash
chmod +x ~/Apps/LMStudio/LMStudio.AppImage
```

* I use the Nano text editor to create a desktop entry:
    

```bash
nano ~/.local/share/applications/lmstudio.desktop
```

* I paste (CTRL + SHIFT + V) the following into the desktop entry:
    

```bash
[Desktop Entry]
Name=Cursor
Exec=~/Apps/LMStudio/LMStudio.AppImage
Icon=~/Apps/LMStudio/LMStudio-icon.png
Type=Application
Categories=Utility;Development;
```

* I save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor.
    
* I create a symbolic link (-s) to start Cursor from the terminal:
    

```bash
sudo ln -s ~/Apps/LMStudio/LMStudio.AppImage /usr/local/bin/lmstudio
```

* I run LMStudio:
    

```bash
lmstudio
```

---

## What is Open WebUI?

Open WebUI is a browser-based interface for using AI models.

### Installing Open WebUI.

* From the terminal, I use Docker to pull Open WebUI:
    

```bash
sudo docker pull ghcr.io/open-webui/open-webui:main
```

* Now I can run Open WebUI on port 3000 from within the Docker container:
    

```bash
docker run -d -p 3000:8080 -v open-webui:/app/backend/data --name open-webui ghcr.io/open-webui/open-webui:main
```

* Alternatively, I can start Open WebUI from Docker Desktop.
    

---

## What is Pinokio?

Pinokio is a browser that runs applications.

### Installing Pinokio.

* I use a browser to visit the download page for Pinokio:
    

```bash
https://github.com/pinokiocomputer/pinokio/releases
```

* I download the latest version of Pinokio that runs on Debian (.deb) distributions for AMD64 processors.
    
* From the terminal, I install Pinokio:
    

```bash
sudo apt install -y ~/Downloads/Pinokio*
```

* I run Pinokio from the Apps Drawer.
    

---

## What is Ngrok?

Ngrok creates secure tunnels to localhost, allowing developers to expose local servers to the Internet.

### Installing Ngrok.

* In a browser, I visit the [https://ngrok.com/](https://ngrok.com/) website and create an account.
    
* I copy the authentication token.
    
* From a new terminal tab, I install Ngrok:
    

```bash
sudo snap install ngrok
```

* I add the authentication token:
    

```bash
ngrok config add-authtoken <auth_token>
```

* I point Ngrok to any local port number that is running a server:
    

```bash
ngrok http <local_port_number>
```

---

## The Results.

Setting up a local AI toolkit significantly improves my chances of improving my AI development skills. By following this guide, I efficiently installed, can manage, and will utilise various AI tools and frameworks. Combining Ollama, CrewAI, Pinokio, Open WebUI, LM Studio, Ngrok, and Cursor provides a robust environment for developing and experimenting with open AI models. This well-equipped, local toolkit will help me develop my vibe coding skills.

---

## In Conclusion.

In this post, I described how to set up a powerful local AI toolkit on Ubuntu with step-by-step instructions. I learned how to install and manage AI tools like Ollama, CrewAI, and more, enhancing my AI development capabilities. This article is perfect for AI enthusiasts and developers looking to harness both open and commercial AI technologies.

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#AI #Artificial-Intelligence #AI-Development #AI-Models #AI-Community #Machine-Learning #Deep-Learning #Linux #Ubuntu #Open-Source #Coding #Tech-Guide #Tech-Tools #Future-Tech #Innovation