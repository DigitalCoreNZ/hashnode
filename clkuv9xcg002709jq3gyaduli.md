---
title: "Monoliths vs API Microservices vs Serverless."
datePublished: Thu Aug 03 2023 08:00:09 GMT+0000 (Coordinated Universal Time)
cuid: clkuv9xcg002709jq3gyaduli
slug: monoliths-vs-api-microservices-vs-serverless
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1699605583929/c8cf450a-e552-49da-8774-79671f7443c6.png
tags: microservices, apis, serverless, monoliths, composable-architecture

---

## TL;DR.

I compare monoliths, API microservices, and serverless architectures. Understanding their pros and cons helps me make informed choices for my software development projects.

## An Introduction.

There are three popular software architectures I would consider using under various circumstances:

* Monoliths,
    
* API microservices, and
    
* Serverless.
    

I'll explore the differences between monoliths, API microservices, and serverless architectures to better understand their advantages and disadvantages. It's important to make informed decisions regarding my software projects so they are developed, and deployed, with as little friction as possible.

Let me show where I'd use these architectures.

## Monoliths.

Monolith architecture is a software design approach where all components of an application are combined into a single codebase and deployed as a single unit, often used for self-contained desktop or smartphone apps.

In one-off instances or self-contained desktop/smartphone applications, I would employ the monolith architecture. Combining all the components of an app into a single codebase, and deploying these components as a unified structure, ensures a seamless development, and deployment, experience with minimal friction.

## API Microservices.

API microservices architecture is a software design approach in which an application is broken down into small, loosely coupled microservices that communicate with each other through APIs. This allows for better scalability, maintainability, and flexibility compared to monolithic architectures.

Using API microservices architecture is great when deploying applications across a network. A single microservice can be used by multiple applications. If a microservice should crash, only that part of the app/apps will fail and will NOT bring down the whole application. If a microservice should crash, it will only take a moment to delete that instance, and replace it with a new microservice. It is typical to operate a minimum number of instances for a particular microservice, with the operations engineer increasing this number as more applications utilizing that microservice is deployed. It is also common to automatically increase the number of instances as the demand for specific microservices increases.

## Serverless.

Serverless architecture is a design approach where applications or services are hosted by third-party providers, such as AWS Lambda, that automatically manage resource allocation. Developers write individual functions, which are triggered by events, and the provider takes care of scaling and infrastructure management.

I would use serverless architecture to enhance the API microservices architecture. Third-party providers, like AWS and their Lambda functions, can be left to automatically manage resource allocation. This approach allows me to focus on writing individual functions triggered by events, while the provider handles scaling and infrastructure management for me.

## The Results.

Monoliths, API microservices, and serverless architectures each have their own advantages and disadvantages. Choosing the appropriate architecture depends on factors such as project requirements, scalability, and infrastructure management. By understanding their pros and cons, I can make informed decisions for my software development projects.

## In Conclusion.

I've run serverless function experiments (Lambda functions on Netlify) and they are very easy to set up and use. However, I couldn't find a use case that needed these functions to solve any of my problems. Serverless, to me, feels like a solution that is looking for a problem to solve.

Monolith and API microservices, on the other hand, are very handy architectures to have in my toolkit. Building an API library for web-facing apps means I can also build OS-specific apps (Windows, iOS, iPhone, Android, Linux) with monolith architectures. The advantage? These monoliths can automatically download, and integrate, any changes to the API library. In other words, the API library becomes the single source of truth for all the apps I build and, in the same way, this blog is *MY* single source of truth for all the ideas I share.

Until next time: Be safe, be kind, be awesome.