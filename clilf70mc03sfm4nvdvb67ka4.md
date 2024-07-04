---
title: "1 of 10: My First Homelab."
seoDescription: "SoloDev sets up a remote homelab for his startup, emphasizing security, Linux distros, LXD container management, and LinuX Containers."
datePublished: Wed Jun 07 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clilf70mc03sfm4nvdvb67ka4
slug: 1-of-10-my-first-homelab
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999230448/9e501d99-4071-4a1f-8549-78c34d876747.png
tags: ubuntu, homelab, 12-startups-in-12-months, company-function, business-core

---

Homelab | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR;

I'm here to describe my remote `homelab` system, which is a key feature of my tech startup. I'll also share my plans for the future, describe how I'll meet my goals, and show how the `homelab` fits into my plans.

## An Introduction.

![intro](https://images.pexels.com/photos/6980429/pexels-photo-6980429.jpeg?cs=srgb&dl=pexels-ann-h-6980429.jpg&fm=jpg&w=640&h=427 align="left")

My name is Brian and I'm a solo developer. Being a SoloDev has its' advantages (I get to try everything, *especially* the interesting bits) but there are many disadvantages, too (like having to learn everything, *including* the boring bits).

Building a remote `homelab` system is new to me. That's why I'll be sharing useful details about how things will be set up.

> The purpose of this post is to present my purpose for using a homelab.

## Using Multiple Computers.

![two computers](https://images.pexels.com/photos/115655/pexels-photo-115655.jpeg?cs=srgb&dl=pexels-lee-campbell-115655.jpg&fm=jpg&w=640&h=427 align="left")

I'm pretty good at using different operating systems, like Windows and Ubuntu. I'm also happy to use remote services like [Linode](https://www.linode.com/), [Digital Ocean](https://www.digitalocean.com/), and [Heroku](https://www.heroku.com/). However, hosting and testing my programs within my *own* LAN, on my own local area network, is a novel idea to me. Although I'm quite proficient at SysOps (systems operations), which means building a remote `homelab` system *should* be easy, I've never *actually* built one before so I'll have to see how things turn out.

I’m going to use two separate computers: A local `workstation` system and a remote `homelab` system. I could have used a single computer and got the same results, but I'm using two machines because there is *also* a networking component that needs investigating.

Throughout this blog, I will be referring to the local `workstation` and remote `homelab`. Although technically correct, these two machines are no more than two feet away from each other. They communicate over ethernet cables through a 2.5Gb/s router, but they're so close I can turn them on without leaving my chair.

| Description | Local Workstation PC | Remote Homelab NUC |
| --- | --- | --- |
| CPU | AMD Ryzen 5 2600 | Intel Core i3-10110U |
| RAM | 16GB (2x8GB) | 40GB (1x8GB, 1x32GB) |
| Main Storage | 1TB M.2 SSD | 256GB M.2 SSD |
| Base Clock | 3.4GHz | 2.1GHz |
| Boost Clock | 3.9GHz | 4.1GHz |
| Cores | 6 | 2 |
| Threads | 12 | 4 |

There are many use cases for building a remote `homelab` system. Creating one may be easy for me, but the value it *might* bring to my development pipeline *could* be enormous.

## Using Linux Distributions.

![terminal](https://images.pexels.com/photos/207580/pexels-photo-207580.jpeg?cs=srgb&dl=pexels-pixabay-207580.jpg&fm=jpg&w=640&h=480 align="left")

I use Linux distributions on both the remote `homelab` and the local `workstation`. I started using CentOS around 2015 but then switched to Ubuntu sometime in 2018. My reason for switching to Linux was simple: Publishing to the web is easier if I know how to use the OS that "is used to power 96.3% of the world's top web servers."

This now begs the question: What's my main reason for deploying a remote `homelab` system?

## The Purpose of my Remote Homelab.

![homelab](https://images.pexels.com/photos/442150/pexels-photo-442150.jpeg?cs=srgb&dl=pexels-field-engineer-442150.jpg&fm=jpg&w=640&h=427 align="left")

I've been interested in computers, and programming, since the late 1980s when I first used QBASIC. Obviously, things have changed since then.

## The 12 Startups Challenge.

In my last post, I introduced [the 12 Startups I want to build](https://solodev.app/the-12-startups-in-12-months-challenge). To build 12 Startups, I will need a foundation that is stable yet flexible, strong yet pliable, and adaptable yet resilient. These requirements provide design targets that will govern my development process. There are many factors to consider when modelling a Technical Design, but there are common architectures that can help with creating a solid strategy. Some of these architectures include:

* The Monolith architecture,
    
* The Microservices architecture,
    
* The Composable architecture, and
    
* The Servless architecture.
    

I'm leaning toward using Composable architecture, which is based on MACH (Microservices, API, Cloud, Headless). I've never used serverless or the cloud: My projects never needed these technologies. Also, I tend to stick with what I know.

## The Future is Now, The Now is Here.

For those paying attention, what I'm saying is "The Future is Here."

It's taken A. VERY. LONG. TIME. to get to a point where modern tools can help me build the stuff that is in my head.

Machine learning, deep learning, artificial intelligence, and prompt engineering are beginning to show promising results. As of this writing, everyone is losing their minds over GPT-4 (and there are rumours that GPT-5 will be video-centric). The real magic, however, is the algorithms that build these models.

## Prototyping and Experiments.

Another reason for this series of posts is to show how I’d build prototype mechanisms for hosting machine-learning models. Building these models requires more resources than the local `workstation` or remote `homelab` can provide. However, designing a system for building AI models is a great topic... For another day. For now, I just want to host these models.

Did you notice that, in the last paragraph, I used the word "prototype"? I'm a fan of experimental systems but there are costs with running these kinds of exercises. I'm constantly repeating processes with slight variations to find closer approximations to a solution. I'm always defining a problem, or a solution, in terms of a simpler version of itself. I'm constantly changing my equipment. I'll replace the dotenv file that controls environment constants. I'll alter the processing order based on the results that I generate. I'd even revise my assumptions if that'll get me closer to an ideal outcome. All of this tinkering generally results in two outcomes: Lots of lab results, and a somewhat unstable system.

## System Stability.

I rely on two tools that help with restoring my systems to their stable conditions.

The first tool is Clonezilla Live. I use it to easily image, i.e. clone, individual machines. Clonezilla Live only works when the PC is offline because it needs to boot from a CD/DVD or USB flash drive. That's why I only use it when I've made, or am about to make, significant software changes to an operating system. Clonezilla Live is beyond the scope of these posts.

The other tool is LXD, pronounced: "lexdee". Note: The next post in this series will describe how I [install, and use, LXD](https://solodev.app/lxd-on-my-homelab) to my advantage.

The question is: What's the point? Why go to all the trouble of setting up a remote `homelab` system?

The simple answer is: I want to build my own tech startup. I want to meet the 12 Startups challenge. I want to use AI models. I want to create my own apps. And I want to use these apps to generate an income.

## DigitalCore: An Overview of My Business.

![laptop](https://images.pexels.com/photos/2312369/pexels-photo-2312369.jpeg?cs=srgb&dl=pexels-andrew-neel-2312369.jpg&fm=jpg&w=640&h=427 align="left")

The key function of every company is to provide products and services to its customers and clients. Digital Core (NZ) Limited is my tech startup and is NOT in a position to generate a profit... because it's NOT closing sales... because it does NOT have any products, or services, to sell.

As a solo developer, I need to turn my Technical Designs and Product Designs into artefacts with value.

As Employee Number One (of one) at my startup, I also need to assume the responsibilities of a manager and company director.

Just to clarify: I’m the *only* employee at my startup so I'm the *only* one who is doing *any of the work*.

## DigitalCore: The Core of My Business.

Being a systems analyst, system designer, product designer, programmer, business manager, bookkeeper, salesperson, and company director imposes HUGE constraints on achieving my professional goals in a timely manner. My goals include making money, spending money, and making *more* money. As a result, I need tools that help with:

* Working precisely,
    
* Working quickly, and
    
* Working economically.
    

Having said that, I need to understand the difference between the function of my company and its core business. After all, I don't want to build any tools that achieve the wrong outcomes. Take this list, for example:

| Company | Company Function | Business Core |
| --- | --- | --- |
| McDonald's (fast-food chain) | Resturant | Real estate |
| Facebook | Social platform | Advertising |
| Google | Search engine | Advertising |
| DigitalCore (my startup) | App development | Advertising |

All of my products include *at least one* specialist feature that helps differentiate them from the competition. However, my products also include the same bog-standard features as every other app (Join, Login, Subscribe, etc.) The *ACTUAL* purpose of my products is to *satisfy my core business objective*: To sell advertisements (although a few of my apps go beyond this income stream). It's disappointing that my core business is the same as everyone else. However, it's a core business objective that is easy to understand... And it works when applied correctly.

To achieve my core business objective, I need a stable, adaptable, and repeatable system on which to build, test, and deliver my products. I also need this platform to promote SECURITY as *the PRIMARY consideration*. I need tools that ensure development pipelines and delivery platforms place security at *the forefront of every publishing cycle*.

## Tools, Pipelines, and Security.

![security](https://images.pexels.com/photos/60504/security-protection-anti-virus-software-60504.jpeg?cs=srgb&dl=pexels-pixabay-60504.jpg&fm=jpg&w=640&h=427 align="left")

The tools that I use, the order in which I use them, and how these tools help to build secure mechanisms, will go a long way to ensuring positive user experiences (even though my security practices will be transparent to the user) while *also* complying with international policies regarding personal data collection, retention, and erasure.

Therefore, the first *technical* step to achieving this outcome is to harden (or *at least* start the process of hardening) my remote `homelab`. Later steps will include hardening the containers that run on my remote `homelab`.

## Blog Direction.

![compass](https://images.pexels.com/photos/3832684/pexels-photo-3832684.jpeg?cs=srgb&dl=pexels-joshua-woroniecki-3832684.jpg&fm=jpg&w=640&h=409 align="left")

I want to take a moment to clarify the direction of this blog. I'll try to cover the technical aspects of setting up and using a remote `homelab`. I'll also recount the business practices that I consider essential. I want to include all the steps I take when completing a specific task, but cannot respond to requests for help due to my lack of resources and experience. (I'd like to help but, at this time, I can barely help myself.)

## The Results.

This post introduced the concept of a remote `homelab` system, its purpose regarding my tech startup, and the importance of security in the development process. My blog aims to cover the technical aspects of setting up a remote `homelab` system, along with essential business practices. Future posts will include the commands I use for deploying different services, with a focus on using LXD and LinuX Containers on my remote `homelab` system.

## In Conclusion.

![conclusion](https://images.pexels.com/photos/6980525/pexels-photo-6980525.jpeg?cs=srgb&dl=pexels-ann-h-6980525.jpg&fm=jpg&w=640&h=427 align="left")

This post covered:

* The technologies I use,
    
* The *main* purpose of my remote `homelab` system,
    
* The function and objective of my startup,
    
* The reasons for hardening a system, and
    
* The direction this series will take.
    

I hope you found this brief useful. The rest of the posts in this series will be very hands-on and comes with plenty of examples.

Be sure to check out the next post in this series where I [setup, and use, LXD](https://solodev.app/lxd-on-my-homelab) on my remote `homelab` system.

Until next time: Be safe, be kind, be awesome.

Homelab | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)