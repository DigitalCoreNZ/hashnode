---
title: "12S: Initial Technology Design."
datePublished: Mon Jul 24 2023 08:00:10 GMT+0000 (Coordinated Universal Time)
cuid: clkgkvfol000709l39aavcb09
slug: 12s-initial-technology-design
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702334766851/f4ac7894-ff9e-4181-b4bd-3d19e62c8375.png
tags: lxc, containers, lxd, 12-startups-in-12-months, technical-design

---

## TL;DR.

A structural design for the 12 Startups (12S) project is proposed, using technologies like React Native, Expo, and Docker to create a scalable, adaptable, and efficient system. The design process involves multiple iterations, addressing challenges such as traffic management, app publishing, and WASM integration. Key performance metrics and quality maintenance strategies are also discussed.

## An Introduction.

A structural design process sets the stage for successful application development. Like the blueprint for a building, a structural design will:

* Guide me as I code,
    
* Prevent me from making costly mistakes, and
    
* Ensures that my apps comply with a minimum set of safety requirements.
    

The design process allows for the consideration of important factors such as scalability, maintainability, and security right from the begining. This proactive approach to structural foundations can save a lot of time and resources down the line, as a template reduces the likelihood of having to make major changes during the development of an app.

Moreover, a well-thought-out structural design can greatly enhance the quality of the final product. A solid foundation ensures that all the hosted apps are robust, user-friendly, and meets the needs of its users.

> The purpose of this post is to propose a structual design for the 12 Startups Project.

## The Big Picture.

Yes, I wrote a post about [creating, and using, a technical design](https://solodev.app/12s-a-blueprint-for-technical-design). At the time, I was advocating for the use of the Qwik framework. I've since moved on: My new favourite tech is the Expo platform running on React Native. (I'll switch to Tauri once native mobile deployment is stablised.)

Design diagrams are handy when I want to explain what I'm doing to other programmers, but creating an *actual* design can be a painful process. There's all the technical details that need to be documented *and* proven *and* evaluated, there's my (undocumented!!) past projects that are vaguely similar to the one that is in front of me, and then there are the minutiae that will turn the tide on any decisions I'll be making at any given moment. Iterating over a design (especially on paper, or the electronic version thereof) can *also* be liberating. I always feel better after committing extra details to the next design.

One of the more positive aspects of the design process is that it provides a clear roadmap for the development of a project. By outlining the system architecture, defining the relationships between different components, and specifying the functionality of each component, the design presents all stakeholders with a shared understanding of what the final product should be.

Creating a design usually starts with: What is the purpose of the app? Of course, I'm not building an app. I'm building a frame on which to hang my apps. Therefore, a slightly altered question is: What is the purpose of the structure on which my apps will run?

## The Purpose of My Stack?

The purpose of the 12S structural design is to define a common development and deployment scheme. This commonality across all the apps will provide a known starting point that will be easy to learn and adopt.

## How Should I Design My Stack?

Consider the following requirements:

* Native publishing to the iOS App Store and the Android Play Store,
    
* Native publishing to the web (e.g. Netlify, Linode, Digital Ocean, etc.), and
    
* WASM binary integration.
    

Adopting, and using, tools that deploy an app across multiple platforms is definitely worth embracing. Expo with React Native gets my approval.

(Later, I will figure out how to integrate Tauri into the deployment strategy. Or maybe I'll switch to Tauri when it supports native mobile deployment.)

Personally, I think my stack should be decomposed into separate containers, i.e. to better reflect the distributed and isolated functionality of a microservice layout.

### Draft v0.0.1.

This is my first design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690180873125/a572f399-048c-4355-b55c-e7b53aca89cc.png align="center")

This is a bad design. Really, *really* bad. I can't even remember why I wanted to separate the microservices from the WASM modules. Oh, and this picture is upside down. There's a convention where the client/cloud is at the top of the graphic. Luckily, software design is an iterative process. I hoped the design would improve as I added new items while fixing existing elements.

### Draft v0.0.2.

Here is my second design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690181012555/fee2bcf0-0b12-424c-bdba-0c567e1fe391.png align="center")

