---
title: "Installing Mojo."
datePublished: Tue Dec 05 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clps40sbl000808l7ckaiebjq
slug: installing-mojo
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705269634784/7dac0957-c1e0-4186-bff1-1a3fd2ae8d7f.png
tags: ai, python, mojo, modular-ai-engine, modular-ai

---

Last Edit: Monday 15th January 2024.

# **TL;DR.**

Mojo is a scalable superset of the Python programming language. It includes enhancements for machine learning and model development, especially when used with the Modular AI Engine.

> ***Attribution:***
> 
> [***https://docs.modular.com/mojo/***](https://docs.modular.com/mojo/)***,***
> 
> [***https://docs.modular.com/mojo/manual/get-started/hello-world.html***](https://docs.modular.com/mojo/manual/get-started/hello-world.html)***.***

# An Introduction.

Mojo is a superset of Python, which means it provides additional features and functionalities while maintaining compatibility with the Python language. This allows me to leverage the benefits of both languages and potentially improve productivity and code quality.

> ***The purpose of this post is to install the Mojo programming language.***

# The Big Picture.

Mojo is a language that can be used for developing and deploying production-grade machine-learning models. It's known for its scalability, ease of use, and ability to handle large datasets, which can be a significant advantage for AI development.

Adopting a new language like Mojo can be a game-changer, but I might want to think about the following:

* How well does Mojo integrate with my current tools and systems?
    
* What kind of support and community exists for a Mojo developer?
    
* Can I easily find solutions or advice when I encounter issues?
    
* How much time and resources am I willing to invest in learning and implementing Mojo?
    

Using Mojo with the Modular AI Engine offers some compelling benefits. The Modular AI Engine allows for the integration of various AI models and algorithms, and Mojo is a robust and scalable language for developing these models. The Modular AI Engine and the Mojo language were created by the same team.

Here are a few advantages:

1. **Scalability**: Mojo is known for its ability to handle large datasets, which is crucial when working with complex AI models that require substantial amounts of data.
    
2. **Flexibility**: The Modular AI Engine's design allows me to easily integrate Mojo-developed models with other components of my system.
    
3. **Efficiency**: Using Mojo streamlines the process of developing, testing, and deploying AI models that are built with the Modular AI Engine.
    

As with any technology decision, it's important to examine the potential challenges. Consider the learning curve associated with Mojo, the compatibility with my existing tech stack, and the available support for this language.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

# Installing the Modular CLI.

* I update and upgrade my system:
    

```plaintext
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt autoclean && \
sudo apt --fix-broken install && \
sudo apt autoremove -y
```

* I install the Modular CLI:
    

```plaintext
curl https://get.modular.com | sh - && \
modular auth mut_9912866fd1474edda3785a9d3c2c9d64
```

# Updating the Modular CLI.

* I update to the latest version of the Modular CLI:
    

```bash
sudo apt install modular
```

# Installing Mojo SDK.

* I install the Mojo SDK:
    

```plaintext
modular install mojo
```

* I install the Mojo Extension for VS Code:
    

```plaintext
https://marketplace.visualstudio.com/items?itemName=modular-mojotools.vscode-mojo
```

# Updating the Mojo SDK.

* I update the Mojo SDK:
    

```plaintext
sudo apt update && \
sudo apt install modular && \
modular clean && \
modular install mojo
```

> NOTE: The Mojo language is under development and new features are constantly added.

# Uninstalling the Mojo SDK.

* I can uninstall the Mojo SDK:
    

```bash
modular uninstall mojo
```

# Uninstalling the Modular CLI.

* I uninstall the Modular CLI:
    

```plaintext
sudo apt uninstall modular
```

# Setting the Environment Variables.

* I set the `MODULAR_HOME` environment variable:
    

```bash
echo 'export MODULAR_HOME="$HOME/.modular"' >> ~/.bashrc
```

* I set the `PATH` environment variable:
    

```bash
echo 'export PATH="$MODULAR_HOME/pkg/packages.modular.com_mojo/bin:$PATH"' >> ~/.bashrc
```

* I set the source:
    

```bash
source ~/.bashrc
```

# Running Code in a REPL.

* I start a REPL session for Mojo:
    

```bash
mojo
```

> ***NOTE: REPL (Read-Eval-Print Loop) is an environment where user inputs are read and evaluated, and then the results are returned to the user.***

* I enter the following and press ENTER twice (a blank line represents the end of an expression):
    

```bash
print("Hello, from the Mojo REPL!")
```

* I exit the REPL (CTRL + C).
    

# Running Code in a Mojo File.

* I use the Nano text editor to create the `hello.mojo` file:
    

```plaintext
sundo nano ./hello.mojo
```

* I add the following to the `hello.mojo` file, save (CTRL + S) the changes, and exit (CTRL + X) the Nano text editor:
    

```plaintext
fn main():
    print("Hello, world!")
```

* I use Mojo to run the `hello.mojo` file:
    

```plaintext
mojo hello.mojo
```

# Running Code as an Executable Binary.

* I use `Mojo` to run the `build` command on the `hello.mojo` file:
    

```plaintext
mojo build hello.mojo
```

* I can run the executable file without needing to use `Mojo` because the build process compiles the code and libraries it needs to run *into* that executable file:
    

```plaintext
./hello
```

# The Results.

I've walked through the process of installing the Mojo programming language on a Debian-based Linux system called Ubuntu. I've covered the installation of the Modular CLI and Mojo SDK, setting the environment variables, running code in a REPL, creating and running a Mojo file, and even building an executable binary. I am now ready to explore the Mojo programming languages' capabilities.

# In Conclusion.

In this post, I compiled a step-by-step guide that got me up and running with Mojo by installing the programming language on a Debian-based Linux system called Ubuntu.

First off, I started with updating and upgrading the system. Then I got my hands on the Modular CLI and Mojo SDK, the two tools I needed to start my Mojo journey.

But it didn't stop there. To make your life easier, I also install the Mojo Extension for VS Code. And let's not forget about a process for keeping the Mojo SDK up to date.

Now, onto the environment variables. I used Nano to open the `.bashrc` file. Then I added a few lines of code at the bottom of the file, saved the changes, and exited the editor. To make sure these changes took effect, I sourced the `.bashrc` file.

Then I ran some code! I started a REPL, typed in some code, and then exited. I also create a Mojo file, add some code to it, and ran it with Mojo. Finally, I built an executable binary.

Voila! Now I'm all set to start exploring the Mojo programming language and this is just the beginning of what I can achieve. I can't wait to see what machine learning and deep learning models I'll build with this powerful language.

Have you used Mojo before? What do you think about it?

Please share your thoughts in the comments!

Until next time: Be safe, be kind, be awesome.