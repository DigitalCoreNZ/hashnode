---
title: "12S: A Blueprint for Technical Design."
datePublished: Sat Jun 24 2023 09:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clj9rt0oa001w09l4gxg498dj
slug: 12s-a-blueprint-for-technical-design
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702334267762/4adc0064-8934-451d-a428-95c027f92766.png
tags: microservices, system-architecture, product-design, technical-design, design-details

---

## TL;DR.

This post explains the importance of creating a Technical Design for a software project, including the use of microservices and APIs to create a scalable, resilient, and flexible application. It reviews the purpose of using APIs, the stakeholders, intended users, business constraints, and technical constraints, and establishes a high-level system architecture using Qwik, Deno, ExpressJS, Axios, and MariaDB.

## An Introduction.

To create a practical Technical Design for a software project, it is important to first identify the needs and requirements of the system's stakeholders. This involves gathering information about the software's intended users, as well as any business or technical constraints that may impact the design.

> ***The purpose of this post is to present a process for starting new projects.***

Once these requirements have been identified, the design process can begin. This typically involves creating a high-level system architecture that outlines the major components and modules of the system, as well as the relationships and interactions between them. From there, more detailed designs can be created for each component or module, specifying the functionality and interfaces they will provide.

Throughout the design process, it is important to consider factors such as scalability, maintainability, and security. By taking these factors into account, developers can ensure that the software system will be able to meet the needs of its users both now and in the future.

Overall, a well-composed Technical Design is crucial for the success of a software project, as it serves as a roadmap for developers and ensures that all requirements are met.

## The Big Picture.

Time for a 10,000-metre overview. This section is ironically appropriate as it covers the Technical Design for the 12 Startups project where a technical design itself is a 10,000-metre overview.

I'm looking to build a collection of common microservices, the ultimate purpose of which is to save time and resources. This "library" will contain simple microservices that have just enough functionality to perform specific operations. APIs will be used to pass microservice operations into any app that needs to perform tasks for which those microservices were built. The APIs will use an HTTP client to connect the databases to the microservices, and the microservices to the apps.

To validate my proposal's functionality, I will build a simple todo app with CRUD microservices, connected to API endpoints, that can access a database.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687427801973/0fda5b97-1406-4033-8b0d-fab1eab0eb24.png align="center")

Now that I know what I want to achieve, I will start by reviewing the purpose of using microservices.

## Microservices: In Review.

In software architecture, a microservice is an approach to building applications that involves breaking down a larger application into small, independently deployable services. Each microservice is designed to perform a specific operation or function within the larger application. By breaking down the application into smaller services, it becomes easier to develop, test, and deploy each service independently.

Microservices are typically designed to be highly scalable and resilient, allowing them to handle large amounts of traffic and requests without failing. They are also designed to be loosely coupled, meaning that each service can be developed and deployed independently of the other services. This makes it easier to update or replace individual services without affecting the rest of the application.

One of the key benefits of using microservices is that they allow developers to build applications that are more flexible and adaptable to changing requirements. Because each service is designed to perform a specific function, it can be updated or replaced without affecting the rest of the application. This makes it easier to add new features or functionality to the application over time.

Microservices are a powerful tool for building scalable, resilient, and flexible applications. By breaking down a larger application into smaller, independently deployable services, developers can build applications that are easier to develop, test, and deploy, while also being more adaptable to changing requirements.

Next, I will review the purpose of using APIs.

## APIs: In Review.

In software development, an API (Application Programming Interface) is a set of protocols, routines, and tools that enable communication between different software applications. APIs are commonly used in microservices architecture, where each microservice performs a specific task or function and communicates with other microservices through APIs.

APIs provide a standardized way for different software components to interact with each other, allowing developers to build complex systems without having to worry about the underlying implementation details. By using APIs, developers can easily integrate different services and components into their applications, making it easier to build scalable, modular, and maintainable software systems.

APIs play a critical role in modern software development, enabling developers to build complex systems by breaking them down into smaller, more manageable components. By using APIs, developers can easily integrate different services and components into their applications, making it easier to build scalable, modular, and maintainable software systems.

Next, I will list the stakeholders.

## The Stakeholders.

I have a vested interest in the success of the 12 Startups project. My interests are personal, professional, technical, and business-related.