I am throwing ideas at the screen to see what sticks. Yes, I have created another *really* bad design. Here, I'm looking at wrapping each app in it's own container. I also lost my requesting platforms (macOS, iOS, Chrome, and Firefox). But I gained an app container and a data container.

### Draft v0.0. 3.

Take a look at my third design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690181101169/756e6079-d73e-450c-8b3b-15be526fa633.png align="center")

This image describes a request coming in from a browser. However, I see a number of problems.

There are three containers (app, api, and data). The requests from the app container and the responses from the data container all pass through the api container. Luckily, I have an idea that may reduce the traffic through this choke point. I also have other solutions to potential problems that I'd also like to try out. And finally, I'm not sure which services are running in each container.

### Draft v0.0.4.

Here's my forth pass at a design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690181167814/14951279-a73e-485d-b316-b4649f834763.png align="left")

This time, I've added more detail. Specifically, every container has a better (read: shorter) name, and I've added a new container called "proxy".

The design now includes a small list of the main services within each container.

One of the original problems still exists, though: The api microservices container is still pulling double duty, i.e. it's responding to app requests while also passing data responses.

### Draft v.0.0.5.

Here is version 5 of my design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690181200391/e7d54276-6fd9-4f46-b1bf-fd7c4431a5ab.png align="left")

Here's the fix to the api container issue: The app container receives its responses directly from the data container instead of through the api microservices container. Adding this loop should reduce the load on the api microservices container.

Also, switching from Qwik/Qwik City to React Native/Expo means that a single code base can be simultaneously pushed to:

* The Web,
    
* The iOS App Store, and
    
* The Android Play Store.
    

### Draft v.0.0.6.

Here is version 6 of my design:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690181238599/1680a234-af54-4f46-a142-5f197e397a6c.png align="left")

With this design, I've added NPM and Docker to the app container.

Also, remember when I added the proxy container way back in version 2? Well, to emphasise the role of the reverse proxy, I've renamed the app container to "app(n)", where "n" references *at least* three containers running in a cluster formation, i.e. using multiple app containers as parts of a Docker Swarm.

## What Should I Add to the Stack?

Although the design continues to evolve, I am now in a position to assess some of my requirements. The specs are still in flux but, for now, version 4 of the design shows six containers (minimum) with the following services sprinkled throughout:

* NGINX Reverse Proxy,
    
* ExpressJS,
    
* Axios,
    
* Deno,
    
* NPM,
    
* Docker,
    
* MariaDB,
    
* Expo, and
    
* React Native.
    

These nine services will be deployed across (*at least*) six containers. Note that multiple services will be deployed within multiple containers.

At this early stage, it is difficult to design solutions to unknown problems. However, as I deploy these containers and weave my APIs, I will begin to notice specific problems that will need resolving. These resolutions should also be reflected back to the design documents.

For now, here are some of the missing components that I already know about.

## What is Missing from the Stack?

Missing from the initial designs are iOS and Android runtimes for WASM. Web deployments should be fine because modern browsers support WASM natively. The mobile runtimes will be a problem, but I'll figure it out. Eventually. Or maybe AI will come to the rescue. Perhaps.

It's importantant to know how much detail to include in a design. Early in the design phase, there are bound to be missing bits. But that doesn't mean the missing bits are not super-important to the overall production. It just means that *sometimes* clarity is better than completeness. The following list is made up of the containers that make up the current design, including known containers that are NOT included in the above diagrams:

### Container name: proxy.

This container receives all of the external requests for web resources. The NGINX reverse proxy passes those requests to the appropriate app(n) container port. NGINX then responds to the original request by sending the resources, processed the app(n) container, back to the requesting IP address.

