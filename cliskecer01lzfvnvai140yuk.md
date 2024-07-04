---
title: "The DevOps-SRE Conundrum."
seoDescription: "DevOps is a software development philosophy that combines development and operations, focusing on collaboration, automation, and continuous delivery."
datePublished: Mon Jun 12 2023 08:00:42 GMT+0000 (Coordinated Universal Time)
cuid: cliskecer01lzfvnvai140yuk
slug: the-devops-sre-conundrum
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699605104444/8dbd6f02-4aec-4288-88b4-25f8ad1b22c0.png
tags: automation, monitoring, devops, logging, sre

---

## TL;DR.

DevOps is a software development philosophy that combines development and operations, focusing on collaboration, automation, and continuous delivery. Site Reliability Engineering (SRE) is a related discipline that ensures the reliability and scalability of production systems. Both practices use various tools for version control, CI/CD, configuration management, containerization, monitoring, and collaboration. Planning and choosing the right tools for your technology stack is crucial for successful implementations.

## An Introduction.

How does DevOps work in the real world? To answer that question, I will:

* Break down what Development and Operations mean,
    
* Explore the different parts that drive DevOps forward,
    
* Compare DevOps to Site Reliability Engineering, and
    
* List some tools that are used by modern practitioners.
    

> The purpose of this post is to present the differences and similarities between DevOps and SRE (Site Reliability Engineering).

