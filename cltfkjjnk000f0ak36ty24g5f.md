---
title: "Installing Jupyter Notebook within Miniconda."
datePublished: Wed Mar 06 2024 09:00:30 GMT+0000 (Coordinated Universal Time)
cuid: cltfkjjnk000f0ak36ty24g5f
slug: installing-jupyter-notebook-within-miniconda
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709426723081/fc2ab15a-939b-445f-b655-21eda6a72f76.png
tags: software-development, technology, python, data-science, opensource, machine-learning, programming-ciovqvfcb008mb253jrczo9ye, jupyter-notebook, miniconda, coding-community

---

# TL;DR.

This post guides me through installing Jupyter Notebook, within Miniconda, on a Debian-based Linux distro called Ubuntu. It starts with updating my base system, then I move on to installing Miniconda, creating a dedicated Miniconda environment, and setting up a Jupyter home directory. I explain Miniconda and Jupyter Notebook, then provide details on how to install Jupyter Notebook, change its default browser, and create a "Hello World" Notebook. The post ends by showcasing the benefits of combining Miniconda and Jupyter Notebook for Python development.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***
> 
> [https://jupyter.org/](https://jupyter.org/)***↗.***

# An Introduction.

> NOTE: The classic, Jupyter Notebook is on the verge of being sunset. Its replacement is JupyterLab which, among other things, includes an embedded version of Jupyter Notebook.

Computer scientists need a simple tool to collect data, apply algorithms to that data, generate visualisations of their results, and present their analysis and conclusions to their colleagues. Jupyter Notebook is *the* computer science tool.

> The purpose of this post is to show an installation process for Jupyter Notebook.

# The Big Picture.

Jupyter Notebook is very popular in the field of computer science and quickly became the de facto platform for data science. Many machine learning and deep learning research papers mention Jupyter Notebook. These Notebooks work well with tools like TensorFlow and PyTorch, and Jupyter Notebook lets researchers mix their code and data with analysis and ideas. This helps computer scientists think creatively. If you haven't checked it out yet, now is a great time to install Jupyter Notebook before it disappears.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my Base System.

* In a terminal, I update my base system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is Miniconda?

Miniconda is a free, small, bootstrap version of Anaconda that includes the conda package manager, Python, packages they both depend on, and a small number of other useful packages (like pip and zlib).

I first ensure that [Miniconda has been installed](https://solodev.app/installing-miniconda) before continuing.

## Creating a Miniconda Environment.

* I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (Jupyter):
    

```bash
conda create -n Jupyter python=3.11 -y && conda activate Jupyter
```

> NOTE: This command creates the (Jupyter) environment, then activates the (Jupyter) environment.

## Creating the `Jupyter` Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the `Jupyter` home directory:
    

```bash
mkdir ~/Jupyter
```

* I make new directories within the (Jupyter) environment:
    

```bash
mkdir -p ~/miniconda3/envs/Jupyter/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/Jupyter/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Jupyter
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (Jupyter) environment:
    

```bash
conda activate Jupyter
```

> NOTE: I should now, by default, be in the `~/Jupyter` home directory.

# What is Jupyter Notebook?

Jupyter Notebook is an open source web application that lets me create, and share, documents that include live code, equations, visuals, and text. It is managed by the maintainers at [Project Jupyter](http://jupyter.org/) and started as part of the IPython project. The name "Jupyter" reflects the main languages it supports: Julia, Python, and R. It comes with the IPython kernel for Python programming, but I can also use over 100 other kernels.

## Installing Jupyter Notebook.

* I use the `pip` command to install the classic Jupyter Notebook:
    

```bash
pip install notebook
```

## Changing the Default Browser for Jupyter Notebook.

* I generate a Jupyter Notebook configuration file:
    

```bash
jupyter notebook --generate-config
```

* I use the Nano text editor to open the config file:
    

```bash
sudo nano ~/.jupyter/jupyter_notebook_config.py
```

* I navigate to the end of the file with (CTRL + END).
    
* I copy the following, paste (CTRL + SHIFT + V) it into the Python module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
c.ServerApp.browser = '/bin/brave-browser %s'
#c.ServerApp.browser = '/bin/firefox %s'
#c.ServerApp.browser = '/bin/google-chrome %s'
```

> NOTE: The Brave browser is now set as the default browser. I can also choose Firefox or Chrome, but it is important to uncomment only one browser at a time.

## Running the Jupyter Home Page.

* I run the Jupyter Notebook:
    

```bash
jupyter notebook
```

> NOTE: This command starts a local Python server (http://localhost) and then the Jupyter Home Page, running on port 8888, opens in my assigned browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709300716185/311d6190-eac2-4249-808e-1ea827a0645d.png align="center")

## Creating the "Hello World" Notebook.

* In the file menu, I select "File &gt; New &gt; Notebook":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709302000585/f6038c0f-1cdc-4e17-b7b1-7811a9b28401.png align="center")

> NOTE: I can also click the "New" button at the top-right of the page.

* I choose the default "Python 3 (ipykernel)" kernel, select the "Always start the preferred kernel" tick box, and click the blue "Select" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709304439910/98dfd0d1-0811-4926-93fd-2cf867bd6276.png align="center")

> NOTE: The Notebook opens in a new browser tab.

* In the file menu of the Notebook, I select "File &gt; Rename...":
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305076720/3a32019c-03b0-4c48-8b38-68a3cec5ebf7.png align="center")