(Although it's not documented in the design, I am thinking about running NGINX across 3 containers running as a Docker Swarm. This implementation would bump the container count up to eight.)

### Container name: app(n).

These containers run the web application code, serve user requests, and includes the frontend UI design. It is fronted by the NGINX reverse proxy container and is made up of a minimum of *at least* three Docker-enabled containers running in the Docker Swarm mode.

### Container name: api.

This container hosts the REST APIs that serves data to the web application. It exposes its API endpoints to the web-app container.

### Container name: data.

This container runs a database like MariaDB to store and serve data to the api container. It exposes its port to the api container.

(I am thinking of replacing MariaDB with SurrealDB.)

### Container name: queue (not included).

This container would run a message queue like RabbitMQ to facilitate communication between microservices. It would expose its port to the API and worker containers.

### Container name: worker (not included).

This container would run background jobs and tasks. It would listen to the queue container for new tasks.

### Container name: monitoring (not included).

This container would run Prometheus for metrics collection from the other containers. It would expose port 9090.

### Container name: alerting (not included).

This container would run Alertmanager to manage alerts from Prometheus. It would expose port 9093.

### Container Concepts.

The containers should communicate with each other via the LXD network. The api and app containers make HTTP requests to each other. The worker container listens to messages from the queue container. The monitoring and alerting containers scrapes metrics endpoints exposed by the other containers.

Prometheus, running in the monitoring container, collects metrics from the other containers and generate alerts. Alertmanager, in the alerting container, receives those alerts, routes, and sends them to the appropriate recipients.

This containerized microservices architecture, deployed with LXD containers, would provide scalability, isolation, and ease of management for an application hosting framework. The monitoring and alerting tools provides visibility and notifications for any issues.

## How Will My TechStack Help?

A great microservice design needs to:

* Scale as the app count (and dev team) grows,
    
* Implement quality outcomes,
    
* Deliver high performance,
    
* Reduce development costs,
    
* Provide a low barrier to entry, and
    
* Support feature expansions and adaptations.
    

My chosen technology stack can help deliver the outcomes I require for my microservice design:

• Scalability - By decomposing my system into independent services, I gain the ability to scale each service independently based on its own needs. As the app count grows, I can add more instances of services as needed.

• Performance - By splitting tasks into focused services, each service can be optimized for its specific purpose. This leads to better performance and resource utilization.

• Low barrier to entry - Using a stack of popular technologies like Express, Deno, React Native, and Docker makes it easy for new developers to get up to speed and contribute.

• Adaptability - The modular nature of microservices makes it easier to replace, upgrade or add new services with minimal impact on the overall system. This supports feature changes and innovation.

• Reliability - Each service can be deployed, tested, monitored and managed independently. This improves the stability and uptime of my system.

• Cost efficiency - Scaling individual services independently allows me to right-size resource allocation based on actual needs. This optimizes costs.

• Development efficiency - Having independent services allows different teams to work in parallel with less dependency on each other. This improves development velocity.

The key benefits that will help me achieve my desired outcomes are:

• The scalability, adaptability and independent management that microservices provide,

• The performance gains from optimizing each service for its specific purpose,

• The development efficiency of having independent, loosely coupled services, and

• The ability to use a stack of popular technologies with a low barrier to entry.

### What to Do in the Face of Popularity.

Growth is one of those awesomely horrible problems experienced by popular apps. Scaling is great because: Eyeballs equals income. Also, growth sucks because: Servers equals expense. Planning for growth *from the very beginning* requires a dynamic scaling process. Dynamic scaling is needed to address the WORST CASE SCENARIO. That's right: Popularity is BAD if I don't plan for it, and dynamic scaling is what I'll use to keep my costs in check. As my costs increase, this rise will (indirectly) prove that an increase in popularity has occured. An increase in (assumed) popularity can easily justify an increase in advertising costs (to my clients). If my platform(s) attract the "eyeballs" of my users, then my clients may want to pay a fee to attract their attention. Remember, the purpose of these platforms is "user engagement" where the community generates it's own engagement. Maintaining a balance between server expenses and advertising costs (plus my cut) is the epitome of providing a perpetual service where the community drives its' own involvement.

### Maintaining Quality.

Here are some ways I can maintain quality outcomes for my microservice architecture:

1. Testing - I can use a thorough test suite for each service, including unit, integration and end-to-end tests. I should frequently run tests as part of my development cycle.
    
2. Monitoring - I can monitor the health, performance and resource usage of each service. I should set up alerts for any issues or degradation in quality.
    
3. Logging - I can implement proper logging for each service. I should capture useful information for debugging and tracing requests.
    
4. Versioning - I can properly version my APIs and make backwards compatible changes where needed. I should avoid any and all breaking changes.
    
5. Documentation - I can maintain up-to-date documentation for each service, including API docs and usage guides. I should help developers build correctly against my services.
    
6. Defensive coding - I can implement defensive coding practices. I should use input validation, error handling and security checks within each service.
    
7. Automation - I can automate tasks like testing, deployments and monitoring setup. I should reduce the amount of manual effort, and thus human errors.
    
8. Continuous improvement - I can identify bottlenecks and opportunities for optimization on an ongoing basis. I should make improvements iteratively.
    
9. Standards - I can adhere to coding and architectural standards. I should promote consistency across services.
    
10. Incident response - I can develop a plan and runbook for responding to production issues quickly and minimize impact. I should learn from all incidents to prevent recurrences.
    

A combination of thorough testing, monitoring, documentation, defensive coding practices, automation, optimization, standards adherence and an incident response plan can help provide high quality outcomes from my microservices.

### Performance Metrics.

Some key performance metrics I should monitor for my microservices:

• Latency - The time taken for a service to respond to a request. High latency can impact performance and user experience.

• Error rates - The percentage of requests that result in an error response. High error rates indicate issues.

• Request counts - The number of requests served per second. This indicates the overall load and usage of the service.

• Saturation - The percentage of maximum capacity currently used. Approaching saturation indicates the need to scale.

• Memory usage - The amount of memory being used by the service. High usage can impact performance.

• CPU usage - The percentage of CPU being used. High CPU usage can indicate the need to optimize code or scale.

• Network I/O - The amount of network traffic in and out of the service. High network I/O can bottleneck performance.

• Disk I/O - The amount of disk read/write activity. High disk I/O can bottleneck performance.

• Response times - The amount of time to return from a service call. Response time includes latency, processing time and queueing delays.

• Throughput - The number of requests served successfully in a given time period.

• Concurrency - The number of concurrent requests being served at a given time.

• Container metrics - For containerized services, metrics like CPU/memory usage and network I/O per container.

• Service level objectives (SLOs) - The key performance indicators you have defined for your services based on your requirements.

These are the main performance metrics I should monitor to get a complete picture of how my microservices are performing and to quickly identify and address any performance issues.

## The Results.

I have many more questions, like:

* How Much is Too Expensive?
    
* What are my Barriers to Entry?
    
* Horizontal Expansion or Vertical Expansion?
    
* The Best Way to Combine Technologies?
    
* What is the Best Landing Page Design?
    
* Using Virtual Machines or Containers?
    
* How Should I Process Subscriptions?
    
* Oppenheimer or Barbie?
    

But sometimes I just need to move forward and start building some stuff.

Designing a software architecture for the 12 Startups Project requires careful consideration of various factors such as scalability, performance, and maintainability. By adopting technologies like React Native, Expo, and Docker, and following best practices in testing, monitoring, and documentation, it is possible to build a robust and adaptable system that can efficiently handle growth and deliver high-quality outcomes.

> **Attribution:**
> 
> [https://www.youtube.com/watch?v=j6ow-UemzBc](https://www.youtube.com/watch?v=j6ow-UemzBc)

## In Conclusion.

An adaptable design becomes more important as a project grows in size and complexity. I don't know if the 12S project will grow beyond the initial 12 Startups (although technically it has already grown to 18 apps). However, the *WHOLE* point of these experiments is to iterate through the designs and deployments. The hope is that I'll eventually create a structural design that is:

* Maintainable,
    
* Easy to adopt,
    
* Simple to deploy,
    
* Clear and concise,
    
* Safe and secure, and
    
* Extensible and adaptable.
    

I hope to achieve these outcomes by using, and combining these processes, procedures, and philosophies:

* IaC,
    
* SaaS,
    
* CI/CD,
    
* GitOps,
    
* DevOps, and
    
* Agile.
    

Specific technologies like Expo, React Native, and Tauri are also important to my structural design. I suspect, however, that IaC is going to be the foundation of my next series of articles. Yippee!!

Until next time: Be safe, be kind, be awesome.