---
title: "Using Flowise with Local LLMs."
datePublished: Sun May 12 2024 10:00:15 GMT+0000 (Coordinated Universal Time)
cuid: clw3d6g1r00060aml3z2d5ah5
slug: using-flowise-with-local-llms
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715493896351/eaa7c848-d5ec-4d8d-99d9-8a6191e7ea6f.png
tags: ai, machine-learning, chatbots, ai-development, data-privacy, operational-security, ai-applications, tech-innovation, flowise, ai-workflow, local-llms

---

# TL;DR.

Using Flowise, with local LLMs like Ollama, allows for the creation of cost-effective, secure, and highly customizable AI-powered applications. Flowise provides a versatile environment that supports the integration of various tools and components, enhancing AI workflows and enabling the development of local chatbots and AI agents. This setup offers benefits in terms of data privacy and operational security, making it ideal for both business and personal AI projects.

> **Attributions:**
> 
> A YouTube video produced by [Leon van Zyl](https://www.youtube.com/@leonvanzyl)***↗:***
> 
> [https://www.youtube.com/watch?v=85gZ7G-ze3c](https://www.youtube.com/watch?v=85gZ7G-ze3c)***↗.***

---

# An Introduction.

Low-code GUI solutions like Flowise allows developers to focus on the big picture while maintaining an eye on the details:

> The purpose of this post is to demonstrate how to build Chatflows.

---

# The Big Picture.

This post is a continuation of the [Langflow and Flowise installation](https://solodev.app/installing-langflow-and-flowise) post.

Flowise is an excellent low-code GUI for creating AI workflows and agents. It simplifies the use of LangChain and LlamaIndex solutions. LangChain is a Python library that makes it easier to develop, produce, and deploy applications using large language models (LLMs). It offers open-source components, integrations, and tools for different purposes, like question answering, chatbots, and more.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda),
    
* [Ollama](https://solodev.app/installing-ollama),
    
* [An LLM](https://ollama.com/library)***↗***,
    
* [NPM](https://solodev.app/installing-node-and-npm-with-nvm), and
    
* [Flowise UI](https://solodev.app/installing-langflow-and-flowise).
    

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

# What is Flowise?

Flowise is an open-source, low-code platform that helps me easily create customized AI workflows and agents. It simplifies the development of AI applications, which usually require many iterations, by allowing for quick changes from testing to production. Chatflows link AI models with various tools like memory, data loaders, and cache, along with over a hundred other integrations including LangChain and LlamaIndex. This setup enables the creation of autonomous agents and assistants that can perform diverse tasks using custom tools. I can build functional agents and OpenAI assistants, or opt for local AI models to save costs. Flowise supports extensions and integrations through APIs, SDKs, and embedded chat features. It is platform-agnostic, meaning Flowise can work with local, open-source AI models in secure, offline environments using local data storage. It is compatible with various platforms and technologies like Ollama, HuggingFace, AWS (Amazon Web Services), Azure, and GCP (Google Cloud Platform), offering flexibility in deployment.

[https://docs.flowiseai.com/](https://docs.flowiseai.com/)***↗.***

---

# Running the Flowise UI.

* From the Terminal, I activate the Flow environment:
    

```plaintext
conda activate Flow
```

* I run Flowise:
    

```plaintext
npx flowise start
```

* I open the Flowise UI in the browser:
    

[http://localhost:3000](http://localhost:3000)

---

# Example 1: Local Chatbot.

* I click `Chatflows` button in the Main Menu, found on the left of the Flowise UI:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715395278560/0be56ec8-05b3-4998-b39f-a00a47b32d3e.png align="center")

* At the top-right of the UI, I click the blue `+ Add New` button.
    
* At the top-right of the `Untitled chatflow` canvas, I click the Save (💾) button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715395791483/c50dfcba-0c97-417a-96dd-3d889c866558.png align="center")

* I name the canvas `Local Chatbot` and and click the blue `Save` button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715396024907/1aef3462-eb94-4c51-a2e5-e6d001f4a592.png align="left")

> NOTE: On the left of the UI is a round, blue button with a plus symbol (+). This is the `Add Nodes` button. Clicking the `Add Nodes` button causes the blue button to change to a minus symbol (-) and a drop-down menu to display. Clicking the blue minus symbol (-) closes the drop-down menu. Within the drop-down menu are closed sub-menus (˅) that twirl open (˄) when clicked. Click an open sub-menu to close it again. The convention is to follow the path (&gt;) to a node. All paths start with `Add Nodes >` and end with nodes being dragged onto the current canvas.

* I drag the `Add Nodes > Chains > Conversation Chain` onto the `Local Chatbot` canvas:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715396617275/60afd350-98c6-46e7-9339-b97bf6f4efe5.png align="left")

* I drag the `Add Nodes > Chat Models > ChatOllama` node onto the canvas.
    
* In the `ChatOllama` node, I I define the following settings:
    

| Setting | Value |
| --- | --- |
| Base URL \* | http://localhost:11434 |
| Model Name \* | codellama:13b-instruct |
| Temperature | 0.7 |

* I connect the `ChatOllama` Output to the `Chat Model *` Input of the `Conversation Chain` by clicking-and-dragging a connector from one node to the other node:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715404997726/0128a40a-68b0-41ab-88de-66556bb2a44b.png align="center")

* I drag the `Add Nodes > Memory > Buffer Memory` onto the canvas.
    
* I connect the `Buffer Memory` Output to the `Memory *` Input of the `Conversation Chain`:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715404821620/d9986482-3ae0-441b-8378-19d11bf7aa80.png align="center")

* I save the changes to the `Local Chatbot`.
    
* On the right of the UI, I click the round, purple Chat icon to send the "Tell me a joke" message to the LLM:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715404566968/81bd8c02-8e78-4891-80c3-9a83f23788b3.png align="center")

* At the top-left of the UI, I click the left-pointing arrow to return to the Main Menu.
    

---

# Example 2: Local RAG Chatbot.

* From the Main Menu ( on the left of the UI), I click `Chatflows`.
    
* In the `Untitled chatflow` canvas, I click the `Save` button (that looks like a floppy disk.)
    
* I rename the canvas `Local RAG Chatbot`.
    

> NOTE: Remember, the `Add Nodes` button on the left is round, blue, and has a (+) symbol.

* I drag the `Add Nodes > Chains > Conversational Retrieval QA Chain` node to the canvas.
    
* I drag the `Add Nodes > Chat Models > ChatOllama` node to the canvas.
    
* I connect the `ChatOllama` node Output to the `Conversational Retrieval QA Chain` node `Chat Model` Input.
    
* In the `ChatOllama` node, I define the following settings:
    

| Setting | Value |
| --- | --- |
| Base URL \* | http://localhost:11434 |
| Model Name \* | codellama:13b-instruct |
| Temperature | 0.4 |

* I drag the `Add Nodes > Vector Stores > In-Memory Vector Store` node to the canvas.
    
* I connect the `In-Memory Vector Store` node Output to the `Conversational Retrieval QA Chain` node `Vector Store Retriever` Input.
    
* I drag the `Add Nodes > Embeddings > Ollama Embeddings` node to the canvas.
    
* I connect the `Ollama Embeddings` node Output to the `In-Memory Vector Store` node `Embeddings` Input.
    
* In the `Ollama Embeddings` node, I define the following settings:
    

| Setting | Value |
| --- | --- |
| Base URL \* | http://localhost:11434 |
| Model Name \* | codellama:13b-instruct |
| Additional Parameters | Number of GPU: 1 |
| Use MMap: On |  |

* I drag the `Add Nodes > Document Loaders > Cheerio Web Scraper` node to the canvas.
    
* I connect the `Cheerio Web Scraper` Output to the `In-Memory Vector Store` node `Document` Input.
    
* In the `Cheerio Web Scraper` node, I define the following settings:
    

| Setting | Value |
| --- | --- |
| URL \* | https://www.langchain.com/langsmith |

* I save the changes to the `Local RAG Chatbot`.
    
* I insert data from the `Cheerio Web Scraper` into the `In-Memory Vector Store` by clicking the green DB button at the top-right of the screen.
    
* Once completed, I can chat with the results, e.g. "What is LangSmith?"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715472743496/7720bce9-3874-4308-8ad4-6929d2c52cca.png align="center")

