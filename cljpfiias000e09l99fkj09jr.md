---
title: "5 of 10: Deno, ExpressJS, and Axios in the Docker Container."
datePublished: Wed Jul 05 2023 08:00:22 GMT+0000 (Coordinated Universal Time)
cuid: cljpfiias000e09l99fkj09jr
slug: 5-of-10-deno-in-the-docker-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999392482/5784da5d-150e-4bbe-8c48-17ccc2253bb3.png
tags: express, docker, axios, deno, apis-and-microservices

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | Deno | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)

## TL;DR.

Install Deno, ExpressJS, and Axios in a Docker container to build secure and efficient JavaScript and TypeScript applications, web applications, and APIs. Deno addresses Node.js shortcomings, ExpressJS streamlines development, and Axios enables easy HTTP requests management.

## An Introduction.

My previous post in this 8-part mini-series covered how I installed Docker Desktop locally and connected it to the remote Docker container. This time I'm going to install Deno, ExpressJS, and Axios into the Docker container.

> ***The purpose of this post is to present*** a way to install Deno, ExpressJS, and Axios into a Docker container.

Deno, ExpressJS, and Axios are fundamental to building APIs and microservices.

## The Big Picture.

The view of my services from up here in the clouds shows all of the servers that I've quietly assembled. There's Docker Desktop that runs on my local `workstation` and the Docker container that is running on my `homelab`. There's also the LXD (<mark>L</mark>inu<mark>XD</mark>aemon) manager that I use to spin up LXCs (<mark>L</mark>inu<mark>XC</mark>ontainers). This week, I'm installing Deno, ExpressJS, and Axios because these are the services I'll need to build the APIs and microservices that will be used by the 12 Startups.

## What is Deno?

Deno is a modern, secure, and efficient runtime for JavaScript and TypeScript applications. It was created by Ryan Dahl who is the original creator of Node.js. Node is another popular JS runtime environment. Deno is designed to address some of the shortcomings of Node.js. It provides developers with a more robust and secure platform for building applications. By leveraging the capabilities of Deno, I aim to create scalable and secure applications that can be easily deployed across the apps that make up the 12 Startups project.

## How Does Deno Work?

To understand how Deno works, it is essential to first recognize its primary goal, which is to address the shortcomings of Node.js. Deno enables the creation of scalable and secure applications that can be deployed as part of any project.

Deno is a runtime environment that executes JavaScript and TypeScript code outside of a web browser. It is built on top of the Chrome V8 JavaScript engine and utilizes the Rust programming language to ensure optimal performance and security. One of the key differences between Deno and Node.js is the way they handle modules. Deno employs the use of ES modules and fetches them directly from URLs, thereby eliminating the need for a package manager like NPM.

Furthermore, Deno places a strong emphasis on security by implementing a sandbox environment. This means that, by default, Deno applications cannot access the file system, network, or environment variables without explicit permission from the developer. This security feature is a significant improvement over Node.js, where applications have unrestricted access to system resources.

Deno provides a more secure and efficient runtime for JavaScript and TypeScript code while addressing the limitations of Node.js. By leveraging the capabilities of Deno, I can build most of the functionality that my apps need to meet their goals.

## How Do I Install Deno?

To install Deno in the Docker container, I follow these steps:

* From my workstation terminal (`Ctrl + Alt + T`), I login to the Docker container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> I replace the -p(ort) number and '?' above with the actual port number and IP address of the Docker container.

* Before installing any new software, it's always a good idea to update my container. I run the following command to clean out the APT, update my system's packages, upgrade the distro, and automatically remove any unrequired packages from the system:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I need Curl (a command-line tool for transferring data with URLs) and Unzip (a compression/decompression utility) to download, and install, Deno:
    

```plaintext
sudo apt install -y curl unzip
```

* I use Curl to download Deno's installation script by running the following command:
    

```plaintext
curl -fsSL https://deno.land/x/install/install.sh | sh
```

> This command downloads the installation script and pipes it to the shell, which then executes the script to install Deno on my system.

* After the installation is complete, I need to configure the environment variables to make Deno accessible from anywhere in my container:
    

```javascript
sudo nano ~/.bashrc
```

* I add the following lines to the `~/.bashrc`, `~/.zshrc`, or `~/.profile` file, depending on which shell I am using, save the changes, and close Nano:
    

```plaintext
export DENO_INSTALL="/home/$USER/.deno"
export PATH="$DENO_INSTALL/bin:$PATH"
```

> Replace `$USER` with my actual username.

* To apply the changes to my current session, I run the following command:
    

```plaintext
source ~/.bashrc
```

> If I'm using a different shell, I replace `.bashrc` with the appropriate configuration file (e.g., `.zshrc` or `.profile`).

* To confirm that Deno has been successfully installed, I run the following command:
    

```plaintext
deno --version
```

> If the installation was successful, this command will display the Deno version.

I now have Deno installed in the Docker container. Building secure and efficient JavaScript and TypeScript applications is now one step closer.

## What is ExpressJS?

