---
title: "Pythagora: DeepSpeech."
slug: pythagora-deepspeech

---

# TL;DR.

\[pending\]

> **Attributions:**
> 
> ***pending ↗.***

# An Introduction.

\[pending\]

# The Big Picture.

\[pending\]

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

* I use `conda` to `create`, and `activate`, a new environment named (-n) (DeepSpeech):
    

```bash
conda create -n DeepSpeech python=3.11 -y && conda activate DeepSpeech
```

> NOTE: This command creates the (DeepSpeech) environment, then activates the (DeepSpeech) environment.

## Creating the DeepSpeech Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the DeepSpeech home directory:
    

```bash
mkdir ~/DeepSpeech
```

* I make new directories within the (DeepSpeech) environment:
    

```bash
mkdir -p ~/miniconda3/envs/DeepSpeech/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/DeepSpeech/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/DeepSpeech
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (DeepSpeech) environment:
    

```bash
conda activate DeepSpeech
```

> NOTE: I should now, by default, be in the `~/DeepSpeech` home directory.

# What is DeepSpeech?

DeepSpeech is a neural network architecture first published by a research team at Baidu. In 2017, Mozilla created an open source implementation of this paper called Mozilla DeepSpeech. This speech-to-text engine uses Google's TensorFlow to make the implementation easier.

## Creating, and activating, a venv.

* I make a new directory called deep-env:
    

```plaintext
mkdir ./deep-env
```

* I create a new venv (virtual environment):
    

```plaintext
python -m venv --without-pip ~/DeepSpeech/deep-env
```

* I activate the venv:
    

```plaintext
source ~/DeepSpeech/deep-env/bin/activate
```

* From the (deep-env) environment, I install pip:
    

```plaintext
curl https://bootstrap.pypa.io/get-pip.py | python
```

* I check pip:
    

```plaintext
which pip
```

* I upgrade pip:
    

```plaintext
pip install --upgrade pip
```

* I install DeepSpeech:
    

```plaintext
pip install deepspeech
```

* I download pre-trained English model files:
    

```plaintext
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.pbmm && \
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.scorer
```

* I download example audio files:
    

```plaintext
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/audio-0.9.3.tar.gz
```

* I extract the audio files:
    

```plaintext
tar xvf audio-0.9.3.tar.gz
```

* I transcribe an audio file:
    

```plaintext
deepspeech --model deepspeech-0.9.3-models.pbmm --scorer deepspeech-0.9.3-models.scorer --audio audio/2830-3980-0043.wav
```

* I deactivate the (deep-env) environment:
    

```plaintext
deactivate
```

* I activate the (base) environment:
    

```plaintext
conda activate
```

## Project Details.

You are a TypeScript programmer.

# The Results.

\[pending\]

# In Conclusion.

\[pending\]