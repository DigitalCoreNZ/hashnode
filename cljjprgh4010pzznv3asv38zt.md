---
title: "The Modular AI Engine and Mojo Programming Language."
datePublished: Sat Jul 01 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: cljjprgh4010pzznv3asv38zt
slug: the-modular-ai-engine-and-mojo-programming-language
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698960591135/02f5c875-9d80-4ff9-b6a8-542a935ae8ff.png
tags: python, swift, llvm, mojo, chris-lattner

---

## TL;DR.

Modular AI, founded by Chris Lattner, aims to revolutionize the AI and machine learning landscape by unifying disparate resources with its Modular AI Engine and Mojo programming language. Lattner's previous contributions to software engineering include LLVM, Clang, Swift, MLIR, and TPU, showcasing his ability to create impactful technologies.

## An Introduction.

Python developers and AI modellers, rejoice!! For [Modular AI](https://www.modular.com/) will lighten your load and light your way!! Yes, I sound like an acolyte exalting the virtues of The Way (and if I was [Grogu's](https://en.wikipedia.org/wiki/Grogu) dad, then I'd be right) but it feels like 2023 will be an inflexion point for historians to point at, and say "This is when it started."

> ***The purpose of this post is to present a tool for improving the AI development ecosystem.***

To understand how, and why, [Modular AI](https://www.modular.com/) will have such a massive impact beyond engineering and science, we need to look at the historical projects of the Modular AI CEO and co-founder, Chris Lattner, and only *then* can we extrapolate the importance of the Modular AI Engine and the Mojo programming language.

## LLVM: A Compiler for Building Compilers.

LLVM (Low-Level Virtual Machine) was created by Chris Lattner while he was a graduate student at the University of Illinois at Urbana-Champaign. He initially started working on LLVM in 2000 as a research project, but it later evolved into a complete compiler infrastructure that is widely used in the industry today.

LLVM is an open-source project that provides a set of modular and reusable compiler and toolchain technologies. It includes a powerful optimizer and code-generation toolchain, as well as a wide range of programming language front ends for languages such as C, C++, Objective-C, Fortran, Rust, Swift, and many others.

LLVM has become a popular choice for compiler developers and toolchain engineers because of its flexibility, modularity, and ease of use. It is used in a wide range of embedded systems, server-side applications, game development, and other areas where high-performance code generation is important. Additionally, LLVM has been used as the basis for Apple's Swift programming language, as well as Google's upcoming Fuchsia operating system.

LLVM is language-agnostic but has spawned frontend languages and compilers, including ActionScript, Ada, C#, Common Lisp, PicoLisp, Crystal, CUDA, D, Delphi, Dylan, Forth, Fortran, FreeBASIC, Free Pascal, Graphical G, Halide, Haskell, Java Bytecode, Julia, Kotlin, Lua, Objective-C, OpenCL, PostgreSQL's SQL and PLpgSQL, Ruby, Rust, Scala, Swift, Xojo, and Zig.

> **Attribution:**
> 
> [Wikipedia](https://en.wikipedia.org/wiki/LLVM#:~:text=Originally%20implemented%20for%20C%20and,%2C%20Crystal%2C%20CUDA%2C%20D%2C)

## Clang: Forcing GCC to Up their Game.

Competition is good for GCC (GNU Compiler Collection). Clang is an open-source C/C++/Objective-C compiler, which is based on LLVM, a modular and reusable compiler infrastructure. This was another special project from Lattner.

Clang is known for its high performance, low memory usage, and strict adherence to C, C++, and Objective-C standards. It supports a wide range of operating systems including Linux, macOS, and Windows, and it is integrated with many development tools and Integrated Development Environments (IDEs) like Xcode, Visual Studio, and Eclipse, as well as build systems like CMake, Ninja, and Gradle.

Clang also has a number of unique features that set it apart from other compilers. For example, it has a powerful static analyzer that can detect potential bugs *in your code* without even running it, and it also has a modular architecture that makes it easy to add new functionality to the compiler. Additionally, because it is built on LLVM, Clang can leverage many of the advanced optimization features provided by LLVM, resulting in faster and more efficient code.

## Swift: Pushing Objective-C to the Sideline.

Swift is a powerful and intuitive programming language developed within Apple Inc. because Lattner, an employee at the time, thought it might be a good project. Swift is used to build apps for iOS, macOS, watchOS, and tvOS systems.

Swift was first introduced at Apple's Worldwide Developers Conference (WWDC) in 2014 and, since then, has rapidly gained popularity among developers due to its speed, safety, and expressiveness. It is designed to be easy to use and provides a modern syntax that is similar to other popular programming languages, such as Python and Ruby.

Swift is an open-source language, which means that it can be easily accessed and modified by developers. It also offers several features, such as optionals, tuples, closures, and generics, that simplify the development process and make it easier to write clean and concise code.

A significant benefit of using Swift is its performance. It is designed to be fast and efficient, which makes it ideal for developing high-performance apps. Additionally, Swift is type-safe, which means it catches errors at compile-time, and offers strong support for functional programming.

Overall, Swift is a versatile and powerful programming language that is well-suited to developing a wide range of applications for Apple platforms and beyond.

## MLIR: Another Compiler for Building Compilers.

Co-founded by Lattner, MLIR (Multi-Level Intermediate Representation) is a cutting-edge compiler infrastructure developed by Google, which aims to define a common intermediate representation (IR) format for a wide range of compilers.

The goal of MLIR is to make it easier to build custom tools and systems by enabling effective translation and transformation of code across different high-level programming languages and hardware platforms. For example, it can be used to implement compilers, code generators, and other optimization tools.

One of the key features of MLIR is its ability to represent code at different levels of abstraction, making it an ideal choice for heterogeneous computing systems that run different types of programs at different levels of optimization. It achieves this by using a modular and extensible design that supports independent and composable dialects for other programming languages and hardware targets.

Another important aspect of MLIR is that it is designed to be efficient and scalable, which makes it suitable for large-scale software development projects. It provides a set of built-in optimization passes and tools, such as the MLIR optimizer and the MLIR rewrite tool, which can be used to improve the performance and maintainability of code written in different programming languages.

Overall, MLIR is a powerful and flexible compiler infrastructure that can help developers to build more efficient and optimized software for a wide range of platforms and use cases.

## TPU: Helping to Train those AI Models.

TPU (Tensor Processing Unit) is a specialized hardware accelerator that is designed to speed up machine learning workloads, particularly those that involve neural networks. TPUs are developed by Google and are available as a service on Google Cloud. Lattner "**helped scale ML systems globally (while) bringing Google Cloud TPUs to market, unifying the ML compiler stack at Google (and beyond) with MLIR, (while) scaling Google's SW and HW on both server and edge to impact billions of users.**"

Unlike CPUs and GPUs, which are general-purpose processors, TPUs are specifically optimized for tensor operations and can perform matrix multiplication and other tensor operations much faster than CPU- and GPU-based calculations.

TPUs are particularly useful for large-scale machine learning workloads, such as training deep neural networks, because they can process large amounts of data in parallel and deliver results much faster than traditional processors. They are also very energy-efficient, which makes them a great choice for running machine learning workloads that require a lot of computation power.

## CEO and Co-Founder at Modular AI.

Christopher Arthur Lattner is an American software engineer. He has worked at Google, Tesla, and Apple. Over the past 20-something years, Lattner has made incredibly significant contributions to the engineering field.

In 2022, Lattner co-founded and is the CEO of Modular AI, an artificial intelligence platform for developers.

## How Modular AI Will Change the World.

Modular AI is the first-ever attempt to unify the disparate resources that are used in AI, machine learning, and deep learning. Modular AI Engine (the inference engine) and the Mojo programming language (a Python superset) are the two products that lay at the heart of Modular AI.

Lattner is a well-respected engineer who knows how to follow through on his visions and, in the past, has united corporate interests behind singular projects. Modular AI will change the world because Lattner knows things *need* to change.

## The Results.

In conclusion, Modular AI, led by the visionary Chris Lattner, has the potential to revolutionize the AI and machine learning landscape by unifying disparate resources through its Modular AI Engine and Mojo programming language. Drawing from Lattner's past successes in creating impactful technologies such as LLVM, Clang, Swift, MLIR, and TPU, it is expected that Modular AI will significantly impact not only engineering and science but also the world as a whole.

## In Conclusion.

As I work my way through the Modular AI documentation while exploring the Playground, I can see my follow-up posts will contain more details about the technologies I find and my experiences with the ecosystem. My immediate future is full of fun technologies and sparkly processes. Neat-o.

Until next time: Be safe, be kind, be awesome.