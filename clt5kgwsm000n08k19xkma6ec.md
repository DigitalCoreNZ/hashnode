---
title: "2 of 2: Setting Up AnythingLLM for Work."
datePublished: Wed Feb 28 2024 09:00:45 GMT+0000 (Coordinated Universal Time)
cuid: clt5kgwsm000n08k19xkma6ec
slug: 2-of-2-setting-up-anythingllm-for-work
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708935846561/e21494b8-6673-4d1e-87bd-dd22b1638031.png
tags: ai, chatbot, knowledge-base, chatgpt, systems-analyst, ai-chatbot, anythingllm, document-chatbot, personalized-chatbot, workspace-customization

---

# TL;DR.

This post details the setup process for AnythingLLM, a versatile document chatbot. It is a guide through updating the system, starting services like Llama 2 and ChromaDB, and running AnythingLLM. It also explains how to prepare, customize, and add documents to AnythingLLM workspaces, using a Systems Analyst Workspace as an example. This post highlights the potential of AnythingLLM to provide a personalized ChatGPT experience with complete privacy.

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

In [my last post](https://solodev.app/1-of-2-installing-anythingllm-for-linux), I described how to install a Dockerized instance of AnythingLLM. This time, I show how to set it up as a private, specialised LLM experience.

> The purpose of this post is to show how to set up AnythingLLM for custom results.

# The Big Picture.

AnythingLLM runs natively on Windows and macOS. Although a Linux deployment is still to emerge, that didn't stop me (mostly because the developers created a Dockerized version) from exploring how to install it on an Ubuntu system. Now that AnythingLLM is installed, I will show how to set it up as a powerful, personal assistant.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda),
    
* [AnythingLLM](https://solodev.app/1-of-2-installing-anythingllm-for-linux).
    

# Updating the System.

* I update my system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# Starting the Services.

In [my previous post](https://solodev.app/1-of-2-installing-anythingllm-for-linux), I spent time setting up the following services. Now I can start these services whenever its time to get work.

## Starting Llama 2.

In the *first* terminal, I activate the Ollama environment:

```bash
conda activate Ollama
```

* I run Llama 2:
    

```bash
ollama run llama2
```

* I can now access Llama 2 through port 11434, e.g.:
    

```bash
http://192.168.188.41:11434
```

> NOTE: The IP address above points to the PC that is running ChromaDB.

## Starting ChromaDB.

* In the *second* terminal, I activate the ChromaDB environment:
    

```bash
conda activate ChromaDB
```

* I run ChromaDB:
    

```bash
chroma run
```

> NOTE: ChromaDB saves data to the `~/ChromaDB/chroma_data/chroma.sqlite3` file.

* I can now access ChromaDB through port 8000, e.g.:
    

```bash
http://192.168.188.41:8000
```

> NOTE: The IP address above points to the PC that is running ChromaDB.

## Starting AnythingLLM.

> NOTE: At this stage:
> 
> * Ollama is running Llama2 in the Ollama environment, and
>     
> * ChromaDB is running in the Chroma environment.
>     
> 
> Both environments are provided by the Miniconda package manager , conda, and are running in separate terminals.

* From the *third* terminal, I check if any containers are running on port 3001:
    

```bash
docker container ls
```

* I delete any containers running on port 3001:
    

```bash
docker rm -f <container-name>
```

* I run AnythingLLM:
    

```bash
docker start AnythingLLM
```

# What is AnythingLLM?

AnythingLLM is a free, easy-to-use, and versatile document chatbot. It is made for people who want to chat with, or create, a custom knowledge base using existing documents and websites. RAG (Retrieval-Augmented Generation) is the process of creating custom knowledge bases, which conveniently sidesteps the need for finetuning an LLM (Large Language Model) with LoRA (Low-Rank Adaptation) or QLoRA (Quantised LoRA). The information from the documents and websites are converted, and saved, to a vector database so an LLM can use this data to improve its answers my queries. AnythingLLM can work with many users, or just a single user, from one installation. This makes AnythingLLM great for those who want a ChatGPT experience, and complete privacy, while supporting multiple users in the same setup.

## Preparing AnythingLLM.

* I open AnythingLLM in a browser:
    

```bash
http://localhost:3001
```

* On the "Welcome to AnythingLLM" screen, I click the "Get started" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708850459900/9cbe5289-e9a3-4de2-b1f7-74be169137ce.png align="center")

* On the "LLM Preference" screen, I select "Ollama", specify the "Ollama Base URL", and set the "Token context window":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708851102420/30b55b8b-6cff-4741-9648-937e223031ad.png align="center")

> NOTE: The "Chat Model Selection" chooses the Llama2 model by default.

* On the "Embedding Preference" screen, I select the default "AnythingLLM Embedder":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708851141214/3fa476e4-2aa9-4074-80b9-589cdc7a9575.png align="center")

* On the "Vector Database Connection" screen, I select "Chroma" and set the "Chroma Endpoint":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708851375895/0c5beccf-c6ab-420f-ac48-14c810452383.png align="center")

* On the "Custom Logo" screen, I leave the "AnythingLLM" logo:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708851525667/28fd14dc-d8bb-4821-8c5f-25681d653e43.png align="center")

* On the "User Setup" screen, I click the "Just me" button and set a password:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708851890366/2c32135b-67f2-4b73-9da1-226aa1126d88.png align="center")

* On the "Data Handling & Privacy" screen, I check my chosen settings:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708852038242/51b94913-2b1f-4f9b-b985-dcd601bac288.png align="center")

* On the "Welcome to AnythingLLM" screen, I complete the survey:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708852174687/71556dd0-5117-49d6-b471-3551f80ea6b0.png align="center")