My flatmate, who is my silent partner and financial backer, also has a vested interest in the 12 Startups project. I am *very grateful* for her confidence in my abilities, as well as her quiet patience, as I slowly line up my ducks in a row.

Next, I will define my intended users.

## Intended Users.

For the most part, each of my 12 Startups primarily consists of an app that is either a business utility or a lifestyle utility. Either way, each app is designed to improve my interaction with the real world. These apps solve distinct problems that I encounter every day. Solving my own real-world problems is the foundation of my 12 Startups project.

However, these solutions might also work for others. In other words: The intended users of my apps are the same people who experience that same problems as myself.

Next, I will identify my business constraints.

## Business Constraints.

Due to my limited access to capital, I can only "employ" myself at my primary startup, Digital Core (NZ) Limited. The same financial limitation also sees me working from a tiny anteroom that connects the lounge, bedroom, bathroom, garage, and stairs to the top floor. Yes, my "office" has five doors, and my flatmate is always passing through as she heads to... somewhere else.

Next, I will pinpoint my technical constraints.

## Technical Constraints.

As much as I would like to use every technology under the sun, that would be a waste of time, a waste of money, and a waste of my sanity.

The table below lists five technologies that I will use to build the 12 Projects:

| Name | Purpose |
| --- | --- |
| Deno | A JavaScript runtime. |
| MariaDB | A relational database. |
| Axios | A lightweight HTTP client. |
| ExpressJS | A popular web framework. |
| Qwik | A very fast web framework. |

Other technical constraints include:

* Using a 10th Gen Intel NUC, 2-core/4-thread `homelab` with 40Gb RAM,
    
* Using a Ryzen5, 6-core/12-thread `workstation` with 16Gb RAM,
    
* Inexperience with using Qwik and Deno to build apps, and
    
* Limited Internet bandwidth (450Mb/s up, 900Mb/s down).
    

Next, I will establish a high-level system architecture.

## A High-Level System Architecture.

Qwik is a modern web framework that is built to run on Deno, a secure runtime for JavaScript and TypeScript. ExpressJS, another popular web framework, can also run on Deno. Axios is a lightweight HTTP client that can be used to make API requests. And MariaDB is a popular open-source relational database.

My chosen system architecture consists of a frontend UI, which communicates (using Axios) with a backend (built with Qwik, ExpressJS, Axios, Deno, and MariaDB). Axios can be used to make API requests between the frontend, the backend, and the database. The database is used to store data, which can be accessed and updated through the APIs.

Overall, this system architecture provides a secure and scalable solution for building web applications with Qwik, ExpressJS, Axios, Deno, and MariaDB.

Next, I will clarify these technologies' relationships and interactions.

## Relationships and Interactions.

Qwik and ExpressJS are web frameworks that can run on the Deno runtime. They both allow me to build HTTP servers, define routes, handle requests, and respond to clients.

Deno is a JavaScript runtime that can run the Qwik and ExpressJS web frameworks.

Axios is an HTTP client that can make HTTP requests from both Qwik and ExpressJS applications to external APIs or databases.

MariaDB is a relational database and can be used with applications built with Qwik or ExpressJS. Qwik and ExpressJS applications can connect to MariaDB using a database driver like MariaDB and perform CRUD operations.

A Qwik/ExpressJS application can expose an API that Axios makes requests to.

The Qwik/ExpressJS application can then query the MariaDB database and return the data in the response to Axios.

In summary:

* Deno is the runtime environment for Qwik and ExpressJS,
    
* Qwik/ExpressJS are frameworks that build HTTP servers,
    
* Axios allows Qwik/ExpressJS to make HTTP requests, and
    
* MariaDB is used as the database.
    

These technologies work together as a full-stack development environment. This technology stack can be used to build a database, API connectivity, microservice functionalities, and a client-side user interface.

Next, I will describe my design details.

## Design Details.

My design is based on building an extensible collection of loosely coupled microservices. As time goes by, the number of microservices will increase and, as a consequence, the overall functionality of this collection will also expand.

To fully realise the separation of concerns between the app, the microservices, and the database, I will design, and run, an experiment that uses three LXCs (<mark>L</mark>inu<mark>X</mark> <mark>C</mark>ontainers) to hold each technology. That way, the only way for the app, microservices, and database to interact with each other is to use well-defined APIs.

