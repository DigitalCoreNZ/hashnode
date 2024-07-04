---
title: "10 of 10: CrowdSec in the Docker Container."
datePublished: Thu Jul 13 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clk0v1om000a21bnv53vl24kv
slug: 10-of-10-crowdsec-in-the-docker-container
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701999562710/b702ee95-9fbd-4665-a83a-aabca15e15ea.png
tags: security, protection, fail2ban, crowdsec, safeguard

---

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | CrowdSec

## TL;DR.

Install CrowdSec in a Docker container to detect and block malicious traffic using collective threat intelligence, providing real-time protection and easy management for containerized environments.

## An Introduction.

My previous post in this 8-part mini-series covered how I [installed Docker Swarm](https://solodev.app/7-of-8-docker-swarm-with-docker-containers) for remote Docker containers. This time, I'm going to show how I install CrowdSec in the Docker container.

> The purpose of this post is to install CrowdSec in the Docker container.

CrowdSec is an open-source collaborative security system that detects and blocks malicious traffic in real-time. It works by:

1. Detecting malicious traffic behaviours on individual servers running the CrowdSec Security Engine,
    
2. Sharing detected threats with the CrowdSec network to build threat intelligence, and
    
3. Providing this threat intelligence back to all nodes in the network to help them detect and block similar threats.
    

In essence, it leverages the wisdom of the crowd to identify new threats and stop them before they cause damage.

CrowdSec has two main components:

1. The CrowdSec Security Engine - This detects malicious traffic behaviours by analyzing log files from services like Nginx, Apache, iptables, etc. It can run on Linux, Windows and containerized environments.
    
2. The CrowdSec Console - This is a web interface that allows me to monitor threats detected by the CrowdSec Security Engine, get alerts, and access the shared threat intelligence from the CrowdSec network.
    

When the CrowdSec Security Engine detects malicious behavior, it will:

* Block the offending IP address using a firewall bouncer plugin,
    
* Share anonymous details about the threat with the CrowdSec network, and
    
* Receive threat intelligence from the CrowdSec network to improve its detection capabilities.
    

The shared threat intelligence includes information like:

* Country of origin,
    
* Autonomous system,
    
* Aggressiveness level,
    
* Type of attack,
    
* And more.
    

This intelligence can then be accessed via the CrowdSec Console or CrowdSec API to get insights into flagged IP addresses. It can also be integrated with threat intelligence platforms and security orchestration systems.

## The Big Picture.

We often *need* to grow beyond our comfort zone. The world changes and we (sometimes) change with it. Programmers are no different but are less averse to learning new things and trying new... things. There's an adage that goes "If it ain't broke, don't fix it" but, as engineers, we go out of our way to break things *on purpose*.

CrowdSec is a Big Picture example of our collective mindset. We had a well-considered tool called Fail2Ban. It did exactly what I wanted. But when the mice learned to defeat the mousetrap (and walk away with my cheese) everyone who used Fail2Ban had a problem. Luckily, I belong to an industry of problem solvers. Not only is CrowdSec a better mousetrap (compared to Fail2Ban) but it invisibly spreads its processing requirements across every installation. Clever.

I am very lucky to work in a field where engineers love showing off their skills.

## Installing CrowdSec.

* From a terminal (`CTRL` + `ALT` + `T`) that is connected to the Docker container, I Install the CrowdSec repository:
    

```javascript
  curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
```

> NOTE: Curl will need to be installed for this command to work:
> 
> ```javascript
> sudo apt install -y curl
> ```

* After downloading the repo details, I update the package list:
    

```javascript
  sudo apt update
```

* I install CrowdSec:
    

```javascript
  sudo apt install crowdsec
```

> NOTE: During installation, CrowdSec will detect existing services like Nginx, Apache, etc. and configure itself automatically.

After installation, I can manage CrowdSec using the cscli command line client.

* Here are some useful cscli commands are:
    

```javascript
sudo cscli metrics #view statistics
sudo cscli alerts list #view alerts
sudo cscli decisions list #view blocking decisions
sudo cscli parsers list #list parsers
sudo cscli scenarios list #list scenarios
```

> Attributions:
> 
> [https://docs.crowdsec.net/docs/cscli/](https://docs.crowdsec.net/docs/cscli/)

* To block attacks, I will need to install a bouncer. The firewall bouncer cs-firewall-bouncer can be installed with this command:
    

```javascript
  wget https://github.com/crowdsecurity/cs-firewall-bouncer/releases/download/v0.0.12/cs-firewall-bouncer.tgz
  tar xzvf cs-firewall-bouncer.tgz
  cd cs-firewall-bouncer-v0.0.12/
  sudo ./install.sh
```

* I will then need to configure the bouncer API key in `/etc/crowdsec/cs-firewall-bouncer/cs-firewall-bouncer.yaml`.
    
* I can add components from the CrowdSec Hub using cscli:
    

```javascript
  sudo cscli postoverflows install crowdsecurity/seo-bots-whitelist
  sudo systemctl reload crowdsec
```

## The Results.

CrowdSec provides collaborative detection, prevention and intelligence about malicious traffic. It's open source, free to use and easy to setup and manage.

I explored the installation and setup of CrowdSec in a Docker container, enhancing the security of my container by leveraging the power of collective threat intelligence. This open-source solution provides real-time protection and easy management, making it an essential addition to my `homelab` or any containerized environment.

Both CrowdSec and Fail2ban are open-source intrusion prevention tools that detect and block malicious activity. However, there are some key differences:

### **CrowdSec.**

* Uses a dynamic rule engine that analyzes logs in real-time to determine threats and block IPs. The rules adapt as threats evolve.
    
* Leverages threat intelligence from a global community of CrowdSec users to identify and block emerging attacks.
    
* Has machine learning capabilities that improve detection accuracy over time.
    
* Is designed for scalability and high performance, even under heavy load.
    
* Offers integration with various security tools and platforms.
    

### **Fail2Ban.**

* Uses a static rule-based approach where rules are defined manually.
    
* Relies only on logs from the local server - it does not share threat intelligence with other users.
    
* Has no machine-learning capabilities.
    
* Is not as scalable and may impact performance under high load.
    
* Has limited integration options.
    

CrowdSec is the better choice for:

* Detecting and blocking unknown threats through community threat intelligence and machine learning,
    
* Handling large deployments and high traffic due to its scalable architecture, and
    
* Integrating with your existing security tools and platforms.
    

Fail2ban is better suited for:

* Simple deployments with well-defined threats and rules, and
    
* Systems with limited resources where performance is crucial.
    

For most modern infrastructure, CrowdSec will provide a more robust and proactive intrusion prevention solution thanks to its dynamic rule engine, threat intelligence, machine learning and scalability. However, Fail2ban is still a good option for basic protection on resource-constrained systems.

## In Conclusion.

CrowdSec has proven that one indisputable fact is true: This is an opportunity for clever programmers to build some awesome threat-analysis tools. Developers, hosting providers, and ISPs can easily install open-source solutions that provide a safe Internet experience. These server-based, network-enabled, AI-powered, auto-evolving, self-regulating, semi-autonomous utilities can coordinate their resources to clean up a bulk of the Internet. Yes, I see a subscription opportunity on the horizon: A service where clients contribute small amounts of processor time to the mission: Squash spam, vanquish viruses, and smash spammers.

Until next time: Be safe, be kind, be awesome.

[Homelab](https://solodev.app/1-of-10-my-first-homelab) | [LXD Manager](https://solodev.app/2-of-10-lxd-on-the-homelab) | [Docker](https://solodev.app/3-of-10-docker-in-a-linux-container) | [Docker Desktop](https://solodev.app/4-of-10-docker-desktop-on-the-local-system) | [Deno](https://solodev.app/5-of-10-deno-in-the-docker-container) | [MariaDB](https://solodev.app/6-of-10-installing-mariadb-and-mysql-workbench) | [Portainer](https://solodev.app/7-of-10-portainer-in-the-docker-container) | [More Docker](https://solodev.app/8-of-10-more-docker-containers) | [Docker Swarm](https://solodev.app/9-of-10-docker-swarm-with-docker-containers) | CrowdSec