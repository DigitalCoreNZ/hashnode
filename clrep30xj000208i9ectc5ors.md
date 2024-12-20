---
title: "Installing ComfyUI, it's Manager, and SDXL (DEPRECATED)."
datePublished: Mon Jan 15 2024 09:00:27 GMT+0000 (Coordinated Universal Time)
cuid: clrep30xj000208i9ectc5ors
slug: installing-comfyui-its-manager-and-sdxl
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704961284771/634c7465-f793-4699-ad5a-8851a9291a48.png
tags: ai-image-generator, sdxl, comfyui, comfyui-manager, ai-image-generation

---

# DEPRECATED.

Use [Pinokio](https://solodev.app/apps-utilities-for-ubuntu-2404-lts#heading-installing-pinokio) to run ComfyUI.

# TL;DR.

This post is a guide to installing ComfyUI and Stable Diffusion XL (SDXL) within an Anaconda environment on an Ubuntu distro. It covers the environment setup, using git to clone the ComfyUI repo, downloading the SDXL checkpoints, and combining a few other tools. This guide also includes references to other, popular workflows.

> **Attributions:**
> 
> [https://aituts.com/comfyui/](https://aituts.com/comfyui/)***↗.***

# An Introduction.

Prompting AI to generate images was a Big Deal in 2023. This post shows how I put together a few tools so I can make AI-generated images, too.

> The purpose of this post is to install ComfyUI and SDXL.

# The Big Picture.

The practical reason for installing ComfyUI is to generate images for my posts and projects. In the future, I also want to write a post about combining the ComfyUI server with an image editor. (Foreshadowing much?)

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my Base System.

* In the base terminal, I update my base system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
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

* I use `conda` to create, and activate, a new environment named (-n) (ComfyUI):
    

```bash
conda create -n ComfyUI python=3.11 -y && conda activate ComfyUI
```

> NOTE: This command creates the (ComfyUI) environment, then activates the (ComfyUI) environment.

# Cloning the ComfyUI Repo.

* I change to the $HOME directory:
    

```plaintext
cd ~
```

* I use `git` to `clone` the ComfyUI `repo`:
    

```plaintext
git clone https://github.com/comfyanonymous/ComfyUI.git
```

# Changing the ComfyUI Home Directory.

* I make new directories within the (ComfyUI) environment:
    

```bash
mkdir -p ~/miniconda3/envs/ComfyUI/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/ComfyUI/etc/conda/activate.d/set_working_directory.sh
```

* I add the following to the script, save the changes (CTRL + S), and exit (CTRL + X) the Nano text editor:
    

```bash
cd ~/ComfyUI
```

* I activate the (base) environment:
    

```bash
conda activate
```

# Installing the ComfyUI Requirements.

* I activate the (ComfyUI) environment:
    

```bash
conda activate ComfyUI
```

> NOTE: Activating the (ComfyUI) environment takes me to the `ComfyUI` directory.

* I install the ComfyUI requirements:
    

```plaintext
pip install -r ./requirements.txt
```

* I install pyTorch:
    

```plaintext
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu121
```

# Running ComfyUI.

* I change to the `ComfyUI` directory:
    

```plaintext
cd ~/ComfyUI
```

* I run the ComfyUI server:
    

```plaintext
python3 main.py
```

* I run the ComfyUI GUI from a browser:
    

```plaintext
http://127.0.0.1:8188
```

# Finishing the ComfyUI Installation.

To save some time and bandwidth, I usually copy-paste local copies of the `custom_nodes` and `models` directories. When I make changes to ComfyUI, I also update these directories. Below are the processes I used to build these directories.

## Cloning the ComfyUI Manager.

> NOTE: This is part of my local copy-paste `custom_nodes` directory.

* I change to the `custom_nodes` directory:
    

```plaintext
cd ~/ComfyUI/custom_nodes
```

* I use `git` to `clone` the ComfyUI Manager `repo`:
    

```plaintext
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```

* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

## Installing the SDXL Checkpoints.

> NOTE: These are part of my local copy-paste `models` directory.

* I download the SDXL checkpoints:
    
    * [**SDXL 1.0 base checkpoint**](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/resolve/main/sd_xl_base_1.0.safetensors)
        
    * [**SDXL 1.0 refiner checkpoint**](https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0/resolve/main/sd_xl_refiner_1.0.safetensors)
        
* I change to the ~/Downloads directory:
    

```plaintext
cd ~/Downloads
```

* I move the SDXL 1.0 base checkpoint to the checkpoints directory:
    

```plaintext
mv ./sd_xl_base_1.0.safetensors ~/ComfyUI/models/checkpoints/sd_xl_base_1.0.safetensors
```

* I move the SDXL 1.0 refiner checkpoint to the checkpoints directory:
    

```plaintext
mv ./sd_xl_refiner_1.0.safetensors ~/ComfyUI/models/checkpoints/sd_xl_refiner_1.0.safetensors
```

* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

## Tools.

Below is a small list of tools that may (or may not) come in handy.

### VAEs.

> NOTE: This is part of my local copy-paste `models` directory.

VAE (Variational Auto Encoder) is an AI neural network architecture. During training, encoding distributions are regularised so its latent space allows a model to generate new data.

* I download and place the VAE in the `ComfyUI/models/vae` directory.
    
* [**Fixed SDXL 0.9 VAE**](https://huggingface.co/madebyollin/sdxl-vae-fp16-fix/resolve/main/sdxl_vae.safetensors)
    
* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

### LoRAs.

> NOTE: This is part of my local copy-paste `models` directory.

LoRAs (Low-Rank Adaptations) are small, fine-tuned models that are trained on large, base models and are used to introduce new concepts to that LLM.

* I download and place the LoRA in the `ComfyUI/models/loras` directory.
    
* [**SDXL Offset Noise LoRA**](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/resolve/main/sd_xl_offset_example-lora_1.0.safetensors)
    
* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

### Upscalers.

> NOTE: These are part of my local copy-paste `models` directory.

These tools are used to upscale my images. Some workflows don't include them while other workflows require them.

I download and place the upscalers in the `ComfyUI/models/upscaler` directory.

* [**4x\_NMKD-Siax\_200k.pth upscaler**](https://huggingface.co/uwg/upscaler/resolve/main/ESRGAN/4x_NMKD-Siax_200k.pth)
    
* [**4x-Ultrasharp.pth upscaler**](https://huggingface.co/uwg/upscaler/resolve/main/ESRGAN/4x-UltraSharp.pth)
    
* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

## Workflows.

Below is a small list of workflows.

### The ComfyUI Examples.

* I visit the [ComfyUI repo](https://github.com/comfyanonymous/ComfyUI_examples) for a list of examples.
    

### The Sytan SDXL Workflow.

> NOTE: This is part of my local copy-paste `custom_nodes` directory.

* I navigate to the ComfyUI `custom_nodes` directory:
    

```plaintext
cd ~/ComfyUI/custom_nodes
```

* I use `Git` to `clone` the Searge `repo`:
    

```plaintext
git clone https://github.com/SytanSD/Sytan-SDXL-ComfyUI.git
```

* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

### **The Searge SDXL** Workflow.

> NOTE: Extra downloads and some tweaking is needed to successfully deploy the SeargeSDXL workflow. I read the documentation for more information.

> NOTE: This is part of my local copy-paste `custom_nodes` directory.

* I navigate to the ComfyUI `custom_nodes` directory:
    

```plaintext
cd ~/ComfyUI/custom_nodes
```

* I use `Git` to `clone` the Searge `repo`:
    

```plaintext
git clone https://github.com/SeargeDP/SeargeSDXL.git
```

* I return to the ComfyUI directory:
    

```plaintext
cd ~/ComfyUI
```

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

# The Results.

This post provided a comprehensive guide to installing ComfyUI, the ComfyUI Manager, and SDXL within an Anaconda environment running on an Ubuntu distro. It started with setting up a `conda` environment, moved on to installing the necessary components, and eventually described how to run the ComfyUI server and view the UI in a browser. This guide also provided links to other tools and workflows. By following these instructions, I was able to set up, and run, ComfyUI and SDXL on my PC.

# In Conclusion.

I was looking to install ComfyUI and SDXL within an Anaconda environment on my Ubuntu system. As a result of my investigations, I ended up with this guide.

In this post, I went through the environment setup, used git to clone the ComfyUI repo, downloaded the SDXL checkpoints, and combined ComfyUI with a few other tools and workflows.

Why would I want to install ComfyUI? Well, it's an amazing tool that I can use to generate images for my posts and projects.

I used a Debian-based distro called Ubuntu, as well as Anaconda, to get started. From there, I went through using Anaconda to setup an environment, cloning the ComfyUI repo, installing the ComfyUI requirements, and cloning the ComfyUI Manager. To save time and bandwidth, I copy-pasted a local copy of the 50GB+ `models` directory into the ComfyUI directory. I also included links to download the SDXL checkpoints, a list of tools, and a few workflow references.

By the end of this guide, I was able to efficiently set up and run ComfyUI and SDXL on my PC. This comprehensive guide makes the setup process a lot easier for me. (As a development workstation, I'm constantly destabilising this system. Yes, I'm always cloning (and using) recovery images, but these guides are also part of my Upgrade Plan for when the next LTS distro is released.)

Have you dived into the world of ComfyUI and SDXL? Let me know in the comments below if you've used ComfyUI or SDXL before, and what your experience was like.

Until next time: Be safe, be kind, be awesome.