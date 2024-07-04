---
title: "7 of 10: Portainer in the Docker Container."
datePublished: Mon Jul 10 2023 08:00:42 GMT+0000 (Coordinated Universal Time)
cuid: cljwkq6yw0h80zynv240t90z7
slug: 7-of-10-portainer-in-the-docker-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999457880/f7ad0706-6b84-413a-aa10-7a6cf1e492ad.png
tags: docker, portainer

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | Portainer | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

I will install Portainer in a remote Docker container to manage and monitor my Docker environment. Portainer will be accessible at http://localhost:9000 or http://&lt;server\_ip&gt;:9000.

## An Introduction.

My previous post in this 8-part mini-series covered how I installed Deno, ExpressJS, and Axios in the remote Docker container. This time, I'm going to show how I install Portainer in the remote Docker container.

> The purpose of this post is to demonstrate how to install Portainer on a Docker system.

## The Big Picture.

Sometimes, it's the little things.

I'm bombastic in my posts. I'm so busy showing off that sometimes the message gets buried in all the noise. (BTW: being bombastic is a bad thing.)

I'm going to try something different.

Welcome to my first micro post.

## Installing Portainer CE Server.

* From a terminal (`CTRL` + `ALT` + `T`) that is connected to the Docker container, I create a persistent Docker volume to store Portainer's data:
    

```plaintext
docker volume create portainer_data
```

* I use the Docker command to pull, and run, the Portainer image while including a few setup flags:
    

```plaintext
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
```

This command will:

* Run the Portainer container in detached mode `-d`
    
* Expose Port 9000 `-p 9000:9000`
    
* Name the container `portainer`  
    \--restart=always\` to restart the container on reboot
    
* Mount the Docker socket `-v /var/run/docker.sock:/var/run/docker.sock`
    
* Mount the data volume `-v portainer_data:/data`
    
* Use the Portainer Community Edition image `portainer/portainer-ce`
    
* Access the Portainer UI by navigating to [`http://localhost:9000`](http://localhost:9000) in your browser.
    
* Set the admin password during the initial setup.
    
* The Portainer UI will show you the `local` environment containing your Docker containers, images, volumes, etc.
    

I can then use Portainer to manage, and monitor, my Docker environment. After installation, the Portainer UI will be available at [`http://localhost:9000`](http://localhost:9000) or `http://<server_ip>:9000`.

> Attribution:
> 
> [https://docs.portainer.io/start/install-ce/server](https://docs.portainer.io/start/install-ce/server)

## The Results.

I demonstrated how to install Portainer in a remote Docker container. Portainer is used to manage and monitor my Docker environment. By following the steps outlined, I can easily set up Portainer and access its UI to gain insight into my containerized applications. With this powerful tool, I can simplify container management and enhance my overall experience in working with Docker.

## In Conclusion.

You know what? Cutting out the drivel and sticking to the point helped get this post down to a 3-minute read time.

Here's my new rule for writing posts: Cut the crap and stick to the point.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | Portainer | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)