---
title: "Installing DaVinci Resolve 19 Studio on Ubuntu 24.04."
datePublished: Thu Oct 10 2024 09:00:20 GMT+0000 (Coordinated Universal Time)
cuid: cm232j1bv000f09i87q3hdvie
slug: installing-davinci-resolve-19-studio-on-ubuntu-2404
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1728524560078/3a997ce1-f641-4b4a-8db5-e4937fc3ae01.png
tags: video-editing, video-production, video-post-production, motion-graphics, blackmagic-design, davinci-resolve-19, davinci-resolve-19-studio, colour-grading, video-post, video-content-creation, film-editing, creative-editing, professional-video-editing, audio-post-production, linux-video-editing

---

# TL;DR.

This post provides a step-by-step guide to installing DaVinci Resolve 19 Studio on Ubuntu 24.04. It covers downloading the software, preparing the download, ensuring compatibility with necessary libraries, and updating my drivers. By following these instructions, I can effectively set up DaVinci Resolve for professional video editing on my Linux system.

> NOTE: This guide has only been tested with the Studio version of Resolve. Let me know, in the comments below, if this process also works with the FREE version of DaVinci Resolve. Thank-you.

> **Attributions:**
> 
> [hackmd.io](https://hackmd.io/@brlin/install-davinci-resolve-19-on-ubuntu-2404) ***↗,***
> 
> [how2shout.com](https://linux.how2shout.com/how-to-install-davinci-resolve-on-ubuntu-22-04-lts-jammy/) ***↗.***

---

# An Introduction.

Resolve a a great tool for performing many video post production activities.

> The purpose of this post is to describe how to install Resolve Studio on Ubuntu.

---

# The Big Picture.

DaVinci Resolve is traditionally thought of as an industry-standard colour correction and colour grading system. But since 2009, Resolve has slowly evolved into a complete, powerful, video production tool with features like:

* Video editing,
    
* Special effects,
    
* Motion graphics, and
    
* Audio post-production.
    

For professional film productions, the Studio version of Resolve actively supports the workflows of many on-set DITs (Digital Imaging Technicians) as well as activities like editing, colour correction, colour grading, visual effects, green screen work, matte paintings, sound effects, audio post-processing and balancing, and audio mixing.

---

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

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

# What is DaVinci Resolve?

DaVinci Resolve is a video editing, colour grading and correction, visual effects, motion graphics, and audio post-production application for macOS, Windows, and Linux. It was originally developed by da Vinci Systems as da Vinci Resolve. Then in 2009, when da Vinci Systems was acquired by Blackmagic Design, the application was rebranded as DaVinci Resolve.

[https://www.blackmagicdesign.com/](https://www.blackmagicdesign.com/%E2%86%97)***↗.***

## Downloading DaVinci Resolve.

* I download the latest copy of DaVinci Resolve 19 Studio:
    

[https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion](https://www.blackmagicdesign.com/au/support/family/davinci-resolve-and-fusion)

## Unzipping the Downloaded File.

* In a terminal, I go to the Downloads directory:
    

```bash
cd ~/Downloads
```

* I check if the downloaded ZIP file exists:
    

```bash
ls
```

* I install UNZIP (if required):
    

```bash
sudo apt install unzip
```

* I extract the contents of the ZIP file:
    

```bash
sudo unzip ./DaVinci_Resolve_*_Linux.zip
```

## Changing the Mode of the RUN File.

* I change the mode of the extracted RUN file to an executable:
    

```bash
sudo chmod +x ./DaVinci_Resolve_Studio_*_Linux.run
```

## Installing the Software.

* I install the software:
    

```bash
sudo SKIP_PACKAGE_CHECK=1 ./DaVinci_Resolve_*_Linux.run -i
```

> NOTE: This command does not check for missing libraries during the installation.

* I change to the `libs` directory:
    

```bash
cd /opt/resolve/libs
```

* I make a new directory called `disabled_libs`:
    

```bash
sudo mkdir ./disabled_libs
```

* I move the `libglib`, `libgio`, and `libgmodule` into the `disabled_libs` directory:
    

```bash
sudo mv libglib-2.0.so* libgio-2.0.so* libgmodule-2.0.so* disabled_libs/
```

> NOTE: Moving these libraries forces Resolve to use the Ubuntu 24.04LTS libraries.

* I update my NVIDIA drivers, if required:
    

```bash
sudo apt install -y nvidia-driver-550
```

> NOTE: Resolve requires the 550 driver or later.

* I run the application:
    

```bash
/opt/resolve/bin/resolve
```

---

# The Results.

Installing DaVinci Resolve 19 Studio on Ubuntu 24.04 involves several steps, including downloading the Resolve software and ensuring compatibility with the system drivers and libraries. By following the outlined process, I can successfully set up this powerful video editing tool on my Linux system. With DaVinci Resolve, I can enhance my video editing capabilities and create professional-level video content.

---

# In Conclusion.

I discovered how to install DaVinci Resolve 19 Studio on Ubuntu 24.04!

DaVinci Resolve is a powerhouse application (for video editing, colour grading, visual effects, and more) from Blackmagic Design.

Here's my quick guide to getting started:

1. I use a Debian-based Linux distro called Ubuntu.
    
2. I update my base system via the terminal.
    
3. I download the latest version of DaVinci Resolve 19 Studio from the Blackmagic Design website.
    
4. I unzip the downloaded file.
    
5. I make the unzipped RUN file executable.
    
6. I install the software while repressing error messages.
    
7. I move specific libraries to another directory.
    
8. I update my NVIDIA drivers to 550 or later.
    
9. I run the application and start creating professional-level video content!
    

By following these steps, I can harness the full potential of DaVinci Resolve on my Linux system.

Are you ready to transform your video editing experience? What projects are you excited to work on with DaVinci Resolve? Let me know in the comments!

Until next time: Be safe, be kind, be awesome.

---

# Hash Tags.

#BlackmagicDesign #DaVinciResolve19 #DaVinciResolve19Studio #VideoEditing #ColourGrading #VideoProduction #VideoPost #VideoPostProduction #VideoContentCreation #FilmEditing #CreativeEditing #ProfessionalVideoEditing #MotionGraphics #AudioPostProduction #LinuxVideoEditing