---

# The Results.

Using Flowise with local LLMs offers a robust and flexible environment for developing advanced, AI-powered applications. By integrating tools like Ollama, and various Flowise components, I can create efficient, cost-effective, local chatbots and AI agents capable of performing a wide range of tasks. This setup enhances data privacy, operational security, and allows for extensive customization to meet specific needs. Whether for business processes, customer service, or personal projects, the ability to build and manage local AI models with Flowise opens up new possibilities for innovation and efficiency in AI application development.

---

# In Conclusion.

I discovered how Flowise can transform my AI development process and revolutionize my AI workflows with local LLMs.

In today's tech-driven world, efficiency and customization in AI are crucial. That's why I'm excited to share my journey using Flowise with local LLMs, a robust platform that simplifies the creation of AI-powered applications.

With Flowise, I've built powerful local chatbots and AI agents that are not only cost-effective but also prioritize data privacy and operational security. This setup is perfect for businesses and individual developers looking to innovate, while also maintaining control over their data.

From integrating tools like Ollama to utilizing components like Chatflows and Memory Buffers, Flowise has allowed me to seamlessly transition from testing to production, ensuring my AI solutions are both dynamic and scalable.

Have you considered using local LLMs for your AI projects? What has been your biggest challenge in AI development?

---

Until next time: Be safe, be kind, be awesome.

---

#Flowise #AI #AIdevelopment #AIWorkflow #AIApplications #LocalLLMs #Chatbots #MachineLearning #TechInnovation #DataPrivacy #OperationalSecurity