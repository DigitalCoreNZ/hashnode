---
title: "Installing Langflow and Flowise."
datePublished: Mon May 06 2024 10:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clvusj82k00070amhbwyo69fk
slug: installing-langflow-and-flowise
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1714952656308/8a8b36fa-c02d-41dd-bb5e-a1be3cae95f3.png
tags: ai, artificial-intelligence, software-development, innovation, workflow-automation, tech-community, ai-integration, ai-applications, low-code-platforms, tech-tools, langflow, flowise

---

# TL;DR.

Installing Langflow and Flowise involves setting up an environment using Miniconda, installing Node.js via NVM, and creating the necessary directories and scripts. Langflow, a user-friendly interface for LangChain, allows easy AI application creation with minimal coding. Flowise, an open-source platform for building AI workflows, supports extensive integrations and operates in secure environments. Both tools are designed to streamline AI application development but cater to different needs: Langflow is used for rapid prototyping and Flowise is used for customizable workflows. The choice between these tools depends on specific requirements like ease of use, customization, and deployment scope.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗.***

# An Introduction.

Langflow and Flowise are are two AI tools that that serve different purposes. This means that using both tools expands my ability to create amazing AI experiences.

> The purpose of this post is to describe the installation of Langflow and Flowise.

# The Big Picture.

* Below is an image of the newly-installed Langflow UI:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714954167924/8fd22868-e8e7-439e-8c0c-951f5d906276.png align="center")

* Below is an image of the newly-installed Flowise UI:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714954182824/88ef16a1-f4c1-4ab4-891c-8fe6c5b3f9e7.png align="center")

Combined, these tools provide a wide range of options when developing AI solutions.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda),
    
* [LiteLLM](https://solodev.app/installing-litellm), and
    
* Flowise UI.
    

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

# What is Node.js, NPM, and NVM?

Node.js is a free, JavaScript (JS) server runtime. It runs JS code as single-threaded, non-blocking, asynchronous programs, which makes it very memory efficient. Node.js performs many system-level tasks, but is commonly used to run JS servers.

NPM (Node Package Manager) is the world's largest software registry. Open source developers use it to share packages with each other. Many organizations use NPM to manage private development as well. Most developers interact with NPM using the CLI (Command Line Interface), and usually ships with Node.js.

NVM (Node Version Manager) is used to switch between versions of Node.js. NVM works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash) and runs on Linux distros, macOS, and Windows WSL.

[https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)↗,