> **Attribution:**  
> [What is DevOps? REALLY understand it | DevOps vs SRE](https://www.youtube.com/watch?v=0yWAtQ6wYNM) from [TechWorld with Nana](https://www.youtube.com/channel/UCdngmbVKX1Tgre699-XLlUA)

## What is DevOps?

DevOps is a software development philosophy that combines software development (Dev) and system operations (Ops); it is a doctrine that guides a set of practices. DevOps emphasizes collaboration and communication between development teams, and operations teams, to improve the speed of software delivery and the quality of software deliverables.

The main goal of DevOps is to enable organizations to release high-quality software more frequently and reliably. DevOps teams work together to automate infrastructure and deployment processes, test and deliver changes in an agile way, and monitor applications and infrastructure for technical issues.

DevOps typically include mechanisms like the Agile principles, version control systems, continuous integration/continuous delivery (CI/CD) pipelines, containerization, configuration management, and monitoring/observability solutions.

Overall, DevOps can help organizations reduce the time it takes to bring new features to market, increase the reliability and stability of applications, and improve collaboration and communication across teams throughout the software development lifecycle.

### Development.

Development in DevOps typically involves continuous integration (CI) and continuous delivery (CD), where small changes are made frequently, and tested automatically, to ensure they integrate smoothly with the existing codebase while meeting code quality standards.

Development teams often use Agile principles, which prioritize flexibility, teamwork, and customer satisfaction. Agile development teams typically work in short iterations known as sprints, where they plan, build, test, and deliver a small set of features or improvements.

Tools and technologies, such as version control systems (e.g., <mark>Git</mark>), issue tracking systems (e.g., <mark>Jira</mark>), build automation tools (e.g., <mark>Jenkins</mark>), and containerization platforms (e.g., <mark>Docker</mark>) enable teams to:

* Quickly iterate on code and platform changes,
    
* Automate testing and deployment processes, and
    
* Collaborate across multiple teams and environments.
    

### Operations.

Operations refer to the processes that occur during, and after, software development. Operations are the practices and tools used to deploy, monitor, and manage the applications in production environments.

The goal of operations is to make the deployment and management of software applications as efficient, reliable, and scalable as possible. Operations teams use a variety of techniques and tools to achieve this goal, such as server automation, infrastructure as code, and continuous monitoring and testing.

Operations teams are responsible for ensuring that applications are deployed to production environments in a consistent and repeatable manner. They also monitor and manage the performance, availability, and security of applications. If an incident occurs, operations teams work to quickly identify the issue and resolve it, often through automation and collaboration with other teams.

To support operations, teams use a variety of tools and technologies, such as configuration management systems (e.g., <mark>Ansible</mark>), container orchestration platforms (e.g., <mark>Kubernetes</mark>), log analysis tools (e.g., <mark>Splunk</mark>), and incident management systems (e.g., <mark>PagerDuty</mark>). These tools enable operations teams to automate routine tasks, detect problems, and troubleshoot issues faster while also collaborating across multiple teams and environments.

### Engagement.

DevOps is a philosophy, and engineering practice, for software developers and systems operators.

The ideas behind DevOps emerged in 2007, while the term itself was coined in 2008. Skip forward to November 2021 when the Continuous Delivery Foundation released a report where 19,000 developers were surveyed. The Foundation was asking questions regarding the developer's engagement with DevOps practices. The results of this survey show that 80% of developers who work for companies with two or more employees use at least some aspects of the DevOps practice. However, only 14% of developers take less than one day to push code into production and only 10% perform multiple deployments each day. There were no signs of an increased velocity for DevOps adoption, although it is still a popular model for software development.

### DevOps is NOT a Simple Term.

DevOps, in its simplest form, is a philosophical ideal where communication between technology silos improves when the barriers between these silos are reduced. Software developers are conceptually thought of as a silo, as are systems operators. Other silos include security and testing. Of course, just like in real life, things are never as simple as they seem. Beyond the philosophy is an engineering practice that is elaborate, exacting, and rigorous. Established engineering teams who adopt DevOps wholesale are few and far between. Most teams adopt parts of the DevOps practice, those parts that are appropriate to their specific needs. But what about a SoloDev like myself? How do I learn, and adopt, DevOps if DevOps is specifically designed to improve teamwork situations?

### There is More to DevOps than DevOps.

As already mentioned, DevOps - as a practice - is partly software development and partly systems operations. But DevOps is also testing, security, continuous integration, and continuous delivery. DevTestSecCiCdOps is a mouth full, doesn’t roll off the tongue, and leaves a sour taste in my mouth. So we just call it DevOps for brevity and because it’s a catchy marketing term.

DevOps is mostly about improved communications between (previously siloed) teams, but the CI/CD part of DevOps is where I get to practice (and improve) my automation planning, deployment, and expansion.

### The Application Release Process.

DevOps includes a detailed pipeline called the Application Release Process. The main purposes of this pipeline are to:

* Deliver an app to the end users,
    
* Deliver new features to the app that benefit the end users,
    
* Deliver bug fixes that improve the useability of the app,
    
* Deliver optimisations to the app that improves the user experience,
    
* Deliver security patches that protect the end users of the app, and
    
* Deliver maintenance updates to the app until sunset when the app is finally deprecated.
    

Deliverables are the only goals that matter, regardless of the SDLC (covered in the next section) that was used to create and deploy the app. An ARP pipeline is vital to achieving an app’s deliverable targets.

### The Software Development Life Cycle.

The SDLC (Software Development Life Cycle) is a model for businesses to follow, businesses that produce software with:

* The highest quality, and
    
* The lowest cost, within
    
* The shortest timeframe.
    

DevOps is an SDLC that is well-known (though, arguably, not well understood) to many development teams, but it’s not the only SDLC available. There are other models, like:

* Agile,
    
* Lean,
    
* Waterfall,
    
* Iterative, and
    
* Spiral.
    

Each of these SDLCs has its strengths and weaknesses, its pros and cons, and each team is welcome to choose a model that is appropriate to their needs. One of the reasons for choosing DevOps is because of its focus on building, and using, automation processes whenever possible.

As the sole proprietor of my company and its only developer (which is the *exact* definition of a SoloDev), I will happily adopt any practice that reduces my workload and improves my code reliability.

### The Key to DevOps.

Over the past 15 years, different companies have implemented DevOps in different ways, using different tools, and focusing on different aspects of the DevOps practice.

More recently, common patterns have emerged. These patterns have allowed DevOps to coalesce into a more defined and predictable workflow. This workflow, as such things are wont to do, has seeped into many companies, and service providers, to replace their in-house, ad-hoc, cobbled-together solutions.

The singular key to successful DevOps integrations is automation. Achieving a level of automation that has a measurable impact on a business requires adopting a significant technology stack.

### DevOps Tools

Here are some commonly used tools in DevOps:

* **Version Control:** Version control systems such as <mark>Git</mark>, <mark>SVN</mark>, and <mark>Mercurial</mark> are used for code management, tracking changes and enabling collaboration.
    
* **Continuous Integration/Continuous Deployment (CI/CD) tools:** CI/CD tools like <mark>Jenkins</mark>, <mark>Travis CI</mark>, <mark>CircleCI</mark>, <mark>GitLab CI/CD</mark>, and <mark>GitHub Actions</mark> enable developers to continuously build and test code changes and deploy them to production environments.
    
* **Configuration Management:** Configuration management tools like <mark>Ansible</mark>, <mark>Chef</mark>, and <mark>Puppet</mark> enable teams to configure, deploy and manage infrastructure, including servers, databases and other resources used in the software development process.
    
* **Containerization:** Container technologies like <mark>Docker</mark>, <mark>Kubernetes</mark>, <mark>OpenVZ</mark>, <mark>Proxmox</mark>, and <mark>LXD</mark> are used to deploy applications on different hosting environments, providing portability and easier management.
    
* **Monitoring and Alerting:** Tools such as <mark>Prometheus</mark>, <mark>Nagios</mark>, <mark>Sensu</mark>, and <mark>Zabbix</mark> help teams monitor application performance, log files, and system metrics. Alerting tools like <mark>PagerDuty</mark> and <mark>OpsGenie</mark> notify teams of potential issues or outages.
    
* **Collaboration Tools:** Communication and collaboration tools like <mark>Slack</mark>, <mark>Microsoft Teams</mark>, and <mark>Zoom</mark> help team members communicate efficiently and respond to issues in real time.
    

These are just a few examples of the wide variety of tools used in DevOps.

## What is Site Reliability Engineering?

Site Reliability Engineering (SRE) is a discipline that focuses on the reliability, scalability, and performance of large-scale distributed systems. It emerged from the need to manage the complex systems that power modern websites and applications, enabling businesses to keep up with growing user demands while maintaining high levels of availability and resiliency.

SRE is based on the principles of software engineering and applies them to the operations of complex systems. Key aspects of SRE include proactive monitoring, automated incident responses, and scalable infrastructure that can handle large amounts of traffic and data. SRE teams use tools and technologies such as automation, monitoring systems, alerting systems, and performance management tools to continuously monitor the system and improve its reliability.

The role of an SRE team is to ensure that the systems they manage are highly available, performant, and scalable, and to understand and reduce the impact of incidents when they occur. They work closely with development teams to share responsibility for the performance and reliability of the system as a whole.

Overall, SRE is a discipline that focuses on operational excellence for large-scale distributed systems, enabling businesses to deliver high-quality applications and services to their users.

### The Differences between DevOps and SRE.

DevOps and SRE (Site Reliability Engineering) are related, but distinct, approaches to managing software development and operations. While there are some similarities between the two, there are also significant differences in their focus and goals.

DevOps is a cultural and organizational movement that emphasizes collaboration and communication between development teams and operations teams. DevOps aims to create a culture where developers and operations engineers work together closely, using shared tools, processes, and metrics, to build, test, and deploy software more quickly, and with higher quality.

SRE, on the other hand, is a discipline that focuses specifically on the reliability and scalability of production systems. SRE applies the principles of software engineering to operations, with a focus on automation, monitoring, and measuring system performance to ensure that it meets user needs and business goals.

The key differences between DevOps and SRE are:

* **Focus:** DevOps focuses on collaboration and communication between development and operations teams, while SRE focuses on ensuring the reliability and scalability of production systems.
    
* **Goals:** DevOps aims to improve the speed and quality of software development processes, while SRE aims to ensure the reliability and availability of production systems.
    
* **Scope:** DevOps covers the entire software development lifecycle, from development to production, while SRE is primarily focused on the production environment.
    
* **Metrics:** DevOps measures success in terms of the speed and quality of software delivery, while SRE measures success in terms of system uptime, reliability, and performance.
    

Overall, while DevOps and SRE share some similar goals and principles, they have different areas of focus and are designed to solve different problems in the software development and operations lifecycle.

### SRE Tools.

The tools used in SRE usually depend on the specific requirements of the organization and the technology stack used. However, there are some commonly used tools in SRE:

* **Monitoring tools:** SREs use monitoring tools to track system health, identify performance issues, and optimize system performance. Some popular monitoring tools include <mark>Prometheus</mark>, <mark>Nagios</mark>, and <mark>Zabbix</mark>.
    
* **Logging tools:** Logging tools are used to collect, aggregate, and analyze logs generated by an application or system. Popular logging tools include ELK Stack (<mark>Elasticsearch</mark>, <mark>Logstash</mark>, <mark>Kibana</mark>), <mark>Splunk</mark>, and <mark>Graylog</mark>.
    
* **Configuration management tools:** SREs use configuration management tools to automate the deployment, configuration, and management of infrastructure and applications. Popular tools include <mark>Ansible</mark>, <mark>Puppet</mark>, and <mark>Chef</mark>.
    
* **Incident response tools:** Incident response tools are used by SREs to manage incidents and outages. These tools may include <mark>PagerDuty</mark>, <mark>OpsGenie</mark>, or <mark>VictorOps</mark>.
    
* **Automation tools:** SREs use numerous automation tools to improve operational efficiency and reduce manual operations. For instance, <mark>Jenkins</mark>, <mark>Terraform</mark>, and <mark>Packer</mark>.
    
* **Collaboration tools:** SREs collaborate using communication tools such as <mark>Slack</mark>, <mark>Microsoft Teams</mark>, and <mark>Zoom</mark>. These tools enable efficient cross-functional communication and problem resolution.
    

These are just a few examples of the wide variety of tools used in SRE.

## My Dilemma.

Herein lies my problem: There are just too many DevOps and SRE tool categories (let alone the tools in *each* category) for this SoloDev to consider. What tools should I include in a viable technology stack? How will I ever learn to *use* the tools in a tech stack? What should I do when I discover better tools? When will everyone stop launching *new* tools?

Mine is truly a first-world problem, but the joke is only half-funny because I'm only half-kidding. I have a 12-month time crunch (which sounds like a lot but, from experience, I know I'll piss most of it away) and I need a clue pretty darn quick.

