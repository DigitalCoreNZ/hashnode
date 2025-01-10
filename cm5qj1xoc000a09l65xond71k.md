---
title: "DSPy 01: Install, Setup, and Test."
datePublished: Fri Jan 10 2025 09:00:45 GMT+0000 (Coordinated Universal Time)
cuid: cm5qj1xoc000a09l65xond71k
slug: dspy-01-install-setup-and-test
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1736447549485/b7aca566-4954-4914-95a3-d80dd1a337ca.png

---

# TL;DR.

This post is a guide to installing, setting up, and testing DSPy (***Declarative Self-improving Python***) and will cover the following topics:

* The prerequisites for assembling a DSPy development environment,
    
* The installation of Ollama and Miniconda,
    
* The creation of a Conda environment for DSPy,
    
* The installation of the DSPy framework,
    
* The installation and setup up of Jupyter Notebook, and
    
* The testing of the newly assembled DSPy development environment.
    

The aim of this guide is to assemble, and test, a development environment for DSPy programming.

> **Attributions *↗*:**
> 
> [https://dspy.ai/tutorials/rag/](https://dspy.ai/tutorials/rag/) ***↗,***
> 
> [https://github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy) ***↗.***

# An Introduction.

DSPy is used to programmatically provide "a more systematic approach to solving hard tasks with advanced LMs." It exists to build simple Classifiers, sophisticated RAG pipelines, and Agentic loops.

> The purpose of this post is to provide a process for creating a DSPy programming environment.

# The Big Picture.

For classifiers, RAG (Retrieval-Augmented Generation), and agent, the main idea is to take advantage of advanced LM workflows, especially those systems that can retrieve relevant information while generating contextually accurate responses. By integrating retrieval mechanisms with generative models, these workflows aim to create intelligent systems that can autonomously navigate complex tasks, adapt to dynamic environments, and provide insightful solutions. This approach not only improves the accuracy and relevance of LM outputs but also empowers users to leverage AI for complex, problem-solving operations.

DSPy is a programmatic tool for creating advanced AI solutions that was originally designed to replace the clunky, and fragile, prompt engineering paradigm.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

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

# What is Ollama?

Ollama is a tool that is used to download, set up, and run large language models on a local PC. It lets me use powerful models like Llama 2 and Mistral on my personal computer. Ollama natively runs on Linux, macOS, and Windows (in preview).

## Installing Ollama.

* From the terminal, I install Ollama:
    

```bash
curl https://ollama.ai/install.sh | sh
```

* I list the LMs downloaded by Ollama:
    

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

## Pulling an Advanced LM.

* I pull an advanced LM:
    

```bash
ollama pull qwen2.5-coder:latest
```

---

# What is Miniconda?

Miniconda, a bootstrap version of Anaconda, is a virtual environment manager that is small, FREE, and also includes the conda package manager, Python, and other packages that are required or useful to a developer, like pip and zlib.

## Installing Miniconda.

* I make the Miniconda directory:
    

```bash
mkdir -p ~/miniconda3
```

* I download the installation payload:
    

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
```

* I run the installation:
    

```bash
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
```

* I remove the payload:
    

```bash
rm -rf ~/miniconda3/miniconda.sh
```

## Initialising Miniconda.

* I initialize `Miniconda`:
    

```bash
~/miniconda3/bin/conda init bash
```

## Updating Miniconda.

* I change the owner of the `Miniconda` directory to the current, logged-in account:
    

```bash
sudo chown -R $USER:$USER $HOME/miniconda3
```

* I update `Miniconda`:
    

```bash
conda update -n base -c defaults conda
```

## Creating a Conda Environment.

* I use `conda` to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (DSPy):
    

```bash
conda create -n DSPy python=3.11 -y && conda activate DSPy
```

> NOTE: This command creates the (DSPy) environment, then activates the (DSPy) environment.

## Creating the `DSPy` Home Directory.

> NOTE: I will define the home directory with settings in the environment directory.

* I create the `DSPy` home directory:
    

```bash
mkdir ~/DSPy
```

* I make new directories within the (DSPy) environment:
    

```bash
mkdir -p ~/anaconda3/envs/DSPy/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/anaconda3/envs/DSPy/etc/conda/activate.d/set_working_directory.sh
```

* I add the following, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/DSPy
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (DSPy) environment:
    

```bash
conda activate DSPy
```

> NOTE: I should now, by default, be in the `~/DSPy` home directory.

---

# Installing DSPy.

* From the (DSPy) terminal, I install the latest version of DSPy:
    

```bash
pip install git+https://github.com/stanfordnlp/dspy.git
```

* I can also use pip to install DSPy directly from PyPI:
    

```bash
pip install -U dspy
```

---

# Installing Jupyter Notebook

* From the DSPy terminal, I install Jupyter Notebook:
    

```bash
pip install notebook
```

* I generate a Jupyter Notebook configuration file:
    

```bash
jupyter notebook --generate-config
```

* I open the configuration file with the Nano text editor:
    

```bash
sudo nano ~/.jupyter/jupyter_notebook_config.py
```

* I set a default browser\*:
    

```bash
c.ServerApp.browser = '/bin/brave-browser %s'
```

* I save (CTRL + S) the changes and exit (CTRL + X) the Nano text editor,
    
* I upgrade Jupyter Notebook:
    

```bash
pip install --upgrade jupyter
```

* I upgrade a Jupyter Notebook dependency:
    

```bash
pip install --upgrade ipywidgets
```

* I run the Jupyter Notebook on port 8091:
    

```bash
jupyter notebook --port 8091
```

* In the file menu, I select "File &gt; New &gt; Notebook",
    
* I choose the default "Python 3 (ipykernel)" kernel, select the "Always start the preferred kernel" tick box, and click the blue "Select" button,
    
* In the file menu of the Notebook, I select "File &gt; Rename...",
    
* I rename the Notebook as "Hello World.ipynb" and click the blue "Rename" button.
    

---

# Testing the DSPy Environment.

* In the “Hello World“ Notebook, I define the local model that is used by DSPy:
    

```bash
import dspy

lm = dspy.LM(model='ollama/qwen2.5-coder:latest')
dspy.configure(lm=lm)
```

* I declare a module that takes a `question` (of type `str`) as input and produces a `response` as an output:
    

```bash
qa = dspy.Predict('question: str -> response: str')
response = qa(question="What is Hello World?")

print(response.response)
```

---

# The Results.

Setting up DSPy involves creating a robust, development environment where complex tasks can leverage the capabilities of advanced, and powerful, language models. By following the outlined process, from installing Ollama and Miniconda, to creating a dedicated Conda environment, while setting up a Jupyter Notebook, I can use the resulting environment to efficiently manage (and execute) DSPy programmes. The whole purpose of this post is to setup a local workspace for DSPy development. With DSPy, I will be equipped to explore, and implement, advanced LM capabilities that provide leading, innovative solutions.

---

# In Conclusion.

I am now ready to revolutionize my approach to complex tasks with advanced LMs. Meet DSPy (***Declarative Self-improving Python***) – my new best friend in systematic problem-solving!

Setting up DSPy is a breeze with a few essential steps. I start by installing Ollama and Miniconda, then I create a dedicated environment for DSPy.

Next, set up Jupyter Notebook to streamline my workflow and enhance productivity. With DSPy, I’m paving the way for innovative solutions across numerous domains.

By following this structured setup, I can efficiently manage and execute DSPy procedures, unlocking advanced LM capabilities.

Are you ready to explore the potential of DSPy in your projects? How do you plan to leverage advanced LMs for your next big idea? Let's discuss below!

Until next time: Be safe, be kind, be awesome.

---

# Tags.

#DSPy #Python #LanguageModels #Innovation #ProblemSolving