---
title: "Learning New Technologies."
datePublished: Thu Dec 07 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clpuywhox000g08ldcq8i3fgk
slug: learning-new-technologies
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1701473790901/2a8344cc-9347-4b1d-887c-b8a928caf41b.png
tags: self-improvement

---

Update: Tuesday 2<sup>nd</sup> January 2024.

## TL;DR.

As a solo developer, staying up-to-date with new technologies is crucial. Mastering these technologies also requires time, active learning strategies, and environments for developing new apps and practising new skills.

I can build, and test, my apps on the AMD Ryzen 5 `workstation`. This is the place where I can adopt any programming language or employ any ecosystem.

I can test my deployment strategies on the Intel NUC 10 `homelab`. This is the place where I can validate the deployment viability of my packaged apps.

Also, I build system images that allow me to restore my systems to a stable state, if needed.

But that's not all...

I also post to my blog and put theories into practice. Projects like the "12 Startups" challenge (in progress) and the AI-based code-generating app (under development) are active learning experiences.

The result?

Continuous growth and new skills in a constantly changing field.

## An Introduction.

It feels like every week someone releases new software. Keeping up with, and evaluating these new releases seems like a Sisyphean curse, i.e. laborious and futile. For this reason, I must be selective about the technologies I evaluate.

> The purpose of this post is to present my learning method.

I also need to be methodical if I want to compare similar technologies, like Node vs Deno and Bun, Express vs Elysia, and SvelteKit vs Qwik City vs Astro.

## The Big Picture.

It is important to choose the right technologies for any given project. My problem is many of these technologies are new to me. For instance, I need to learn Svelte before learning SveltKit. Then I need to go through the same process with Qwik and Qwik City, especially if I want to compare them against Svelte and SvelteKit. And let's not forget Astro.

Luckily, their tutorials have interactive code editors. For me, I use my `homelab` where I can safely practice my computer coding and server deployment skills.

## My Homelab vs My Workstation.