## My Solution.

This is my answer: Plan for organic integrations. What the fudge does *that* mean?! I know I'll deploy Prometheus and Grafana, but knowing what I'll use helps me prepare for that eventually.

### Building a Basic, Strategic Plan.

Strategic planning (mid-term thinking) really helps with tactical execution (short-term conduct). Knowing my actions today will affect my plans for tomorrow ensures I focus on achieving the correct outcomes *right now*. Luckily, (strategic) planning for tomorrow can be as simple as drawing a block diagram or making a list.

### Making a List.

This 2-column table is so basic that an explanation is superfluous:

| Category | Tools |
| --- | --- |
| Version Control | Git, SVN, Mercurial |
| CI/CD | Jenkins, Travis CI, CircleCI, GitLab CI/CD, GitHub Actions |
| Build Automation | Jenkins, Terraform, Packer |
| Configuration Management | Ansible, Chef, Puppet |
| Microservice Containerization | Docker |
| Container Orchestration | K8s, K3s, Rancher |
| System Containerization | OpenVZ, Proxmox, LXD |
| Monitoring | Prometheus (and Grafana), Nagios, Zabbix |
| Alerting | PagerDuty, OpsGenie, VictorOps |
| Collaboration Tools | Slack, Discord, Microsoft Teams, Zoom |
| Log Analysis | ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Graylog |
| Issue Tracking | Jira |