* In the "New Workspace" modal window, I call my first workspace "Systems Analyst":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708852975675/09257cb3-c7f9-430a-943f-8e1c4d05c4cb.png align="center")

## Tuning the Systems Analyst Workspace.

* I ask the following: What is the average salary for a systems analyst in the United States?
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708858423655/6bdf370d-c6c9-42ef-a956-f6560f504833.png align="center")

* In the left pane, I click the gear icon next to "Systems Analyst":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708856209098/4ad96ff8-3af7-4598-aeea-6967faf6030d.png align="center")

> NOTE: Along the top of the General Appearance Settings are 3 tabs: General Settings, Chat Settings, and Vector Database.

* In the Vector Database tab, I change the "Document similarity threshold" from low to high and click the "Update workspace" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708856595994/4acaffc2-51cf-4f22-9c5d-152fc473dd46.png align="center")

* I click the return button (to the left of the tabs) and, on the main screen, I ask the same question again:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708858743207/483eab10-9c7c-4a8b-ae96-989a74c78fe8.png align="center")

> NOTE: The answer is essentially the same as last time.

* I click the gear icon again, click the "Chat Settings" tab, change the "Chat mode" from "Chat" to "Query", click to "Update workspace" button at the bottom of the screen, and return to the main screen:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708857264226/ddfe5bff-886c-4f6b-8a71-29dbf0f6dba0.png align="center")

* I ask the same question for a third time:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708858845490/baea6dd5-8dd4-4727-aaf8-b216a4ccb1a3.png align="center")

> NOTE: Query mode only works if there are documents available.

## Adding Documents to the Systems Analyst Workspace.

* In the left pane, I click the upload icon next to "Systems Analyst" (to the left of the gear icon):
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708854457027/caf18482-9a63-4d97-9dee-d2a78af22fd2.png align="center")

* At the bottom of the modal window, I add a URL and click the "Fetch website" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708854705312/54298462-f15f-4421-b994-4b10aca130d2.png align="center")

* In the "My Documents" panel, I select the new file and click the "Move 1 file to workspace" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708854868587/2ed4bee2-e97c-4357-8e06-6e6b36656c56.png align="center")

* Under the "Systems Analyst" panel, I click the "Save and Embed" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708854998620/f8cbdf8a-9492-4db7-964d-87f966f3c81e.png align="center")

* After the Workspace is updated, I close the modal window:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708855050419/c740e45f-c40c-47bf-a752-5168951f482c.png align="center")

* Back at the main screen, I ask the same question a 4th time:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708859102411/765df430-b0a1-4404-8671-3c7da6420fcc.png align="center")

> NOTE: Although still in Query mode, Llama 2 provided an answer and included a citation from the added website.

## Adding a Systems Prompt to the Systems Analyst Workspace.

* I click the gear icon, then I click the "Chat Settings" tab:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708860284833/2cb8e883-441e-4012-b479-f572280ca176.png align="center")

* In the "Prompt" field is the following:
    

```plaintext
Given the following conversation, relevant context, and a
follow up question, reply with an answer to the current
question the user is asking. Return only your response to
the question given the above information following the users
instructions as needed.
```

* The "Prompt" field is where I describe the "Systems Analyst" role:
    

```plaintext
Yoy are a systems analyst. Your skill is the ability to translate
business domain problems into technology domain problems. You will
provide the systems architect with the information she needs to
frame the technology problems for others to understand.
```

The Systems Analyst Workspace, when combined with quality documentation, will become a powerful point of contact where business entities can engage with our services.

## Other Workspaces.

A Systems Analyst Workspace is just the beginning. There is other roles that need filling, too. Workspaces are a great way to delineate these roles, ensuring they each have access to quality, role-specific documents and defined by finely tuned prompts.

## The Next Step.

When the Linux version of AnythingLLM is released, the first thing I'm going to do is dive into the APIs. Yes, I can start the ball rolling with the native Windows installation, but... Wait, I *should* start with the Windows installation!

Right, I've reached the end of this post.

'Bye.

# The Results.

In this post, I've walked through the process of setting up AnythingLLM, a versatile document chatbot that can be tailored to specific use-cases and workspaces. I've explored how to start services, prepare the system, and customize workspaces according to specific roles like a Systems Analyst. I also showed how AnythingLLM can enhance its responses by using documents and websites to build a custom knowledge base. The ability to add documents to workspaces and fine-tune settings allows for a highly customized and efficient workflow. As I anticipate the Linux version of AnythingLLM, I can see the vast possibilities that this tool offers for creating interactive, personalized, and private ChatGPT experiences.

# In Conclusion.

Have you ever dreamed of having a personalized AI-powered chatbot that can adapt to your specific needs? Let me introduce you to AnythingLLM. It is a free, versatile document chatbot that I can tailor with custom knowledge bases using documents and websites. It's like having a personalized ChatGPT experience that offers complete privacy.

Recently, I've set up AnythingLLM and let me tell you, the process is seamless. I can start services, prepare the system, and customize workspaces for specific roles like a Systems Analyst. AnythingLLM can enhance its responses by using documents and websites to build a custom knowledge base. Imagine the efficiency of having a tool that learns from the documents I provide! The ability to add documents to workspaces and fine-tune settings allows for a highly customized workflow, making it a game-changer for those who need an interactive, personalized, and private ChatGPT experience. As I await the Linux version of AnythingLLM, I can only imagine the vast possibilities that this tool offers.

Who else is excited about the potential of AI-powered chatbots like AnythingLLM? How would you use a personalized document chatbot in your workflow? Let's discuss!

Until next time: Be safe, be kind, be awesome.

#AnythingLLM, #Chatbot, #DocumentChatbot, #ChatGPT, #PersonalizedChatbot, #AI, #WorkspaceCustomization, #SystemsAnalyst, #KnowledgeBase, #AIChatbot