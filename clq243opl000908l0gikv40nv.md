---
title: "Local Embeddings with LangChain."
datePublished: Tue Dec 12 2023 09:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clq243opl000908l0gikv40nv
slug: local-embeddings-with-langchain
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702365617621/aadb0bf2-c730-48f1-945c-88a24a1993c6.png
tags: ai, artificial-intelligence, python, machine-learning, miniconda, memory-management, large-language-models, langchain, bs4, chromadb, llms, gpt4all, llama2, ollama, local-embeddings

---

Update: Thursday 25<sup>th</sup> January 2024.  
Update: Monday 18<sup>th</sup> March 2024.  
Update: Wednesday 20<sup>th</sup> March 2024.

# TL;DR.

The post demonstrates how to generate local embeddings with LangChain. Embeddings address some of the memory limitations in Large Language Models (LLMs). I demonstrate an embedding implementation using various AI tools. Using embeddings for long-term memory management has potential applications in many fields, including business, science, and engineering.

> **Attributions:**
> 
> * [https://www.youtube.com/watch?v=CPgp8MhmGVY](https://www.youtube.com/watch?v=CPgp8MhmGVY)
>     

# An Introduction.

In the fascinating world of AI, Large Language Models (LLMs) hold a special place due to their impressive ability to understand and generate human-like responses. However, their static memory, limited to what they were trained on, poses certain challenges. To tackle these limitations, I turn to using LangChain to create local embeddings. In this post, I delve deep into this innovative solution, demonstrating how to implement embeddings using tools like Ollama, Llama2, bs4, GPT4All, Chroma, and LangChain itself.

> The purpose of this post is to present a way for LLMs to use locally generated embeddings.

# The Big Picture.

LLMs (large language models) have static knowledge, limited to what they learned up until the day they were trained and compiled. They cannot retain new information beyond their base knowledge, meaning they only know what they've been taught and nothing more.

Embeddings (partly) resolve one of the known LLM memory issues.

# Prerequisites.

A Debian-based Linux distro (I use Ubuntu),

[Miniconda](https://solodev.app/installing-miniconda).

# Updating my Base System.

From the (base) terminal, I update my (base) system:

```plaintext
sudo apt clean && 
sudo apt update && 
sudo apt dist-upgrade -y && 
sudo apt --fix-broken install && 
sudo apt autoclean && 
sudo apt autoremove -y
```

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments while avoiding version conflicts.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the conda package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the conda package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/](http://www.anaconda.com/)↗,

[https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)↗, and

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

I ensure Miniconda is installed (`conda -V`) before continuing with this post.

## Creating a Miniconda Environment.

* I use `conda` to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to create, and activate, a new environment named (-n) (LangChain):
    

```bash
conda create -n LangChain python=3.11 -y && conda activate LangChain
```

> NOTE: This command creates the (LangChain) environment, then activates the (LangChain) environment.

## Creating the LangChain Home Directory.

> NOTE: I will define the home directory with settings in the environment directory.

* I create the LangChain home directory:
    

```bash
mkdir ~/LangChain
```

* I make new directories within the (LangChain) environment:
    

```bash
mkdir -p $HOME/miniconda3/envs/LangChain/etc/conda/activate.d
```

* I use Nano to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano $HOME/miniconda3/envs/LangChain/etc/conda/activate.d/set_working_directory.sh
```

* I add the following to the script, save the changes (CTRL + S), and exit (CTRL + X) the Nano text editor:
    

```bash
cd ~/LangChain
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (LangChain) environment:
    

```bash
conda activate LangChain
```

> NOTE: I should now, by default, be in the `~/LangChain` home directory.

# What is LangChain?

LangChain is a Python and JavaScript library that helps me build language model applications. It uses these models to help with tasks like answering questions, creating text, or performing other tasks.

## Installing LangChain.

* I install LangChain:
    

```bash
pip install langchain
```

## Updating Ollama.

* I update Ollama:
    

```bash
curl https://ollama.ai/install.sh | sh
```

## Installing Llama2.

* I install Llama2:
    

```bash
ollama pull llama2
```

## Creating a Python Module.

* I create a Python module called `langchain-test.py`:
    

```bash
sudo nano ./langchain-test.py
```

* I add the following to the `langchain-test.py` module, save the file, and exit Nano:
    

```python
from langchain.llms import Ollama
question = Ollama(base_url='http://localhost:11434', model='llama2')
print(question('Why is the sky blue?'))
```

* I run the `langchain-test.py` module:
    

```bash
python3 langchain-test.py
```

## Installing More Requirements.

* I install bs4:
    

```bash
pip install bs4
```

* I install GPT4All:
    

```bash
pip install gpt4all
```

* I install Chroma:
    

```bash
pip install chromadb
```

## Creating Another Python Module.

* I create another Python module called `langchain-ollama.py`:
    

```bash
sudo nano langchain-ollama.py
```

* I add the following to the `langchain-ollama.py` module:
    

```python
# Import Ollama
from langchain.llms import Ollama
# Import the document loader
from langchain.document_loaders import WebBaseLoader
# Import the text splitter
from langchain.text_splitter import RecursiveCharacterTextSplitter
# Import the GPT4All embeddings tool
from langchain.embeddings import GPT4AllEmbeddings
# Import the vector store
from langchain.vectorstores import Chroma
# Import chains
from langchain.chains import RetrievalQA

ollama = Ollama(base_url='http://localhost:11434', model='llama2')

# Load the document from a URL
loader = WebBaseLoader('https://solodev.app/12s-my-2024-technology-stack')
# Load the document contents as 'data'
data = loader.load()
# Define the 'text_splitter' params
text_splitter = RecursiveCharacterTextSplitter(chunk_size=200, chunk_overlap=3)
# Split the 'data'
all_splits = text_splitter.split_documents(data)
# Instantiate the vector store
vectorstore = Chroma.from_documents(documents=all_splits, embedding=GPT4AllEmbeddings())
# Use chains to link tasks
qachain = RetrievalQA.from_chain_type(ollama, retriever=vectorstore.as_retriever())

question = "What technologies will be used in 2024?"
print(qachain({"query": question}))
```

* I run the `langchain-ollama.py` module:
    

```bash
python3 langchain-ollama.py
```

# The Results.

Local embeddings with LangChain offer one solution to the memory limitations of Large Language Models (LLMs). By using tools like Ollama, Llama2, bs4, GPT4All, Chroma, and of course, LangChain itself, I can enhance the static knowledge of an LLM, making it more adaptable and versatile. This process, although technical, is achievable with a Linux-based operating system and Python 3.9 or later. The potential applications of this technology are vast, promising specialist knowledge adaptations in many fields including business, science, and engineering.

# In Conclusion.

In the fascinating world of AI, Large Language Models (LLMs) have some memory limitations. They can only retain information up to the day they were trained and compiled. But guess what? There is a workaround.

Local embeddings with LangChain!

The embedding approach helps LLMs overcome their memory limitations, making them more flexible and useful. Imagine LLMs not being restricted by their initial knowledge. With modern AI tools, I can increase an LLM's knowledge base. Embeddings offer specialized knowledge adaptations in many specialist fields.

I found the concept of embeddings easy to understand and so I created a comprehensive guide for myself. With a Linux-based operating system and Python 3.9 or later (and a decent GPU), I can extend the knowledge base of my favourite LLMs.

What's *your* take on this? What do you think the impact of embeddings will be? I'm looking forward to your thoughts and insights!

Until next time: Be safe, be kind, be awesome.

#LangChain #LocalEmbeddings #LargeLanguageModels  
#LLMs #ArtificialIntelligence #AI #MachineLearning  
#MemoryManagement #Miniconda #Python #Ollama  
#Llama2 #GPT4All #bs4 #ChromaDB #TechnicalGuide  
#AIInnovation