All I did was tabulate all the categories, along with the yellow-highlighted tools, from earlier in this post. Now I clearly see the options available to me. I now have a strategic plan (which looks like a list) for organically integrating the most appropriate tools when each of their times comes. (Obviously, I'll only choose one tool from each category. I'm not a self-masochist.)

### Drawing a Block Diagram.

Using a block diagram for strategic planning is more appropriate when I want to show the relationships between different entities. For instance, a UML class diagram is a great programming tool, while an ERD (entity relationship diagram) is a great relational database design tool. I'm currently using diagrams to arrange my proposed system containers (that will run on the `homelab` system) into different configurations. I'm looking for the best arrangement that meets my limited, technical resources.

I'll use any tool that helps me achieve this specific, tactical objective: Design a container layout, that performs within my resource budget, that can host 18 Startups, and can act as a visual aid to my strategic plan.

Creating a strategic mid-term plan is a tactical short-term objective. Oh, the irony.

## The Results.

DevOps and SRE are powerful methodologies that focus on collaboration, automation, and continuous improvement to deliver high-quality software. While they share some common goals and principles, their areas of focus differ. DevOps emphasizes communication between development and operations teams, while SRE targets the reliability and scalability of production systems. By understanding their distinctions and strategically planning tool integrations, developers can optimize their software development processes to achieve better results.

## In Conclusion.

This post covered a software development methodology that combined software development (Dev) and systems operations (Ops). DevOps is a complex practice that includes software development, systems operations, testing, security, continuous integration, and continuous delivery. It is an SDLC that focuses on automation processes. Site Reliability Engineering (SRE) is a related, but distinct, approach to managing software development and operations.

I miss the good ol' days when LAMP stack was a thing, but I operate in an ever-evolving environment. Working on the bleeding edge of technology is a choice I make. Every. Single. Day.

And I wouldn't have it any other way.

Until next time: Be safe, be kind, be awesome.