---
title: "1 of 2: Installing AnythingLLM for Linux."
datePublished: Tue Feb 27 2024 09:00:18 GMT+0000 (Coordinated Universal Time)
cuid: clt450gwh000c0al5hf3y41em
slug: 1-of-2-installing-anythingllm-for-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708900028424/2974d21b-8dcb-4ae3-943e-ca715920ef2d.png
tags: ai, ubuntu, linux, docker, github, opensource, miniconda, llm, vector-database, chromadb, rag, ollama, tech-tutorial, anythingllm, large-language-model

---

# TL;DR.

This post provides a detailed guide on how I install a Dockerized AnythingLLM on a Debian-based Linux distro called Ubuntu. My process involves setting up various tools including Miniconda, Ollama, ChromaDB, Docker, and an LLM (large language model) called Llama2. I cover the functions of these tools and how they help with running AnythingLLM, a free and versatile document chatbot. This chatbot stands out for its ability to scrape GitHub repositories, making embeddings from the repo scrapings, and saving the results to the ChromaDB vector database.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗,***
> 
> [https://ollama.com/](https://ollama.com/)***↗,***
> 
> [https://www.trychroma.com/](https://www.trychroma.com/)***↗,***
> 
> [https://www.docker.com/](https://www.docker.com/)***↗, and***
> 
> [https://useanything.com/](https://useanything.com/)***↗.***

# An Introduction.

AnythingLLM is a simple-to-use RAG solution the comes with an intuitive UI. This utility is a great tool for app developers, due to its ability to scrape GitLab projects.

> The purpose of this post is to describe how to install AnythingLLM on Ubuntu.

# The Big Picture.

AnythingLLM runs natively on Windows and macOS. Linux support is coming soon. As an Ubuntu user, I usually enjoy immediate access to the latest <s>toys</s> technologies. This time around, I need to wait. Luckily, the developers of AnythingLLM were able to provide their utility as a Docker container (for those of us with allergies to Microsoft and Apple products.)

The killer feature that separates AnythingLLM from other RAG (Retrieval-Augmented Generation) solutions is the ability to scrape GitHub projects. Seriously, this is an amazing ability. Luckily for me, it is easy to deploy this tool to a Linux distro.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my System.

* In a new terminal, I update my system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is Miniconda and Ollama?

Miniconda is a free, small, bootstrap version of Anaconda that includes the `conda` package manager, Python, packages they both depend on, and a small number of other useful packages (like pip and zlib).

Ollama is a tool that is used to download, set up, and run large language models on a local PC. It lets me use powerful models like Llama 2 and Mistral on my personal computer. Ollama natively runs on Linux, macOS, and Windows.

## Creating the Ollama Environment.

* I use `conda` to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (`Ollama`):
    

```bash
conda create -n Ollama python=3.11 -y && conda activate Ollama
```

> NOTE: This command creates the (`Ollama`) environment, then activates the (`Ollama`) environment.

## Creating the Ollama Home Directory.

> NOTE: I will define the home directory with settings in the environment directory.

* I create the `Ollama` home directory:
    

```bash
mkdir ~/Ollama
```

* I make new directories within the (`Ollama`) environment:
    

```bash
sudo mkdir -p ~/miniconda3/envs/Ollama/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/Ollama/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, add it to the script file, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Ollama
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (`Ollama`) environment:
    

```bash
conda activate Ollama
```

> NOTE: I should now be in the (Ollama) environment and the `~/Ollama` home directory.

## Installing Ollama.

* I install Ollama:
    

```bash
curl https://ollama.ai/install.sh | sh
```

* I list the LLMs downloaded by Ollama:
    

```bash
ollama list
```

* If the above command fails, I run Ollama as a background service:
    

```bash
ollama serve &
```

* If the following error shows when running the previous command, that means Ollama is *already* running as a background service:
    

```bash
Error: listen tcp 127.0.0.1:11434: bind: address already in use
```

## Using Ollama to Run the Llama2 Model.

* I run the Llama2 model:
    

```bash
ollama run llama2
```

> NOTE 1: The `ollama run` command performs an `ollama pull` if the model has not already been downloaded.
> 
> NOTE 2: The `ollama run` command is used to run the named LLM.
> 
> NOTE 3: I sometimes need to restart my system to properly run the LLM.

## Testing the Llama2 Model.

* At the `>>>` prompt, I run the following command:
    

```bash
tell me a joke
```

> NOTE: Do NOT expect the joke to be any good.

# What is ChromaDB?

ChromaDB is an open-source vector database for saving, and using, embeddings. Its main job is to store embeddings, with related information, for use by large language models. ChromaDB works well as a foundation for text-based search engines and is perfect for handling lots of unstructured and partly structured data.

## Creating the ChromaDB Environment.

* In a *second* terminal, I use `conda` to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (ChromaDB):
    

```bash
conda create -n ChromaDB python=3.11 -y && conda activate ChromaDB
```

> NOTE: This command creates the (ChromaDB) environment, then activates the (ChromaDB) environment.

## Setting Up the ChromaDB Home Directory.

> NOTE: I will define the home directory with settings in the environment directory.

* I create the ChromaDB home directory:
    

```bash
mkdir ~/ChromaDB
```

* I make new directories within the (ChromaDB) environment:
    

```bash
mkdir -p ~/miniconda3/envs/ChromaDB/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/ChromaDB/etc/conda/activate.d/set_working_directory.sh
```

* I add the following to the script, save the changes (CTRL + S), and exit (CTRL + X) the Nano text editor:
    

```bash
cd ~/ChromaDB
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (ChromaDB) environment:
    

```bash
conda activate ChromaDB
```

> NOTE: I should now be in the(ChromaDB) environment and the  
> `~/ChromaDB` home directory.

## Installing ChromaDB.

* I install ChromaDB:
    

```bash
pip install chromadb
```

## Running ChromaDB.

* I run ChromaDB:
    

```bash
chroma run
```

> NOTE: ChromaDB has created a `~/ChromaDB/chroma_data/chroma.sqlite3` file.

* I access ChromaDB, e.g.:
    

```bash
http://192.168.188.41:8000
```

> NOTE: The IP address above points to the PC that is running ChromaDB.

# What is Docker and Docker Desktop?

Docker is a tool for easily deploying, and running my applications on any platform. I can package an application with all its code, libraries, dependencies, and tools, which allows me to deploy that app as a single bundle. Docker guarantees that my application will run on any computer that also runs Docker.

Docker Desktop is a developer utility for my Mac, Linux, or Windows environments that let me build, share, and run containerized applications and deploy microservices solutions. It provides a straightforward GUI (Graphical User Interface) that lets me manage my applications, containers, and images directly.

## Installing Docker.

* In a *third* terminal, I install the following requirements:
    

```plaintext
sudo apt install -y ca-certificates curl gnupg lsb-release
```

* I make a `keyrings` directory:
    

```plaintext
mkdir -m 0755 -p /etc/apt/keyrings
```

* I add Docker’s official GPG key:
    

```plaintext
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

* I change the mode of the `docker.gpg` file:
    

```plaintext
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

* I install the Docker repository:
    

```plaintext
echo "deb [arch="$(dpkg --print-architecture)" \
  signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

* I update the repo list:
    

```plaintext
sudo apt update
```

* I use the APT package manager to install Docker CE (Community Edition), the CLI, the container daemon, the Build plugin, and the Docker Compose plugin:
    

```plaintext
sudo apt install -y \
docker-ce docker-ce-cli containerd.io \
docker-buildx-plugin docker-compose-plugin
```

## Checking the Docker Installation.

* I check if Docker is active:
    

```plaintext
systemctl is-active docker
```

* I check the status of Docker:
    

```plaintext
service docker status
```

* I check the Docker version:
    

```plaintext
sudo docker version
```

* I list the information for Docker:
    

```plaintext
sudo docker info
```

* I create the Docker group, if required:
    

```plaintext
sudo groupadd docker
```

## Setting the Docker Privileges.

* I create the Docker group, if required:
    

```plaintext
sudo groupadd docker
```

* I add my account to the Docker group:
    

```plaintext
sudo usermod -aG docker $USER
```

* I log in to the new Docker group (or reboot the container):
    

```plaintext
newgrp docker
```

* I verify the Docker installation by running this command without a `sudo` prefix:
    

```plaintext
docker run hello-world
```

> NOTE: This command displays 'Hello from Docker!' if Docker is properly installed.

## Downloading the Docker Desktop Install File.

* From a browser, I download the Docker Desktop `deb` file:
    

```bash
https://www.docker.com/products/docker-desktop/
```

> NOTE: By default, my browser downloads files to the Downloads directory.

## Installing Docker Desktop.

* From the *third* terminal, I change to the `Downloads` directory:
    

```bash
cd ~/Download
```

* I install Docker Desktop:
    

```bash
sudo apt install ./docker-desktop-<version>-<arch>.deb
```

> NOTE: I ignore the error message after `APT` completes the installation:  
> `N: Download is performed unsandboxed as root, as file '/home/user/Downloads/docker-desktop.deb' couldn't be accessed by user '_apt'. - pkgAcquire::Run (13: Permission denied)`

## Testing the Docker Desktop Installation.

* I launch Docker Desktop from the Applications menu, or I can run this command:
    

```bash
sudo systemctl --user start docker-desktop
```

* Within Docker Desktop, I enable it to start on boot @ "Settings &gt; General &gt; Start Docker Desktop when you sign in to your computer", or I can run this command:
    

```bash
systemctl --user enable docker-desktop
```

* Within Docker Desktop, I can stop it from the menu (select Quit Docker Desktop), or I can run this command:
    

```bash
systemctl --user stop docker-desktop
```

> NOTE: Also, Docker Desktop updates can be performed from within the utility.

## ALTERNATIVE: Running ChromaDB in Docker.

> NOTE: I do NOT run ChromaDB in Docker, but I have included this section for completeness.

* I pull the ChromaDB image from the Docker Hub:
    

```bash
docker pull chromadb/chroma
```

* I run ChromaDB on port 8000:
    

```bash
docker run -p 8000:8000 chromadb/chroma
```

* I access ChromaDB, e.g.:
    

```bash
http://host.docker.internal:8000
```

# What is AnythingLLM?

AnythingLLM is a free, easy-to-use, and versatile document chatbot. It is made for people who want to chat with, or create, a custom knowledge base using existing documents and websites. RAG (Retrieval-Augmented Generation) is the process of creating custom knowledge bases, which conveniently sidesteps the need for finetuning an LLM (Large Language Model) with LoRA (Low-Rank Adaptation) or QLoRA (Quantised LoRA). The information from the documents and websites are converted, and saved, to a vector database so an LLM can use this data to improve its answers my queries. AnythingLLM can work with many users, or just a single user, from one installation. This makes AnythingLLM great for those who want a ChatGPT experience, and complete privacy, while supporting multiple users in the same setup.

## Installing AnythingLLM.

* From the *third* terminal, I check if any containers are running on port 3001:
    

```bash
docker container ls
```

* I delete any containers running on port 3001:
    

```bash
docker rm -f <container-name>
```

> NOTE: It may take a few minutes for the container to be fully removed.

* I use (docker) to (run) a container, in (-d)etached mode, on (-p)ort 3001, with the (--name) of AnythingLLM, using the image (mintplexlabs/anythingllm):
    

```bash
docker run -d -p 3001:3001 --name AnythingLLM mintplexlabs/anythingllm
```

* I can use (docker) to (stop) the (AnythingLLM) container:
    

```bash
docker stop AnythingLLM
```

* I can use (docker) to (start) the (AnythingLLM) container:
    

```bash
docker start AnythingLLM
```

## Setting Up AnythingLLM.

The next post in this series will cover how [I setup, and use, AnythingLLM](https://solodev.app/2-of-2-setting-up-anythingllm-for-work) in a business situation. Subscribe below for more AnythingLLM goodness.

# The Results.

In this post, I've gone through the processes of installing and setting up AnythingLLM in Docker. I've delved into various tools such as Miniconda, Ollama, ChromaDB, and Docker, as well as their roles in my setup. I also touched on the unique features of AnythingLLM that make it stand out among other Retrieval-Augmented Generation solutions. In the next post, I explore how to effectively use AnythingLLM in a business setting.

# In Conclusion.

Do you love playing with the latest tech but shy away from Microsoft and Apple? This is how I installed AnythingLLM in Docker, right on my Ubuntu system, even though support for Linux is yet to be deployed!

AnythingLLM is a free, easy-to-use, and versatile document chatbot. The killer feature? It can scrape GitHub projects which is an amazing ability that separates it from other RAG (Retrieval-Augmented Generation) solutions.

As an Ubuntu user, I found it easy to deploy this tool. I also used utilities like Miniconda and Ollama. ChromaDB, an open-source vector database for saving and using embeddings, was another key player in this setup. And there is Docker, a tool for deploying and running applications on any platform. All of these programs were instrumental to installing AnythingLLM.

In [my next post](https://solodev.app/2-of-2-setting-up-anythingllm-for-work), I'll be diving into how I will use AnythingLLM in a business setting.

But for now, tell me, how are you leveraging AI in your business operations?

Until next time: Be safe, be kind, be awesome.

#AnythingLLM, #Docker, #Ubuntu, #Miniconda, #Ollama, #ChromaDB, #LLM, #RAG, #AI, #TechTutorial, #Linux, #OpenSource, #VectorDatabase, #LargeLanguageModel