---
title: "Installing Node and NPM with NVM."
datePublished: Wed Jan 24 2024 09:00:25 GMT+0000 (Coordinated Universal Time)
cuid: clrrk1ndm000109ia5fik6lgy
slug: installing-node-and-npm-with-nvm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709711513513/6e0820e9-a6c2-4ecf-aab4-a566aafb4797.png
tags: software-development, javascript, web-development, nodejs, npm, coding, node, programming-ciovqvfcb008mb253jrczo9ye, nvm, node-js, node-version-manager, tech-guide, node-package-manager

---

# TL;DR.

This post provides a step-by-step guide on how to install NVM (Node Version Manager) for managing Node and NPM versions. It covers everything from the prerequisites and installation of CURL to installing and activating NVM. It then details how to use NVM to install Node LTS and NPM, setting Node LTS as the default NVM version, and confirming the installations. It also includes instructions on how to test the installation by creating and running a simple Node.js project.

> **Attributions:**
> 
> [https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)↗,
> 
> [https://docs.npmjs.com/about-npm](https://docs.npmjs.com/about-npm)↗, and
> 
> [https://github.com/nvm-sh/nvm#intro](https://github.com/nvm-sh/nvm#intro)↗.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705058792137/dc96dd05-e3dd-4b7d-8e02-0010c2afcb57.png align="center")

# An Introduction.

Node is a commonly-used JavaScript runtime that uses the V8 engine from Google. NPM (Node Package Manager) usually ships with Node. NVM (Node Version Manager) is a utility that manages Node versions on my system.

> The purpose of this post is to use NVM to install the latest Node LTS and NPM.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705058738171/d0240ae2-066f-4013-83e2-6fd0444d069d.png align="center")

# The Big Picture.

NVM (Node Version Manager) is capable of much more than is described in this post. For instance, I can have multiple versions on Node installed on my system(s) and, thanks to NVM, I can easily switch between any of them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705058764853/3ff5e17b-d55d-4ee8-a309-699670372445.png align="center")

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705058819339/4c70bd64-9a99-4f94-b5c3-f8c760f341e6.png align="center")

# What is Node.js, NPM, and NVM?

Node.js is a free, JavaScript (JS) server runtime. It runs JS code as single-threaded, non-blocking, asynchronous programs, which makes it very memory efficient. Node.js performs many system-level tasks, but is commonly used to run JS servers.

NPM (Node Package Manager) is the world's largest software registry. Open source developers use it to share packages with each other. Many organizations use NPM to manage private development as well. Most developers interact with NPM using the CLI (Command Line Interface), and usually ships with Node.js.

NVM (Node Version Manager) is used to switch between versions of Node.js. NVM works on any POSIX-compliant shell (sh, dash, ksh, zsh, bash) and runs on Linux distros, macOS, and Windows WSL.

[https://nodejs.org/en/learn/getting-started/introduction-to-nodejs](https://nodejs.org/en/learn/getting-started/introduction-to-nodejs)↗,

[https://docs.npmjs.com/about-npm](https://docs.npmjs.com/about-npm)↗, and

[https://github.com/nvm-sh/nvm#intro](https://github.com/nvm-sh/nvm#intro)↗.

## Installing CURL.

* From the terminal, I install CURL:
    

```bash
sudo apt install -y curl
```

## Installing Node.js, NPM, and NVM.

* From the terminal, I install the NVM (Node Version Manager):
    

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

> NOTE: The version numbers are [listed on the NVM GitHub page](https://github.com/nvm-sh/nvm/tags).

* I activate the NVM:
    

```bash
source ~/.bashrc
```

* I use the NVM to install the LTS version of Node.js:
    

```bash
nvm install --lts
```

> NOTE: The Node and NPM versions are listed on the screen.

* I make Node LTS the default NVM version, as listed in the previous command:
    

```bash
nvm alias default 20.11.0
```

* I confirm the Node installation:
    

```bash
node -v
```

* I confirm the NPM installation:
    

```bash
npm -v
```

## Testing the Installation.

* I make, and change into, a new directory:
    

```bash
mkdir ./test-node-project && cd ./test-node-project
```

* I initialize a new Node project:
    

```bash
npm init -y
```

> NOTE: This command will create a `package.json` file:
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705007002426/8354a297-a7b2-4952-8508-f2c049580d27.png align="center")

* I use the Nano text editor to create a file called `app.js`:
    

```bash
sudo nano app.js
```

* I add the following, save (CTRL + S) the changes, and close (CTRL + X) the Nano text editor:
    

```plaintext
console.log("Hello, from Node.js!");
```

* I run the following command:
    

```bash
node app.js
```

> NOTE: A successful test result has the "Hello, from Node.js!" message printed to the terminal.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705059281951/2aafc759-bd9b-4c65-94cb-25017f0bc51d.png align="center")

# The Results.

Installing NVM on a Debian-based Linux system like Ubuntu allows for easy management of Node.js and NPM versions. This guide walked through installing CURL and NVM to installing, and setting up, the default Node LTS and NPM versions. The successful execution of a simple Node.js project confirmed the installation processes. With NVM, I can now effortlessly switch between different Node versions as needed, enhancing my development workflow.

# In Conclusion.

I've struggled with managing different versions of Node.js and NPM on my system, but here's the solution: Node Version Manager (NVM). NVM lets me install, manage, and switch between different versions of Node.js and NPM with ease.

I've crafted a step-by-step guide on how I install and use NVM on a Debian-based Linux system (like Ubuntu). From installing the prerequisites like CURL, to setting up NVM, and finally running a simple Node.js project to test the installation, this guide has me covered.

Key takeaway? NVM let's me effectively control my Node.js environment, there by enhancing my development workflow. Node.js version management is now easier and more efficient.

Have you tried NVM? How was your experience? Share your thoughts in the comments below!

Until next time: Be safe, be kind, be awesome.

#Node.js #NodeJS #Node #NPM #NodePackageManager #NVM #NodeVersionManager #JavaScript #WebDevelopment #Coding #TechGuide #Programming #SoftwareDevelopment

> NOTE: All images generated by [ComfyUI](https://github.com/comfyanonymous/ComfyUI) using the [juggernautXL\_version6Rundiffusion](https://huggingface.co/frankjoshua/juggernautXL_version6Rundiffusion/tree/main) checkpoint.