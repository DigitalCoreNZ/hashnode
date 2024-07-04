---
title: "Installing Krita 5.2+ Image Editor for ComfyUI."
datePublished: Wed Jan 17 2024 09:00:23 GMT+0000 (Coordinated Universal Time)
cuid: clrhjyn6a00050albhf2p3xld
slug: installing-krita-image-editor-for-comfyui
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704798165391/dce55705-2ae7-45a4-9752-ca190e301e5e.png
tags: comfyui, ai-image-editor, krita, image-editor, ai-image, ai-images

---

# TL;DR.

This post provides a step-by-step guide on how to set up the Krita 5.2+ image editor so it connects to a Local ComfyUI Server running on my Ubuntu distro. It also covers the downloading and setup of the Generative AI plugin for Krita, running the plugin script that it installs all the Models, and using the ComfyUI Manager to install the Custom Nodes. This guide also shows the results of my tests.

> **Attributions:**
> 
> [https://krita.org/en/](https://krita.org/en/) ***↗,***
> 
> [https://github.com/Acly/krita-ai-diffusion#installation](https://github.com/Acly/krita-ai-diffusion#installation) ***↗, and***
> 
> [https://github.com/Acly/krita-ai-diffusion/blob/main/doc/comfy-requirements.md#-download-script](https://github.com/Acly/krita-ai-diffusion/blob/main/doc/comfy-requirements.md#-download-script) ***↗.***

# An Introduction.

As I mentioned in a previous post, ComfyUI and SDXL (Stable Diffusion XL) are a Big Deal, but an image editor adds a new level of AWESOME to local, AI image generation.

> The purpose of this post is to add an image editor to a local, AI image generator.

# The Big Picture.

There is an adage that declares "A picture is worth a thousand words." This statement means "Seeing something is better for learning than having it described." Using AI images in my posts and projects might add "worth" to my work, especially if these pictures help my "learning" process.

# Prerequisites.

* A Linux-based distro (I use Ubuntu),
    
* Anaconda, and
    
* ComfyUI.
    

# Downloading the Krita 5.2+ Image Editor.

* I visit the homepage and download the Krita AppImage package:
    

```bash
https://krita.org/en/download/krita-desktop/
```

> NOTE: An AppImage contains an app and the files it needs to run. It has no dependencies other than what is in the targeted base operating system(s).

* I change to the `Downloads` directory:
    

```plaintext
cd ~/Downloads
```

* I make the AppImage package an executable file:
    

```bash
chmod u+x krita-5.2.2-x86_64.appimage
```

* I create a `symlink` (symbolic link) from the AppImage package to the `Desktop`:
    

```plaintext
ln -s /media/brian/Downloads/Ubuntu/Krita/krita-5.2.2-x86_64.appimage ~/Desktop/'Krita 5.2.2'
```

> NOTE: This symlink is crafted to work with the location of the AppImage package.

* I run Krita by right-clicking on the Desktop symlink and selecting "Run as a program" from the pop-up menu. (As a result, certain directories are made.)
    
* I exit Krita.
    

# Installing Generative AI for Krita.

* I download the plugin for Krita:
    

```plaintext
https://github.com/Acly/krita-ai-diffusion/releases/latest
```

* I unpack the zip file to the (newly made) `pykrita` directory, e.g.:
    

```plaintext
unzip /media/brian/Downloads/Ubuntu/Krita/krita_ai_diffusion-1.12.0.zip -d ~/.local/share/krita/pykrita
```

> NOTE 1: Again, this command is unique to my setup.

> NOTE 2: I installed unzip [in an earlier post](https://solodev.app/5-of-10-deno-in-the-docker-container#heading-how-do-i-install-deno) (`sudo apt install -y unzip`).

# Installing the ComfyUI Custom Nodes.

I start the (comfyui) environment:

```plaintext
conda activate comfyui
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

* I open ComfyUI in a browser:
    

```bash
http://127.0.0.1:8188
```

* I open the Manager and click on the "Install Custom Nodes" button.
    
* I install these custom nodes:
    
    * [**ComfyUI's ControlNet Auxiliary Preprocessors**](https://github.com/Fannovel16/comfyui_controlnet_aux) **(search: fann),**
        
    * [**ComfyUI\_IPAdapter\_plus**](https://github.com/cubiq/ComfyUI_IPAdapter_plus) **(search:** cubiq),
        
    * [**UltimateSDUpscale**](https://github.com/ssitu/ComfyUI_UltimateSDUpscale) **(search:** ssitu), and
        
    * [**ComfyUI Nodes for External Tooling**](https://github.com/Acly/comfyui-tooling-nodes) **(search:** acly).
        

# Installing the ComfyUI Models for Krita.

* I stop the ComfyUI server:
    

```plaintext
CTRL + C
```

* I install the dependencies:
    

```bash
python -m pip install aiohttp tqdm
```

* I change to the `ai_diffusion` directory:
    

```bash
cd ~/.local/share/krita/pykrita/ai_diffusion
```

* I run the `download_models.py` module and add those models to the `ComfyUI` installation:
    

```bash
python ./download_models.py ~/ComfyUI
```

> NOTE: It took me approximately 15-minutes to download these models.

* I exit the (comfyui) environment:
    

```plaintext
conda activate
```

* I return to the (comfyui) environment:
    

```plaintext
conda activate comfyui
```

* I start the ComfyUI server:
    

```plaintext
python3 main.py
```

# Setting Up Krita.

* I run Krita by right-clicking on the Desktop symlink and selecting "Run as a program" from the pop-up menu.
    
* I enable the plugin in Krita:
    

```plaintext
Settings ‣ Configure Krita ‣ Python Plugins Manager
```

* I restart Krita.
    
* I create a new document.
    
* I enable the plugin dock:
    

```plaintext
Settings ‣ Dockers ‣ AI Image Generation
```

* I click the gears icon in the top-right of the "AI Image Generation" dock.
    
* I click the "Connection" option in the left panel.
    
* I choose the "Connect to external Server (local or remote)" radio button.
    
* I set the "Server URL" to `127.0.0.1:8188` and click the "Connect" button.
    

> NOTE: This is the same URL for displaying ComfyUI in a browser.

* I test Krita when the green "Connected" message shows.
    

> NOTE: The Server URL and green message may already be set up.

* I click the "OK" button.
    

# Testing Krita.

* I click the drop-down menu in the top-left of the "AI Image Generation" dock and select the "Live" option (which looks like a play button.)
    
* I click the actual "Live" button called "Start/stop live preview."
    
* I add a prompt.
    
* I draw on the canvas and watch the "AI Image Generation" dock interpret my drawing.
    

# The Results.

I sat down and drew a quick sketch.

## Before.

Here's the prompt that goes with my quick sketch:

a cabin, in a green field, by a river, mountains in the background, blue skies, fluffy clouds...

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704584286033/efe3a971-6aa6-4d66-839f-2eaf53595d3b.png align="center")

## After #1: Cabin by the River.

...and here's (one of) the results. But I want to include a row boat, too.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704584324688/41544538-d5bc-4e78-9d1b-80a270246cb2.png align="center")

## After #2: Row Boat by the Cabin.

With a little bit of scaling and tiny touch of feathering, I now have a row boat.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1704588105268/9ea15007-107e-4327-8327-cad0a7cbabd1.png align="center")

# In Conclusion.

This is how I added a new level of AWESOME to my locally-generated AI images. I set up the Krita 5.2+ image editor and connected it to a local ComfyUI Server running on my Ubuntu `workstation`. The results have changed the game for me. Combining Krita, ComfyUI and SDXL is a Big Deal. They've taken my workflow to a whole new level, especially if I use AI images in my posts and projects. All I did was download, and set up, the Generative AI plugin for Krita, installed all the Models, and used the ComfyUI Manager to install the Custom Nodes.

My test results were mind-melting! A quick sketch of a cabin by the river transformed into a stunning AI-generated image. I'm now ready to bring more value to my work, thanks to these tools.

Have you levelled up your AI image generation game? Are you using AI images? Does it make a difference to your workflow? Leave your thoughts below!

Until next time: Be safe, be kind, be awesome.