Next, I will illustrate the functionalities and interfaces.

## Functionalities and Interfaces.

To successfully implement this experiment, it is crucial to identify the necessary functionalities and interfaces. The following aspects should be considered:

1\. User Interface (UI): A user-friendly and visually appealing interface is essential for the todo app. This interface should provide a seamless experience for users to input their information, such as a todo item, and include mechanisms to mark and remove completed items.

2\. API Endpoints: Clearly defined API endpoints are necessary for the communication between the app, the microservices, and the database. These endpoints should be designed to handle various tasks, such as data storage, data retrieval, data marking, and data removal.

3\. Data Validation: Implementing data validation functionality within the microservices will ensure that the information provided by users is accurate and adheres to the required format. This functionality will help maintain data integrity and prevent potential issues that may arise from incorrect or incomplete data.

4\. Database Schema: A well-structured database schema is crucial for organizing and storing user data efficiently. This schema should be designed to accommodate the necessary data fields, relationships, and constraints, while also being scalable to support future growth.

5\. Security Measures: Implementing robust security measures is essential to protecting user data and maintaining the overall integrity of the system. This includes encryption of sensitive data, secure API authentication, and proper access control mechanisms.

6\. Error Handling and Logging: Developing a comprehensive error handling and logging system will help identify and resolve any issues that may arise during the operation of the app, the microservices, and the database. This system should be designed to provide detailed information about errors, allowing for efficient troubleshooting and resolution.

By addressing these processes, the experiment can be effectively designed and executed, ensuring seamless interaction between the app, the microservices, and the database, through well-defined APIs.

Next, I will focus on scalability.

## Scalability.

While the initial implementation of the system may not yet incorporate scalability features, it is crucial to address this aspect to ensure the long-term success and adaptability of the project. Scalability refers to the ability of the system to handle an increasing workload, user base, or data volume without compromising performance or functionality. By considering scalability from the outset, I can design and execute the experiment more effectively, allowing for seamless interaction between the app, the microservices, and the database through well-defined APIs.

There are several key factors to consider when addressing scalability:

1\. Horizontal vs. Vertical Scaling: Horizontal scaling involves adding more machines to the system, while vertical scaling involves increasing the capacity of existing machines. Both approaches have their merits and should be evaluated based on the specific requirements of the project.

2\. Load Balancing: Efficiently distributing incoming network traffic across multiple servers can help ensure that no single server is overwhelmed, maintaining optimal performance and availability.

3\. Data Partitioning: Dividing the data into smaller, more manageable chunks can help improve performance and facilitate horizontal scaling.

4\. Caching: Storing frequently accessed data in memory can help reduce the load on the database and improve response times.

5\. Asynchronous Processing: Offloading time-consuming tasks to background processes can help maintain system responsiveness and prevent bottlenecks.

By addressing these factors and incorporating scalability considerations into the design and execution of the experiment, I can ensure that the system is well-equipped to handle future growth and changing demands, ultimately contributing to the project's long-term success.

Next, I will cover the importance of maintainability.

## Maintainability.

Maintainability is a crucial aspect that significantly contributes to the overall success of any project, particularly in the context of system responsiveness and preventing bottlenecks. For the 12 Startups project, adopting a microservices and API architecture is primarily driven by the need to enhance maintainability. This approach allows for the efficient management of individual components, ensuring that the system remains adaptable and resilient in the face of evolving requirements and future growth.

By breaking down the system into smaller, more manageable units, microservices architecture enables me to independently update, deploy, and scale each component without affecting the entire system. This modularity not only simplifies the development process but also reduces the risk of introducing errors or complications when making changes. Moreover, the use of APIs facilitates seamless communication between these microservices, further promoting maintainability by allowing for easy integration and interoperability.

Incorporating a maintainability design ensures that the system is prepared for the demands of growing *beyond* 12 Startups. This attitude contributes to a long-term lifecycle that fosters an infrastructure that is geared for growth.

## Security.

It is crucial to prioritize security throughout the development process. This involves implementing robust security measures to protect sensitive data and ensure the integrity of the system. Regular security audits and vulnerability assessments should be conducted to identify and mitigate potential risks.

