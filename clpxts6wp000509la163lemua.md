---
title: "Installing Ollama."
datePublished: Sat Dec 09 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpxts6wp000509la163lemua
slug: installing-ollama
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703975053907/4415f003-b120-40f4-becd-28cb06b1fb6a.png
tags: ai, artificial-intelligence, ubuntu, linux, development, machine-learning, research, deep-learning, llm, large-language-models, tech-blog, ollama, local-llm, mistral-model, ai-installation

---

Update: Saturday 12<sup>th</sup> December 2023.  
Update: Sunday 31<sup>st</sup> December 2023 (yes, I'm working on New Year's Eve.)  
Update: Tuesday 20<sup>th</sup> February 2024.  
Update: Sunday 10<sup>th</sup> March 2024.  
Update: Wednesday 19<sup>th</sup> June, 2024 (installing in the (base) environment.)

---

# TL;DR.

This post describes the installation of Ollama, a local large language model (LLM) manager. It requires a Linux-based distro and Miniconda. I install Ollama into my (base) environment. It is used to download, and run, LLMs. In this case, I use the Mistral model as an example. Ollama enables the use of powerful LLMs for research, development, business (if the license allows), and personal use.

> ***Attributions:***
> 
> [Ollama.ai](https://ollama.ai/)↗.

.

> NOTE: After extensive use, I have decided that Ollama should be installed in the (base) environment. This installation process reflects my opinion.

---

# An Introduction.

LLMs (large language models) are amazing machines. They are the bleeding edge of modern technology and devs should learn, and adapt to, these awesome engines.

> The purpose of this post is to describe how to install Ollama, a local LLM manager.

---

# The Big Picture.

There are many open-source LLMs. Ollama provides easy access to a large, popular set of these models. Visit the [Ollama models library](https://ollama.ai/library) to get a full list of the LLMs they support. The index is continually updated, so I frequently revisit this archive.

I love Hugging Face, but it's *also* nice to have a curated series of models.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

# Updating my Base System.

* From the (base) terminal, I update my base system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

---

# What is Ollama?

Ollama is a tool that is used to download, set up, and run large language models on a local PC. It lets me use powerful models like Llama 2 and Mistral on my personal computer. Ollama natively runs on Linux, macOS, and Windows (in preview).

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

## Using Ollama to Run the Mistral Model.

* I run the Mistral model:
    

```python
ollama run mistral
```

> NOTE 1: The `ollama run` command performs an `ollama pull` if the model has not already been downloaded to my local system.

> NOTE 2: The `ollama run` command is used to run the named LLM.

> NOTE 3: I sometimes need to restart my terminal or system to run the LLM.

## Testing the Mistral Model.

* At the `>>>` prompt, I run the following command:
    

```python
tell me a joke
```

> NOTE: Do NOT expect the joke to be funny. Prepare to be underwhelmed.

---

# Ollama Commands.

| `ollama serve` | Starts the Ollama server to manage models. |
| --- | --- |
| `ollama run <model>` | Runs a specified model, downloading it if not already present. |
| `ollama pull <model>` | Downloads a model from the Ollama library without running it. |
| `ollama list` | Lists all installed models on your system. |
| `ollama rm <model>` | Removes a specific model from your system. |
| `ollama ps` | Shows currently running models and their resource usage. |
| `ollama show <model>` | Displays metadata and details about a specific model. |
| `ollama create <model>` | Creates a new model from an existing one for customization. |

---

# The Results.

By following the steps outlined in this post, I can install Ollama, download LLMs from [Ollama.ai](https://ollama.ai/), and run these models locally. This process enables me to evaluate the power of cutting-edge models for research, development, business, and personal use.

> NOTE: Commercial use depends on the license of each model.

---

# In Conclusion.

LLMs are the bleeding edge of modern technology and I should adopt these awesome engines.

I've been exploring Ollama, a local LLM manager that provides easy access to a selection of open-source LLMs from [Ollama.ai](https://ollama.ai). Their list of supported LLMs is continually updated. It's a buffet of cutting-edge tech that keeps on growing!

The installation process was straightforward because all I needed was a Linux-based distro. I created and activated a new environment named (Ollama) using the `conda` command. I installed Ollama in my (base) environment, downloaded an LLM, and ran that model (which, in this case, was 'Mistral'.)

By following these steps, I have set up and installed Ollama, downloaded an LLM from [Ollama.ai](http://Ollama.ai), and ran the model locally.

This is a game-changer for research, development, business (if the license for the model allows), and personal use. Future Tech is here and it's time to embrace it.

Have you used Ollama? What has been your experience? Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

---

#Ollama #LLM #LocalLLM #LargeLanguageModels

#AI #ArtificialIntelligence #MachineLearning #DeepLearning

#Ubuntu #Linux #MistralModel #TechBlog #Research

#Development #AIInstallation #TechTutorial #OpenSource

#FutureTech #AICommunity