---
title: "Local AI Toolkit."
seoTitle: "Local AI Toolkit: A Comprehensive Installation Guide"
seoDescription: "Discover how to set up a powerful local AI toolkit on Ubuntu with this comprehensive guide. Learn to install and manage essential AI tools like Ollama."
datePublished: Wed Apr 30 2025 10:00:42 GMT+0000 (Coordinated Universal Time)
cuid: cma3rmqr4000o08l6g7mr4zpz
slug: local-ai-toolkit
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746233213818/9ff97f58-6ff6-4dd1-bf6a-26e002239b7e.png
tags: ai, artificial-intelligence, ubuntu, linux, machine-learning, coding, deep-learning, innovation, ai-development, ai-community, open-source, ai-models, future-tech, tech-guide, tech-tools

---

## TL;DR.

This post is a guide to setting up a local AI toolkit on a Debian-based Linux distribution, specifically Ubuntu. It covers the installation and management of various AI tools and frameworks, including Ollama, CrewAI, Pinokio, Open WebUI, LM Studio, Ngrok, and Cursor. This guide includes step-by-step instructions for installing, updating, and uninstalling these tools, as well as setting up virtual environments for best practices. Additionally, it offers insights into the functionalities of each tool and how they can be utilized for AI development.

> **Attributions:**
> 
> ***various ↗.***

---

## An Introduction.

This post highlights the tools I find useful as an AI enthusiast. I want to share my insights into these tools and explain why they are beneficial to AI developers:

> The purpose of this post is to describe the tools that I, as an AI enthusiast, find useful.

---

## The Big Picture.

November 30th 2022 saw the launch of AI’s first killer app: ChatGPT (Generative Pre-trained Transformer). Three months later, in February 2023, someone “leaked“ the first LLM (Large Language Model) from Meta, the corporation that owns Facebook. Since then, many open LLMs have dropped and Hugging Face has become the de facto centre for these models.

The year is now 2025 and over the last two and-a-bit years there has been an explosion of tools and workflows hitting the Internet. The continued growth of commercial, frontier LLMs (e.g. OpenAI models such as GPT-4o, GPT-4o mini, and the GPT-4.1 series) has easily matched, and usually surpasses, the power of my favourite open models (DeepSeek-R1, Phi4, Qwen3, etc.) However, thanks to the rise of open reasoning models, MoE (Mixture of Experts) models, agents, agentic tools, RAG (Retrieval-Augmented Generation) knowledge saved in vector databases, and AI-specific scraping tools like Crawl4AI, AI enthusiasts like myself can develop our vibe coding skills on our own PCs.

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

> NOTE: An error typically displays (see below) because Ollama, by default, *already* runs as a background service. Also, by default, the Ollama localhost (127.0.0.1 or 0.0.0.0) port is 11434.
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
ollama pull codellama:13b &&
ollama pull qwen2.5-coder:14b &&
ollama pull qwen2.5:14b &&
ollama pull granite3.2-vision:2b &&
ollama pull granite3.2:8b &&
ollama pull llama3.1:8b &&
ollama pull llama3.2-vision:11b &&
ollama pull llama3.2:3b &&
ollama pull gemma3:12b &&
ollama pull phi4:14b &&
ollama pull deepseek-coder-v2:16b &&
ollama pull deepseek-r1:14b
```

> NOTE: Theses models are perfect for running on my GTX3060 GPU with 12GB VRAM.

* I list the LLMs (large language models) downloaded by Ollama:
    

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

CrewAI is a framework that is used to build AI crews, agents, and tools.

### Installing CrewAI.

> NOTE: Best practice involves installing this app in a virtual environment, using either venv or [conda](https://solodev.app/installing-miniconda).

* From the terminal, I install CrewAI and its’ tools:
    

```bash
pip install crewai 'crewai[tools]'
```

---

## What is Crawl4AI?

Crawl4AI is a web-scraping tool that can conform website data into a format that can be understood by AI models, or prepared for uploading to a vector database.

### Installing Crawl4AI.

> NOTE: Best practice involves installing this app in a virtual environment, using either venv or [conda](https://solodev.app/installing-miniconda).

* I use the pip command to install Crawl4AI:
    

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

## What are VS Code Extensions?

VS Code is a FREE, open-source IDE (integrated development environment) from Microsoft. Extensions are add-on that are installed within VS Code. These extensions provide extra functionality without having to make changes to the VS Code source code.

### Some Popular AI Extensions for VS Code.

Some of my favourite AI Extensions for VS Code include:

* Twinny,
    
* Roo Code,
    
* Cline, and
    
* Continue.
    

---

## What is OpenRouter.ai?

OpenRouter is a platform that provides a unified API for accessing various large language models (LLMs) from multiple providers.

### Open Models vs. OpenRouter.

I prefer downloading, and using, open models on my local system. This ensures my data does not leak and my constructs are not used to train frontier models. Sometimes, however, I need access to better models with more parameters that run on better hardware.

Choosing OpenRouter over open models depends on my requirements at each stage of a project.

---

## What is Cursor?

Cursor is an IDE, an integrated development environment forked from VS Code, that is used for AI development.

> NOTE: The following process can be use on any AppImage app.

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

## What is LM Studio?

LM Studio is an AI application for locally running AI models.

> The following process can be use on any AppImage app.

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

#AI #Artificial-Intelligence #Machine-Learning #Deep-Learning #AI-Development #Ubuntu #Linux #Open-Source #Tech-Tools #AI-Models #Coding #Tech-Guide #AI-Community #Innovation #Future-Tech