[https://docs.npmjs.com/about-npm](https://docs.npmjs.com/about-npm)↗,

[https://github.com/nvm-sh/nvm#intro](https://github.com/nvm-sh/nvm#intro)↗, and

[https://solodev.app/installing-node-and-npm-with-nvm](https://solodev.app/installing-node-and-npm-with-nvm).

Node.js must be installed (`node -v`) before continuing with this post.

## Installing Node and NPM with NVM.

* I open a terminal.
    
* I install CURL:
    

```plaintext
sudo apt install -y curl
```

* I install the NVM (Node Version Manager):
    

```plaintext
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

> NOTE: The version numbers are listed on the NVM GitHub page.

* I activate the NVM:
    

```plaintext
source ~/.bashrc
```

* I use the NVM to install the LTS version of Node.js:
    

```plaintext
nvm install --lts
```

> NOTE: The Node and NPM versions are listed on the screen.

* I make Node LTS the default NVM version, as listed in the previous command:
    

```plaintext
nvm alias default 20.12.2
```

* I confirm the Node installation:
    

```plaintext
node -v
```

* I confirm the NPM installation:
    

```plaintext
npm -v
```

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments while avoiding version conflicts.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the `conda` package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the `conda` package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/](http://www.anaconda.com/)***↗,***

[https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

I ensure [Miniconda is installed](https://solodev.app/installing-miniconda) (`conda -V`) before continuing with this post.

## Creating a Miniconda Environment.

* I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (Flow):
    

```bash
conda create -n Flow python=3.11 -y && conda activate Flow
```

> NOTE: This command creates the (Flow) environment, then activates the (Flow) environment.

## Creating the Flow Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the Flow home directory:
    

```bash
mkdir ~/Flow
```

* I make new directories within the (Flow) environment:
    

```bash
mkdir -p ~/miniconda3/envs/Flow/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/Flow/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Flow
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (Flow) environment:
    

```bash
conda activate Flow
```

> NOTE: I should now, by default, be in the `~/Flow` home directory.

# What is Langflow?

Langflow is a user-friendly interface for LangChain, built using react-flow. It lets me easily create, and test, different setups by dragging and dropping components and using a chat box. Each part of the graph in Langflow works on its own. It's designed to help me quickly try out new ideas and build AI applications without needing to write much code. Langflow comes with ready-to-use components that I can mix and match to build AI apps. It fits perfectly with the tools I already use and makes it simple to develop basic, or advanced, AI applications. Langflow is all about making AI integration straightforward and expanding what I can do with AI in both tests and real-life uses.

[https://docs.langflow.org/](https://docs.langflow.org/)***↗.***

## Installing Langflow.

* I use pip to install Langflow:
    

```plaintext
pip install langflow[local] -U --force-reinstall
```

* I run Langflow:
    

```plaintext
langflow run
```

* Langflow is accessed using a browser:
    

[http://localhost:7860/](http://localhost:7860/)

# What is Flowise?

Flowise is an open-source, low-code platform that helps me easily create customized AI workflows and agents. It simplifies the development of AI applications, which usually require many iterations, by allowing for quick changes from testing to production. Chatflows link AI models with various tools like memory, data loaders, and cache, along with over a hundred other integrations including LangChain and LlamaIndex. This setup enables the creation of autonomous agents and assistants that can perform diverse tasks using custom tools. I can build functional agents and OpenAI assistants, or opt for local AI models to save costs. Flowise supports extensions and integrations through APIs, SDKs, and embedded chat features. It is platform-agnostic, meaning Flowise can work with local, open-source AI models in secure, offline environments using local data storage. It is compatible with various platforms and technologies like Ollama, HuggingFace, AWS, Azure, and GCP, offering flexibility in deployment.

[https://docs.flowiseai.com/](https://docs.flowiseai.com/)***↗.***

## Installing Flowise.

* I open a new Terminal tab.
    
* I activate the Flow environment:
    

```plaintext
conda activate Flow
```

* I use NPM to install Flowise globally:
    

```plaintext
npm install -g flowise
```

* I use NPX to start Flowise:
    

```plaintext
npx flowise start
```

* Flowise is accessed using a browser:
    

[http://localhost:3000/](http://localhost:3000/)

# Differences are Good.

> NOTE: The differences between Langflow and Flowise results in broader, more diverse solutions.

## 1 of 3: Agent Differences.

| Langflow Agents | Flowise Agents |
| --- | --- |
| Auto GPT: A complete conversational agent built on the React framework, providing a wide range of language processing capabilities. | CSV Agent: Enables data retrieval and manipulation from CSV files. |
| Baby AGI: A pre-trained conversational agent designed for efficient language understanding and response generation. | JSON Agent: Facilitates JSON data extraction, transformation, and manipulation. |
| Conversational Agent: Allows users to define conversational flows and logic to create interactive conversations. | SQL Agent: Interacts with databases using SQL queries to retrieve and update data. |
| LLM (Language Model Memory) Agent: Incorporates memory and context to enable more context-aware language processing. | Vector Store Router: Provides a routing mechanism for directing requests to different vector stores based on predefined rules. |

## 2 of 3: Chain Differences.

| **Langflow Chains** | **Flowise Chains** |
| --- | --- |
| Conversation Chain: Facilitates multi-turn conversations and supports complex dialogue flows. | Conversation Chain: Enables seamless conversations with users, supporting back-and-forth interactions. |
| Retrieval QA Chain: Allows retrieval-based question-answering capabilities using predefined responses. | Retrieval QA Chain: Retrieves answers to user queries from predefined knowledge bases. |
| LLM Chain: Utilizes Language Model Memory to enhance language understanding and generate context-aware responses. | SQL Database Chain: Integrates SQL databases for data retrieval and manipulation. |
| Maths Chain: Provides mathematical computation capabilities within language processing pipelines. | Vector DB Chain: Accesses and manipulates data stored in vector databases. |

## 3 of 3: Tooling Differences.

| Langflow Tools | Flowise Tools |
| --- | --- |
| Text Splitters: Splits text into meaningful units for further processing or analysis. | Wrappers: Offers a text request wrapper, allowing seamless integration with external request libraries. |
| Embeddings: Generates vector representations of text for various natural language processing tasks. | Vector Stores: Manages and organizes vector representations of data for efficient retrieval and comparison. |
| LMS (Language Model Store): Stores and manages pre-trained language models for efficient access and utilization. | Metadata Filter: Filters data based on specific metadata criteria, enabling efficient data processing and retrieval. |
| Prompts: Provides pre-defined prompts to initiate and guide user interactions. |  |

## Further Details.

Please visit the excellent post from [Apoorva Gosain](https://hybrowlabs.com/blog/author/Apoorva) to discover more details about Langflow and Flowise:

> **Attributions:**
> 
> [https://hybrowlabs.com/blog/langflow-vs-flowise-the-ultimate-showdown-for-streamlined-language-processing](https://hybrowlabs.com/blog/langflow-vs-flowise-the-ultimate-showdown-for-streamlined-language-processing)

# The Results.

The exploration of Langflow and Flowise offers a revealing look into the capabilities and distinctions of modern AI tools designed for language processing and workflow automation. While Langflow focuses on ease of use and modular integration for rapid prototyping of AI applications, Flowise caters more to creating customizable AI workflows with a robust set of features for scalability and integration across different platforms. Both tools demonstrate their unique strengths, making them valuable depending on my specific needs and technical environments. Ultimately, the choice between Langflow and Flowise should be guided by the my specific requirements in terms of ease of use, customization, and the scope of deployment. This comparison not only highlights the individual features of each tool but also underscores the broad spectrum of possibilities that AI-driven platforms offer to innovators and developers in the tech industry.

# In Conclusion.

As an AI enthusiast and developer, I am *always* looking to streamline my AI application development with powerful tools. Let's dive into the capabilities of Langflow and Flowise, two cutting-edge platforms that are transforming the landscape of AI-driven applications.

Langflow is a user-friendly interface built on react-flow, perfect for creating and testing AI setups with minimal coding. It is designed to integrate seamlessly into my existing toolkit, enhancing my ability to develop simple, or complex, AI applications.

Flowise, on the other hand, is an open-source, low-code platform that simplifies the creation of customized AI workflows. It supports numerous integrations and can operate in secure, offline environments, making it incredibly flexible for different deployment scenarios.

Both platforms offer unique features:

* Langflow focuses on ease of use and rapid prototyping.
    
* Flowise excels in creating customizable workflows with extensive features for scalability.
    

As a startup looking to innovate, or a large enterprise aiming to enhance my AI capabilities, these tools provide substantial value.

For a deeper comparison and more insights, check out the full article here: \[Link to the full article\]

What has been your experience with AI tools in your projects? Have you tried Langflow or Flowise yet? Let's discuss in the comments below!

Until next time: Be safe, be kind, be awesome.

#Langflow #Flowise #AI #ArtificialIntelligence

#AIIntegration #AIApplications #LowCodePlatforms

#WorkflowAutomation #Innovation #SoftwareDevelopment

#TechCommunity #TechTools