* I rename the Notebook as "Hello World.ipynb" and click the blue "Rename" button:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305102700/c95223f9-d3d7-42f1-a269-cc316d8b37a6.png align="center")

## Running the "Hello World" Cell.

* I add the following to the first cell:
    

```bash
print("Hello, World.")
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305129610/de8b6cde-0bca-4163-83da-812ce993a150.png align="center")

* I use SHIFT + ENTER to run the cell:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305147938/cbcd47e9-642a-438a-8b9d-748f327534c6.png align="center")

> NOTE: The first cell is now numbered \[1\].

* I return to the Home tab to see the newly listed Notebook:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305164900/1ef40e87-5772-48f7-b11d-98451d8964d3.png align="center")

## Opening a Notebook.

* I can select the Notebook and click the "Open" button, or I can right-click the Notebook and select the "Open" option from the pop-up menu:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1709305924466/90edc7d1-bccb-49f5-ba9a-f43193f462ef.png align="center")

# The Results.

Installing Jupyter Notebook within Miniconda offers a streamlined, efficient environment for Python development and data analysis. By leveraging Miniconda, I gain a lightweight, flexible platform that supports the creation of isolated environments tailored to specific projects. My step-by-step guide provided outlines to the process of setting up Miniconda, creating a dedicated environment, and installing Jupyter Notebook. Customizing the Jupyter Notebook environment to fit individual workflow preferences, such as changing the default browser, enhances the user experience. With Jupyter Notebook, I have the ability to combine executable code, rich text, visuals, and equations in a single document that fosters a more interactive, engaging way of presenting data, analysis, and research findings. This approach simplifies the development process and also encourages a more collaborative and reproducible research environment. As demonstrated, the integration of Miniconda and Jupyter Notebook is a powerful combination for anyone looking to dive into data science, machine learning, or general Python programming, providing the tools necessary for a productive coding environment.

# In Conclusion.

Exciting news for Python enthusiasts and data scientists!

I've just navigated the seamless installation of Jupyter Notebook within Miniconda, and the journey was nothing short of enlightening.

Miniconda serves as a lightweight champion, offering the perfect balance between efficiency and functionality with its minimalistic yet powerful package management system.

Why is this important?

It enables a streamlined environment for Python development and sophisticated data analysis without the overhead of unnecessary packages.

The real magic happens when Jupyter Notebook enters the scene. This open-source web application transforms how we present data, code, and research findings.

Imagine combining executable code, rich text, visuals, and equations all in one document.

That's the interactive, engaging experience Jupyter Notebook offers.

Through my step-by-step guide, I've shared insights on setting up Miniconda, creating isolated environments, and customizing Jupyter to enhance your workflow.

This approach not only simplifies the development process but fosters a more collaborative and reproducible research environment.

The integration of Miniconda and Jupyter Notebook is a game-changer for anyone diving into data science, machine learning, or general Python programming.

It's about making our coding environment as productive and enjoyable as possible.

Have you integrated Jupyter Notebook into your Python projects yet?

What has been your experience?

Let's share insights and grow together!

#JupyterNotebook #Python #Programming #SoftwareDevelopment #CodingCommunity #DataScience #MachineLearning #OpenSource #Technology #Miniconda