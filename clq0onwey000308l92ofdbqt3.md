---
title: "12S: My 2024 Technology Stack."
datePublished: Mon Dec 11 2023 09:00:12 GMT+0000 (Coordinated Universal Time)
cuid: clq0onwey000308l92ofdbqt3
slug: 12s-my-2024-technology-stack
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702380103759/2d589ddb-3d20-4605-8413-0989cb3c795b.png
tags: neo4j, typescript, rust, sqlite, htmx, astro, bun, qwik, elysia

---

Updated: Thursday 14<sup>th</sup> December 2023.

## TL;DR.

I plan to adopt a new technology stack in 2024. This stack includes Bun, Elysia, PostgreSQL, Astro, and Qwik: the BEPAQ Stack. I will also use programming languages like TypeScript, Rust, and HTMX (technically, a library). Along with HTML and CSS, these tools combine to make a powerful, and adaptable, application development environment.

> **Attributions:**
> 
> * [https://bun.sh/](https://bun.sh/) ***↗,***
>     
> * [https://elysiajs.com/](https://elysiajs.com/) ***↗,***
>     
> * [https://www.postgresql.org/](https://www.postgresql.org/) ***↗,***
>     
> * [https://astro.build/](https://astro.build/) ***↗,***
>     
> * [https://qwik.builder.io/](https://qwik.builder.io/) ***↗,***
>     
> * [https://www.typescriptlang.org/](https://www.typescriptlang.org/) ***↗,***
>     
> * [https://www.rust-lang.org/](https://www.rust-lang.org/) ***↗,***
>     
> * [https://htmx.org/](https://htmx.org/) ***↗,***
>     
> * [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) ***↗,*** and
>     
> * [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) ***↗.***
>     

## An Introduction.

The skills of modern app developers are partly based on an ability to adapt to new technologies. I plan to embrace a new collection of tools that are *mostly* new to me.

> The purpose of this post is to list the new technologies I plan to use in 2024.

## The Big Picture.

Computer programming. Software engineering. App development. Regardless of the name, the mission remains the same:

* Step 1: Identify the problem.
    
* Step 2: Solve the problem.
    

As a developer, I need tools that help me create my solutions. At a minimum, my app development toolkit is made up of:

* A JavaScript runtime (like Node, Deno, Bun, etc.),
    
* A web framework (like Express, Hono, Elysia, etc.),
    
* A database management system (like MySQL, SQLite, PostgreSQL, etc.),
    
* A frontend architecture (like monolithic, microservices, Astro, etc.),
    
* A frontend framework (like React, Svelte, Qwik, etc.), and
    
* Programming languages (like Rust and TypeScript).
    

Tools like Bootstrap, Tailwind, and HTMX (technically, a library) can also enhance my DX (developer experience).

The rest of this post outlines the tools and languages I plan to embrace in 2024.

## How I Quickly Adapt to New Technologies.

When learning a new language, library, runtime, or framework it is *best practice* - at least, for me - to start reading the official documentation. I usually begin with the official website, although I may also watch a YouTube tutorial or two... dozen.

Part of my learning process involves writing blog posts that regurgitate the content I find. The purpose of these posts is to:

* Minutely read the documentation, and
    
* Re-write the documentation using my own voice.
    

This process ensures that I completely read the documentation, and consume said documentation as part of my rewrite.

Of course, these posts are formatted so I can apply a technology when needed. Aside from the descriptive text, I also present code blocks that show practical examples of how I would deploy a technology.

I use these four steps in my learning process:

* Read.
    
* Write.
    
* Practice.
    
* Repeat.
    

I can quickly adopt a technology to achieve specific outcomes, but only practice and repetition will lead to mastering that technology. In software engineering, however, things change very quickly. Also, I do not have the time to master any specific technology. I have a tech startup to bootstrap.

The JavaScript ecosystem is a mess but learning the concepts behind its popular tools can make the JavaScript landscape more navigable. Maybe. Who knows?

## Developer Toolkit.

Deciding on the tools that make up my technology stack was an arduous and time-consuming endeavour. The main problem was the vast array of available tools, compounded by the similar features many of them shared. Eventually, I was able to whittle down the list of tools in my toolbox.

It took a while.

These are the development tools I will adopt in 2024.

> NOTE: This list does NOT include the AI tools I'm currently exploring.

### Bun.

[Bun](https://bun.sh/) ***↗*** is a JavaScript runtime. Choosing this tool over Node or Deno was a tough decision. The real question was: Do I need flexibility or speed? Bun is currently the fastest JS runtime available, but there is more to it than meets the eye. [This Bun post](https://solodev.app/bun-an-introduction) introduces many utilities that ship with this server-side tool.

### Elysia.

[Elysia](https://elysiajs.com/) ***↗*** is a backend web framework. Other web frameworks, like [Express](https://expressjs.com/) ***↗*** and [Hono](https://hono.dev/) ***↗,*** are just as easy to use, but Elysia is supercharged by (1) the Bun runtime, (2) Static Code Analysis, and (3) various micro-optimizations. It outperforms other tools in similar situations while also supporting TypeScript.

### PostgreSQL.

PostgreSQL is an object-relational database management system (ORDBMS) that originated from [**POSTGRES, Version 4.2**](https://dsf.berkeley.edu/postgres.html) at the University of California's Berkeley Computer Science Department. As an open-source descendant, it supports a significant portion of the SQL standard, offers many modern features, and is highly extensible. With its liberal license, PostgreSQL is free for any use, including private, commercial, or academic purposes.

### Astro.

[Astro](https://astro.build/) ***↗*** is a frontend architecture for creating web applications using popular UI frameworks like React, Vue, or Qwik. It's ideal for building content-driven websites such as blogs, marketing, and e-commerce sites. Known for reducing JavaScript overhead and complexity, Astro offers excellent SEO and performance, evolving from a static site builder to a powerful, dynamic, web application architecture.

### Qwik.

[Qwik](https://qwik.builder.io/docs/qwikcity/) ***↗*** is a frontend JavaScript framework that enhances speed and performance by serializing components and event handlers. Similar to *React*, *Vue*, and *Svelte* in component authoring, it delivers instantly interactive Live HTML without the need for hydration. By using Resumability, Qwik applications execute event handlers immediately upon user interaction, resulting in performant applications by default.

## Programming Languages.

I have already covered the fundamental similarities that are [shared between high-level programming languages](https://solodev.app/the-first-principle-of-software-syntax). However, different languages can be divided into three categories:

* Performance languages like Rust, C/C++, and Zig,
    
* Friendly languages like JavaScript, HTMX (technically, a library) and Python/Mojo, and
    
* Profitable languages like TypeScript, C#, and Java.
    

Below are the programming languages I will adopt in 2024.

### TypeScript: A Profitable Language.

[TypeScript](https://www.typescriptlang.org/) ***↗*** is a version of JavaScript with extra features. It can run regular JavaScript programs but also has added capabilities. JavaScript uses dynamic typing, which can cause issues with data types being incorrect or changing during the program's execution. TypeScript solves these problems by using a strong, static typing system.

### HTMX: A Friendly Language (though technically, a library).

[HTMX](https://htmx.org/) ***↗***(technically, a library) is a compact (14k min. gzipped) and dependency-free JavaScript library that enables the creation of cutting-edge user interfaces using the simplicity and power of hypertext (markup). It offers access to AJAX, CSS Transitions, WebSockets, and Server-Sent Events directly in HTML through the use of attributes.

### Rust: A Performant Language.

[Rust](https://www.rust-lang.org/) ***↗*** is a systems programming language focused on safety, concurrency, and performance. Its features include strong memory safety guarantees, zero-cost abstractions, and a strong static type system. It allows developers to write high-performance code without sacrificing safety and reliability.

## The Results.

In 2015, I switched from the LAMP stack (Linux, Apache, MySQL, PHP) to the MEVN stack (MariaDB, Express, Vue, Node). These tools introduced me to the JavaScript ecosystem. Other technology stacks are/were also available, like the React-based MERN stack and the Angular-based MEAN stack.

Knowing how to use a technology stack is crucial to tackling various software development challenges. Limiting my technologies to the BEPAQ Stack (Bun, Elysia, PostgreSQL, Astro, and Qwik), along with programming languages such as TypeScript, HTMX (technically, a library), and Rust, allows me to focus my efforts on building powerful applications in 2024.

## In Conclusion.

The process of learning new tools involves reading, writing, practising, and repeating. Despite the potential challenges, I'm always excited to dive into new technologies, drawing on my past experiences of adapting to interesting programming techniques and languages. Using new-ish tools in my workflow will undoubtedly be a difficult learning experience, but one that I'm ready to accept.

Also, I like acronym I came up with: BEPAQ.

Until next time: Be safe, be kind, be awesome.