## My Recovery Plan and Iteration Strategy.

One of the most important parts of my developer experience is experimentation. I need to know if my proposed designs/architectures are as effective, and efficient, as possible. My experiments need a common base from which measurements can be taken, so I need a standard platform on which to iterate my build versions.

### Images: My Recovery Plan.

The first part of building a standard platform is to have a collection of images that can be used as recovery points. Below are the two most recent images (as of this post) that I created using [Clonezilla Live](https://clonezilla.org/clonezilla-live.php):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687583583171/a0da971c-f13c-476d-8724-127f6c74d881.png align="center")

If my `homelab` becomes incomprehensibly unstable, I can use one of these images to restore my platform to a previous state. (Older images are moved to the NAS.)

### IaC: My Iteration Strategy.

The other part of building a standard platform involves using Infrastructure as Code (IaC) to build, and prepare, the servers. Once built, I can measure the efficiency of a server and compare the results with other servers that were built with different settings.

My IaC technologies of choice are Terraform (for server and container builds) and Ansible (for server and application settings).

## The Needs of Today.

I need to establish a strong testing and quality assurance process to ensure the system functions as intended and meets my desired performance standards. This includes implementing automated testing, continuous integration, and continuous deployment to streamline the development process and minimize potential issues.

I need to invest in proper documentation and knowledge sharing to make it easier for stakeholders and investors to understand why this system is appropriate to our needs. This will help to promote long-term support for the project, and improve my ability to adapt to the evolving needs of our clients and users.

By investing in QA/QC and knowledge sharing, I will be well-equipped to successfully build a quality project that is understood by everyone involved.

## The Needs of the Future.

Preparing for an uncertain and unpredictable future can be a daunting and risky strategy to embrace. Rather than leaving things to chance, it may be significantly more beneficial to proactively influence the direction in which my future unfolds. By taking charge and shaping my own path, I can better align my actions with the ever-changing needs of our clients and users, ensuring that the project remains relevant and valuable to my stakeholders and investors.

Embracing this proactive mindset will allow me to anticipate potential challenges and opportunities that will arise in the future. By staying ahead of the curve, I can develop innovative solutions and strategies that will ensure the continued success and growth of this project. In this way, I can confidently navigate the complexities of an ever-changing landscape, and create a future that is not only more secure but also more aligned with the needs and desires of all those who rely on the project's success.

## Expanding the Microservices Collection.

Beyond this simple todo app (which, I might add, is NOT one of the 12 Projects) is a future of untapped creativity and a reservoir of pure potential. As important as the CRUD microservices are, they pale into insignificance compared to... The Register microservice, or the Image Compression microservice. Each microservice is built with a simple code base and a basic objective to achieve. Its strength lies not in what a microservice can do. Its power is derived from the impact that a Microservices Collective wields.

## A Custom Solution for Each Startup.

Many functions are similar across multiple apps: Register, Login, and Recover Password to name a few examples. However, if each app is designed to solve a specific problem, then there is still a lot of opportunities to write custom code. JavaScript, TypeScript, and WASM compiled with Rust, everything is allowed when you're a modern app developer.

## The Results.

Creating a Technical Design for a software project is vital for its success. By adopting a microservices architecture and leveraging technologies such as Qwik, Deno, ExpressJS, Axios, and MariaDB, developers can build scalable, resilient, and maintainable applications. Focusing on aspects like scalability, maintainability, and security ensures the system is prepared for both present and future needs. Investing in proper documentation, QA/QC, and knowledge sharing will further contribute to the project's long-term success and adaptability.

## In Conclusion.

A Technical Design is usually the first step toward a much larger, and busier, world. In this draft, I skipped a few sections, including design trade-offs and data modelling because... well, I forgot to include them. Some of the sections above are even cursory. (Yes, "Security" section. I'm looking at you!) My first attempt at drafting a design document has many weaknesses. I waffle in some sections while others are bereft of any substance. Luckily, I have at least 12 opportunities to hone my documenting abilities. Also, there's another template I need to create: A Blueprint for Product Design.

"Practice is the only path to developing any skill." - Me, just now.

Until next time: Be safe, be kind, be awesome.