---
title: "Bolt.diy and Ollama on Ubuntu 24.04 LTS."
datePublished: Mon Dec 30 2024 09:00:24 GMT+0000 (Coordinated Universal Time)
cuid: cm5at748f00170ajscd5cevw6
slug: boltdiy-and-ollama-on-ubuntu-2404-lts
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1739828225418/1b457073-70e3-414c-bdcd-441ff5d43c2a.png
tags: ai, productivity, web-development, coding, innovation, tech-trends

---

# TL;DR.

Local code generation using the [Bolt.diy](https://bolt.diy) agent and Ollama enables efficient development of full-stack applications directly from within a browser. By utilizing local LLMs, I can streamline workflows, enhance productivity, and maintain control over my development environment. This approach simplifies building and deploying applications while providing access to advanced models and technologies, shaping the future of web development.

> **Attributions:**
> 
> [https://github.com/stackblitz-labs/bolt.diy](https://github.com/stackblitz-labs/bolt.diy) ***↗.***

---

# An Introduction.

[Bolt.diy](https://Bolt.diy) and [Ollama](https://ollama.com) are two groundbreaking solutions that empower developers to create full-stack applications directly from our browsers. By leveraging local large language models (LLMs), these tools offer a seamless and efficient development experience. Discover how these tools can transform our workflow and keep us at the forefront of technological advancements.

> he purpose of this post is to describe how I install [Bolt.diy](http://Bolt.diy) on my local system.

---

# The Big Picture.

I want to highlight how [Bolt.diy](http://Bolt.diy) and is transforming web development by enabling developers to efficiently build full-stack applications, from our browsers, using local large language models. The Big Picture is to show how streamlining our workflows enhances productivity while we also maintain control over our development environments.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* PNPM,
    
* Ollama,
    
* and Git.
    

The [installation instructions](https://solodev.app/apps-utilities-for-ubuntu-2404-lts) are available for these prerequisites.

> NOTE: Docker, NodeJS, and NPM are needed

---

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

---

# What is PNPM?

[PNPM](https://pnpm.io/) ↗ (Performant Node Package Manager) is a JavaScript package manager, similar to NPM.

---

# What is Ollama?

[**Ollama**](https://ollama.com/) ↗ is a tool for downloading, setting up, and running LLMs (large language models). It lets me access powerful models like Llama and Qwen, and helps me run them on my local Linux, macOS, and Windows systems.

---

# What is Git?

Git is a version control manager that tracks any changes that are made to the files in a directory and subdirectories.

---

# What is Bolt?

[**Bolt**](https://github.com/stackblitz-labs/bolt.diy) ↗ is a web development agent that allows me to prompt, run, edit, and deploy full-stack applications directly from my browser.

---

# Downloading the Models.

* From the terminal, I use Ollama to pull the DeepSeek Coder V2 16b model:
    

```bash
ollama pull deepseek-coder-v2
```

* I use Ollama to pull the Quen 2.5 Coder 14b model:
    

```bash
ollama pull qwen2.5-coder:14b
```

* I use Ollama to pull the Quen 2.5 Coder 7b model:
    

```bash
ollama pull qwen2.5-coder:7b
```

* I use Ollama to list the models:
    

```bash
ollama list
```

---

# Installing the Bolt Agent.

* From the terminal, I check to see if `/usr/local/bin` is in my $PATH:
    

```bash
echo $PATH .
```

* I change to my home directory:
    

```bash
cd ~
```

* I clone the Bolt repository:
    

```bash
git clone https://github.com/stackblitz-labs/bolt.diy.git
```

* I change to the Bolt directory:
    

```bash
cd bolt.diy
```

## Editing the Environment File.

* I rename `.env.example` to `.env.local` (using the move command):
    

```bash
mv .env.example .env.local
```

> NOTE: Ollama runs locally and doesn't need an API key.

* I open the `.env.local` file in the Nano text editor:
    

```bash
sudo nano .env.local
```

* I set the Ollama API base URL:
    

```bash
OLLAMA_API_BASE_URL=http://localhost:11434
```

* I set the context length for the model being used:
    

```bash
DEFAULT_NUM_CTX=8192
```

* I save (CTRL + S) the changes and exit (CTRL + X) the Nano text editor.
    

---

# Running the Bolt Agent.

* From the terminal, I install PNPM (if required):
    

```bash
sudo npm install -g pnpm
```

* I install the dependencies:
    

```bash
pnpm install
```

* I start the Bolt agent:
    

```bash
pnpm run dev
```

* I open the interface in a browser:
    

```bash
http://localhost:5173/
```

> After the Bolt agent starts, there may be an error message. Simply refresh the page.

---

# The Results.

Local code generation using Bolt.diy and Ollama offers a powerful and efficient way to develop full-stack applications directly from my browser. By leveraging AI-powered tools and local LLMs, I can streamline my workflow, enhance productivity, and maintain control over my development environment. This approach not only simplifies the process of building and deploying applications but also ensures that I have access to cutting-edge models and technologies. As the landscape of web development continues to evolve, tools like Bolt.diy and Ollama will play crucial roles in shaping the future of coding and application development.

---

# In Conclusion.

Am I ready to revolutionize my web development process? Yes!! I want to discover how local code generation with Bolt.diy and Ollama can transform my workflow!

I can easily imagine developing full-stack applications directly from my browser, powered by AI and local LLMs. With Bolt.diy, I can prompt, run, edit, and deploy applications seamlessly, while Ollama ensures I have access to cutting-edge models like DeepSeek Coder V2 and Qwen 2.5 on my local system.

Here's what I need to get started: a Debian-based Linux distro, Git, Ollama, and PNPM. Once set up, I can pull powerful models and integrate them with the Bolt.diy agent for an efficient development experience.

By leveraging these tools, I can streamline my workflow, enhance productivity, and maintain control over my development environment. This approach not only simplifies building and deploying applications but also keeps me at the forefront of web development technology.

As the landscape of web development evolves, tools like Bolt.diy and Ollama are shaping the future of coding and application development.

Are you ready to take your app development process to the next level? How do you see AI-powered tools impacting your workflow? Let me know in the comments below.

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#WebDevelopment #AI #Coding #Productivity #Innovation #TechTrends