ExpressJS is a powerful and flexible web application framework for Node.js and Deno. It is designed to streamline the development of web applications and APIs by providing a robust set of features and utilities. As a minimal and unopinionated framework, ExpressJS allows me to build applications with ease and flexibility, without imposing any specific architectural patterns or constraints. This makes it an ideal choice for creating a wide range of applications, from simple single-page websites to complex, data-driven web applications and APIs.

## How Does ExpressJS Work?

At its core, ExpressJS is a lightweight, minimalist web application framework, built on top of the Node.js and Deno platforms. It streamlines the process of creating web applications and APIs by offering a robust set of features and tools, while still allowing me to maintain full control over my application's structure and design. This is achieved through a modular architecture that promotes the use of middleware functions, which can be easily plugged into the application as needed.

Middleware functions are essentially building blocks that can be combined and customized to create a tailored application structure. They are responsible for handling various aspects of the application, such as routing, authentication, and error handling, among others. By leveraging these middleware functions, I can efficiently implement the desired functionality and features in my applications without being restricted by a predefined architecture.

Furthermore, ExpressJS simplifies the process of handling HTTP requests and responses by providing a straightforward API for defining routes and their corresponding request handlers. This allows me to easily map different URLs to specific functions within the application, ensuring a seamless user experience and efficient navigation.

## How Do I Use ExpressJS?

ExpressJS is a powerful and flexible web application framework. It simplifies the process of handling HTTP requests and responses. This framework provides a straightforward API for defining routes and their corresponding request handlers. This feature enables me to map various URLs to specific functions within my applications. It ensures a seamless user experience and efficient navigation throughout my apps. Follow these steps to use the ExpressJS framework.

* First, I login to the Docker container:
    

```plaintext
ssh -p '4444' 'yt@192.168.?.?'
```

> I replace the -p(ort) number and '?' above with the actual port number and IP address of the Docker container.

* I update the container:
    

```plaintext
sudo apt clean && sudo apt update && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

* I make a test directory:
    

```plaintext
mkdir ~/test
```

* I navigate to the test directory:
    

```plaintext
cd ~/test
```

* Once I'm in the directory, I create a file called main.ts:
    

```plaintext
touch main.ts
```

* In `main.ts`, I create a simple server:
    

```javascript
import express from "npm:express@4.18.2";

const app = express();

app.get("/", (req, res) => {
  res.send("Welcome to the Dinosaur API!");
});

app.listen(8000);
```

* I run the server:
    

```plaintext
deno run -A main.ts
```

* I point my browser to [`192.168.?.?:8000`](http://localhost:8000) where I see:
    

```plaintext
Welcome to the Dinosaur API!
```

I can now use ExpressJS to easily create my web applications.

> **Attribution:**
> 
> [https://deno.land/manual@v1.35.0/node/how\_to\_with\_npm/express](https://deno.land/manual@v1.35.0/node/how_to_with_npm/express)

## What is Axios?

I am now ready to begin defining routes, request handlers, and other essential components to build a fully functional web application using the ExpressJS framework. It is important to explore additional tools and libraries that can further enhance my application's capabilities. One such library is Axios.

Axios is a widely-used, feature-rich, and highly efficient JavaScript library designed for making HTTP requests from the browser, Node.js, and Deno environments. It is built on top of the XMLHttpRequest object in the browser and the http module in Node.js, which allows developers to seamlessly perform asynchronous operations, such as fetching data from APIs or submitting form data, within their web applications. Axios provides a simple, promise-based API that enables me to easily manage and handle HTTP requests and responses, while also offering a range of advanced features like intercepting requests and responses, cancelling requests, and automatic transformations of JSON data. By incorporating Axios into my ExpressJS-based web applications, I can effectively harness its powerful capabilities to create even better, more efficient apps.

## How Does Axios Work?

Axios is designed to facilitate seamless HTTP communication between the client and server. By incorporating Axios into ExpressJS-based web applications, developers can take advantage of its advanced features, such as intercepting requests and responses, cancelling requests, and automatic JSON data transformations. This, in turn, leads to the creation of more robust, efficient, and user-friendly web applications.

## How Do I Import Axios?

To begin, I will need to import Axios as a dependency in my project. I can do this because Deno supports `npm:specifiers`.

* I connect my terminal (`CTRL` + `ALT` + `T`) to the Docker container.
    
* I navigate to my project directory called 'test'.
    
* To import Axios into my ExpressJS application, I add the following line to the top of the `main.ts` file:
    

```javascript
import axios from "npm:axios@^1.4.0"; /* As of July 2023 */
```

Now that Axios is imported, I can start using its advanced features in my ExpressJS-based web application. For example, I can make HTTP requests, intercept requests and responses, cancel requests, and automatically transform JSON data.

## The Results.

Deno, ExpressJS, and Axios allows me to build JavaScript and TypeScript applications, web applications, and APIs. Deno addresses Node.js shortcomings, ExpressJS streamlines services development, and Axios simplifies HTTP requests management. Together, these tools provide a powerful environment for creating APIs and microservices.

## In Conclusion.

That's where I'm headed, isn't it? Tumbling head-first into microservices and APIs. Composable architecture and microservices architecture are two environments where Node, Deno, ExpressJS, and Axios really shines.

And, as developers, we like really shiny things.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | Deno | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | [CrowdSec](https://solodev.app/10-of-10-crowdsec-in-the-docker-container)