The main advantage of my [homelab](https://solodev.app/1-of-10-my-first-homelab)↗, an Intel NUC 10 small form-factor PC, is that I can test different programs that I write, regardless of the programming language, ecosystem, or other servers that are used by the application. If there are problems running an app on my `homelab`, then I have to fix those issues before "containing" the app for publication.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689485289426/187d69ca-3dcd-43c1-a6ba-4551b3813fdd.jpeg align="center")

The main advantage of my `workstation` (a Ryzen 5, 6-Core CPU-based PC with a 12GB RTX 3060 GPU) lies in the power it has for running 15B LLMs.

> NOTE: 2024 will see the introduction of a Beast PC for fine-tuning LLMs.

## Cloning My Systems.

I can clone my systems and use the resulting images as recovery checkpoints. If any system gets "truly messed up" I can restore it by using these images. My recovery images are built using a free utility called CloneZilla.

## Containers vs Environments.

I use a number of container managers and environment managers, including LXD/LXC (LinuX Daemon/LinuX Containers), Docker, Distrobox, and Anaconda.

LXD and Docker are container managers. I use these tools to "spin up" isolated LXCs and Docker containers. The containers I build with LXD and Docker are used to enclose my software experiments or deploy my software solutions. Unless I set up communication channels, the running services within an LXC or Docker cannot affect other containers or the host operating system. The main advantage of using LXC and Docker containers is that I can safely build new technology stacks, evaluate their performance, and learn how different services interoperate. Tuning these services so they work well together can also lead to breakages. Luckily, isolated containers are also disposable. Other advantages include:

* The ease of of creating an LXC, and
    
* The speed of deploying a Docker container.
    

Distrobox and Anaconda (Conda) are environment managers. They have direct access to the host file system and PC hardware because environment managers serve a different purpose: The environments they build are virtual. This is why Distrobox can host any Linux distro in my terminal, and Conda can host multiple versions of Python. Also, virtual environments are as ephemeral as containers, and can be deleted with ease.

My `homelab` is a great place to test any newly acquired skills, but how do I know which skills to practice? There's a process that I used to help define an answer.

## Creating Content.

As a content creator, I need to generate posts for my blog. Fortunately, this blog centres on my being a solo developer who is developing his software skills. (Yes, my pronouns are him, he, and his. I'm boringly pedestrian. \*Yawn\*) Even though my blog needs posts, the *real* question is: Which skills do I *need*?

First, I need a limiting factor. Luckily, mine is *also* the reason for this blog:

> Every skill that I acquire must be directly applicable to bootstrapping, and then running, my technology startup.

Next, I need a purpose. Creating content around learning new skills that are applied to bootstrapping a company is fantastic, but where lies the nobility, the passion, and the spirit? What is the aspiration I have for my company?

> Every utility that I build must have a positive, measurable effect on the lives of my users, and others around them.

Finally, I need a timeline. The "12 Startups in 12 Months" challenge has an obvious end date, but the rationale for doing "12 Months" is less obvious. The reason for accepting the "12 Startups" challenge is that my company needs a software production pipeline. This challenge gives me an excuse to develop that pipeline. So, what about any other projects that the company accepts? The goal of the pipeline is to efficiently develop, and deploy, any project that comes my way.

> Every project that I undertake must result in a minimum viable product within 28-days, with open invitations sent to alpha testers on the 29<sup>th</sup> day.

"12 Startups" gives me a lot of opportunities to create content for this blog, but where do I find the source material for each post?

## The Only Constant is Change.

For over 30 years I've relied on books, videos, and official documentation when it comes to learning new technologies. When I switched from compiled languages for MS-DOS and Windows (QBasic, Turbo Pascal, Turbo C, Delphi, and Visual C++) to CGI scripts and LAMP Stack for the web, I relied on books I purchased from Borders Bookstore, Queen Street, Auckland. (Borders Group filed, and was approved, for Chapter 7 bankruptcy in 2011 after triumphantly failing to compete with Amazon and Barnes & Noble.)

In the early 2000s, I also realised that the best way to learn a subject was to teach that subject. I spent a year teaching others how to be computer service technicians, or at least provide them with enough knowledge to obtain a CompTIA A+ certificate and become Microsoft Certified Professionals.

In 2015, I switched from PHP (the change from PHP 5.4 to PHP 7 was in progress) to the JavaScript ecosystem because ECMAScript 2015 (formally ES6) was released and I also wanted to use the Node runtime. At the time, I felt JavaScript was heading into strange and exciting territories. Boy, was I right!!

We used to call ourselves software engineers (before my time) and then computer programmers (when I started) and now we're known as app developers (because writing the word 'application' takes too long). If our job title is always changing then it's no wonder our tools are constantly in flux.

The adage is true, especially in our field: Change is constant. But how do I stay abreast of the changes that happen all around me?

## The Best Way to Learn...

As I mentioned in the last section, the best way to learn a subject is to teach that subject. This philosophy is the main reason for my blog and the driving force behind my writing of these posts.

Except, I specifically write these posts for an audience of one: Me. I'm always saying "I follow this process to get this result", or "I follow that procedure to get that outcome." I purposely avoid "You should do this", or "You should do that" because this blog is a first-person narrative: I'm a person and this is my story. You're welcome to read my story if you want but I'm not here to tell you what to do. Instead, I'm here to show what *I* did, to explain how *I* do things, and to share *my* rationale behind the choices I make. The purpose of my blog is not to tell others what to do but to share what *I've* done. I give context, I give perspective, I don't give instructions. Yes, most of my posts have step-by-step instructions, but these are the steps I took and I do NOT expect anyone to follow in my footsteps.

I've ALWAYS highlighted text passages in my books (where now I use a Chrome extension called [Web Highlights - PDF & Web Highlighter](https://chrome.google.com/webstore/detail/web-highlights-pdf-web-hi/hldjnlbobkdkghfidgoecgmklcemanhm)) and written my own, detailed notes. Only recently have I blogged about my technology experiences. (I tried blogging before, on more than one occasion, but I never got the hang of it.) I write this blog and create my notes because committing my thoughts to "paper" forces me to be clear and precise regarding the steps I take and the rationales I use. When adapting the official documentation for a new piece of technology, I rewrite those documents using my voice while maintaining the integrity of the original text.

This is how I learn new technologies, at least technologies that are new to me. It's a tried and battle-tested process, but can I adopt other learning methods?

## ...Is to Teach.

In the early 2000s, I spent a year teaching others (1) how to obtain their CompTIA A+ Certificate and (2) how to become a Microsoft Certified Professional. For me to effectively share my knowledge about PC hardware and the Windows 2000 operating system, I needed to know *everything* about being a computer service technician, or *at least* enough to answer any question that was asked in class. As a result of my 12-month tenure, I became very good at building and servicing PCs. Tutoring 4 classes gave me 4 opportunities to scour our textbooks for knowledge.

The point is that: I found myself in a situation where I needed to acquire specific knowledge to effectively perform my duties. Nowadays, I require self-motivation to improve what I know. Therein lays the purpose of this blog: To learn new technologies and post articles about my findings.

Writing posts is a great motivator for acquiring new knowledge. Also, this blog becomes a central repository of all my learnings. However, now that I've trawled the documentation and written about what I found, is there anything else I can do to solidify my newly won insights?

## Making Videos.

Working through the official documentation for new technologies takes time, but I once saw a video where the presenter was reading the documentation verbatim. No, I never watched to the end but that's not the point: *He* read the documentation and, from a learning perspective, that's a major part of *my* learning process.

I'm going to make similar videos and categorise them as "The TechDoc Series". It will make for boring videos but, as a podcast, this series may just be what engineers need to lull themselves to sleep. Yeah, ASMR for software engineers.

Also, I have this blog which I can use as source material for my videos.

But are there other ways for me to learn technical topics?

## Practice makes Perfect.

Having my notes to call on is a great start, and making videos is a terrific follow-up, but nothing beats putting my new skills into practice. Thankfully, I have the "12 Startups" challenge on which to apply any newly acquired abilities.

Although "Practice makes Perfect" is a great path to proficiency, I need to remember that "Perfect is the Enemy of Good." In other words, the real world requires practical solutions. The purpose of an MVP (minimum viable product) is to provide a platform where select, real-world testers can provide their feedback and opinions. Testers will have their points of view and can provide observations that go beyond my limited perspective. My mission is to build products that people will use, not apps with all the bells and whistles.

The point I'm making is this: I need to be practical. I would love to spend the rest of my life at university... if I had the money, but I have a startup to bootstrap. I only need to learn enough about specific technologies for those techs to be effective in my business. MVPs are not built on the subtle nuances of a programming language, but "[bodged](https://www.google.com/search?q=bodge+british+meaning)" together with the software equivalent of duct tape and spit.

## Using AI, LLMs, and Agents.

In June 2018, OpenAI launched GPT (generative pre-trained transformer). GPT is a generative language model that was trained on an enormous BooksCorpus dataset. However, the current hype around AI is the result of over 70 years of academic research.

![](https://media.licdn.com/dms/image/D5612AQF_uwUrIzdW8A/article-inline_image-shrink_1000_1488/0/1693907807531?e=1706140800&v=beta&t=aPVCqUprbsVwT_IO3n5dikKHxLc2zbn89Tf9HcbnH-4 align="center")

The current popularity of AI dwarfs any other technology zeitgeist:

![](https://media.licdn.com/dms/image/D5612AQGjj35zuEbjAQ/article-inline_image-shrink_1000_1488/0/1693906316278?e=1706140800&v=beta&t=spVijs4A_w2SPoQ-8D3g9AejzfirbFBu-32geRTizdQ align="center")

The boost in AI popularity has exploded beyond the hallowed halls of academia and the jaded déjà vu of software engineers. No, this is different. AI has filtered into our social fabric thanks to the proliferation of mobile devices. The manufacturers of smartphones and tablets (both Apple *and* Samsung) have seen fit to include AI chips in their products. ([Check out this report](https://www.precedenceresearch.com/mobile-artificial-intelligence-market)↗.) Huawei started the trend in 2017 but all the other tech companies also saw the writing on the wall. The writing was vague and indistinct but they knew the next killer app would be an AI-based monster. Enter ChatGPT.

Just look at that chart! ChatGPT is more celebrated than the Metaverse and crypto combined!! The hallucination problem can also be fixed with Internet-enabled agents that confirm the accuracy of an answer while providing citations, too.

As a developer, it is in my best interests to get to grips with AI, machine learning, deep learning, LLMs, and agents. Sadly, using the models from OpenAI can become an expensive proposition, considering how much time I'll need to practice, and develop, my prompt engineering skills. Luckily, Hugging Face hosts many open-source LLMs. These models are, more than likely, capable of meeting my needs.

## The Results.

Staying up-to-date with new technologies is essential for a solo developer. By using a homelab, creating content, making videos, and putting theory into practice with projects like "12 Startups" and using AI-based models, I can efficiently learn and adapt to the ever-changing landscape of software development. These methods ensure my continued growth as an engineer by acquiring new skills and knowledge.

## In Conclusion.

I'm a life-long learner. I would spend the rest of my life at university if I could afford it. (It ain't cheap trying to learn what I don't know.) My way of learning isn't special and is probably the same as everyone else. As a result of our chosen field, however, there is no denying that programmers are very adaptable.

Bring it on, Evolution. We're ready to take on whatever you throw at us! (And while you're at it, bring back the dinosaurs!!)

Until next time: Be safe, be kind, be awesome.