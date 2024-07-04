---
title: "The Magic of VMs and Containers."
seoDescription: "Discover virtualization through hypervisors and container managers, enhancing workload optimization, resource utilization, and virtual deployment."
datePublished: Mon Jun 19 2023 08:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clj2kh8fm01vj54nv17oa661q
slug: the-magic-of-vms-and-containers
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700726974656/f976c910-55a3-4b40-bd13-819597a07192.png
tags: virtual-machines, hypervisors, application-containers, system-containers, container-managers

---

Updated: Wednesday 11th October 2023.

## TL;DR.

Virtualization has evolved significantly since its inception in the 1960s, with hypervisors and container managers playing crucial roles in managing resources and creating virtual environments. Virtual machines and application containers have revolutionized workload optimization and resource utilization, while modern container managers offer versatile solutions for deploying both Linux containers and virtual machines.

## An Introduction.

Computer hardware is expensive, especially server hardware. In the early days (circa 1950s and 1960s), only large corporations could afford to own these room-sized servers. At the end of each working day, these massive machines were shut down for the night. Then one day, someone had the bright idea of renting out their spare processing capacity for others to use. But how can this be achieved?

> The purpose of this post is to present a number of techniques for safely running multiple systems on a single computer.

## In the Beginning...

In 1968, a significant milestone in the history of computing was achieved by IBM's Cambridge Scientific Center (CSC), which also had strong connections with the prestigious Massachusetts Institute of Technology (MIT). The CSC team developed a groundbreaking mainframe computer that was specifically designed to support the CP/CMS operating system. CP/CMS, which stands for Control Program/Cambridge Monitor System, was a highly advanced time-sharing operating system that saw widespread usage from the late 1960s until the early 1970s. One of the most remarkable features of CP/CMS was its pioneering support for virtualization technology, which allowed multiple users to access and utilize the system's resources simultaneously. This innovative approach laid the foundation for many modern computing concepts and has had a lasting impact on the development of subsequent operating systems and virtualization techniques.

## Hypervisors.

In the realm of contemporary computing, a cutting-edge virtualization program is commonly referred to as a hypervisor. Functioning as a virtual machine manager, the hypervisor plays a crucial role in the creation, execution, and administration of virtual machines. This advanced technology has its roots in the pioneering support for virtualization, which has had a lasting impact on the development of subsequent operating systems and virtualization techniques.

Hypervisors are designed to abstract the physical hardware of a server, thereby allocating "virtual" resources such as processing power, memory, and storage, to the virtual machines that run on top of the hardware. This abstraction allows multiple users to access the system's resources simultaneously.

One of the key responsibilities of a hypervisor is to ensure that virtual machines remain independent from one another. This independence allows each virtual machine to run its operating system, without interference from other virtual machines sharing the same physical hardware. This isolation is essential for maintaining the stability and security of each virtual environment, as it prevents potential conflicts and vulnerabilities that could arise from shared resources.

There are two primary types of hypervisors: Type 1, or "bare-metal" hypervisors, which run directly on the hardware of the host machine, and Type 2, or "hosted" hypervisors, which operate within a conventional operating system. Both types of hypervisors have their unique advantages, depending on the specific goals of a virtualization deployment.

Hypervisors represent a significant advancement in virtualization technology, enabling the efficient allocation of resources, and the seamless management of multiple virtual machines. By ensuring the independence, and isolation, of each virtual environment, hypervisors have laid the groundwork for many modern computing concepts, and continue to play a vital role in the ongoing evolution of operating systems, and virtualization techniques.

## Type 1 Hypervisors.

Type 1 hypervisors, commonly referred to as "bare-metal" hypervisors, operate directly on the server hardware, without the need for an underlying *host* operating system. This characteristic makes them particularly popular in environments where efficiency, and performance, are of utmost importance. A type 1 hypervisor features a tightly integrated operating system within the hypervisor itself, which is extremely optimized, resulting in minimal resource consumption.

These "bare-metal" hypervisors have been specifically designed to manage hardware resources efficiently, ensuring that each virtual machine operates independently, and securely. These hypervisors provide a stable, and reliable, foundation for running multiple virtual environments concurrently, without compromising on performance, or security. This has made them the go-to choice for many enterprises, and data centres, that require high levels of virtualization.

Some well-known examples of Type 1 hypervisors include VMware vSphere, Microsoft Hyper-V, Oracle VM Server, Citrix Hypervisor, and the Linux KVM (kernel-based virtual machine). Each of these solutions offers its own unique set of features, and capabilities, catering to different use cases, and requirements. However, they all share the common goal of delivering efficient, secure, and scalable virtualization solutions, that can adapt to the ever-evolving landscape of modern networks.

## Type 2 Hypervisors.

Type 2 hypervisors, also referred to as "hosted" hypervisors, exhibit a range of functionalities that are quite similar to those of type 1 hypervisors. The primary distinction between the two lies in the fact that type 2 hypervisors operate on server, or desktop, operating systems, rather than directly on the hardware. Consequently, type 2 hypervisors have relatively limited resources available for their virtual machines, as the underlying operating system also demands a share of these resources.

Despite this limitation, type 2 hypervisors offer a notable advantage in that they can be executed on a daily-driver personal computer, coexisting seamlessly with other desktop applications. This makes them an attractive option for users who require virtualization capabilities without the need for dedicated hardware, or specialized infrastructure.

Some prominent examples of type 2 hypervisors include VMware Fusion, Microsoft Virtual PC, and Oracle VirtualBox. These solutions have their strengths and weaknesses, but later, I'll introduce a modern alternative to hypervisors called container managers.

## Virtual Machines.

The primary objective of a virtual machine is to emulate the computing environment of a physical computer, thereby providing a flexible, and efficient, platform for running various applications. Virtual machines consist of a kernel and incorporate their own, distinct operating systems. This is made possible by the hypervisor, which ensures that each virtual machine remains isolated from the others, effectively preventing any interference or conflicts between virtual machines.

Within a virtual machine, an operating system can execute typical OS functions, such as running multiple processes concurrently. Virtual machines are "virtual environments" that are equipped with "virtual resources" such as CPU, GPU, RAM, and storage. These virtual resources, however, are derived from the actual resources of the physical host machine. The hypervisor plays a crucial role in managing, and abstracting, these resources, making them available to the virtual machines as needed.

Resource allocation by the hypervisor is a key factor that enables multiple virtual machines to operate simultaneously on a single server. This efficient distribution of resources is what makes virtual machines a cost-effective solution for computing tasks. By allowing multiple virtual environments to share the same physical hardware, organizations can optimize their infrastructure, and reduce overall costs.

Virtual machines replicate the computing environment of a physical computer, complete with their own kernels and operating systems. The hypervisor is responsible for maintaining a separation between virtual machines and managing the allocation of resources. This efficient use of resources allows multiple virtual machines to run concurrently on a single server, making them a cost-efficient option for networking needs.

## Application Containers.

Application containers are specifically engineered to efficiently execute a single process, making them distinct from virtual machines. As amorphous entities, application containers possess a unique ability to "spin up" and "power down" as needed, allowing them to scale dynamically according to the demand for their processes. This on-demand scalability can lead to significant cost reductions, energy savings, and the efficient allocation of unused processing power to other tasks, such as database optimizations.

One notable advantage to application containers is their considerably smaller size compared to virtual machines. This is primarily because, unlike a virtual machine which contains a full operating system, an application container only includes the essential resources it needs to perform a specific operation. This streamlined design results in a more lightweight and efficient solution for running applications.

Docker is a widely recognized, and popular, example of an application container. It has become the industry standard for containerization, offering a robust platform for developers to build, package, and distribute contained applications.

## Container Orchestrators.

To manage multiple application containers, specialized container orchestrators are available, including but not limited to Kubernetes, K3s, and Portainer. These tools streamline the process of deploying, scaling, and monitoring application containers, ensuring optimal performance and efficient resource utilization.

Docker, a highly acclaimed and widely adopted example of an application container, had rapidly emerged as the industry standard for application containment. It provides a powerful and versatile platform that enables developers to effortlessly build, package, and distribute applications within self-contained environments without the overhead of using virtual machines. This results in a more lightweight and efficient solution for running applications and allows for seamless portability across different systems.

By leveraging the capabilities of these container orchestrators, developers and IT professionals can effectively manage the entire lifecycle of application containers, from creation and deployment to scaling and monitoring. This, in turn, enables organizations to rapidly deploy new applications, scale existing ones, and maintain a high level of reliability, all while minimizing resource usage.

## System Containers.

Modern container managers play a crucial role in the creation, execution, and deletion of system containers. These container managers can either operate within an existing host operating system, akin to type 2 hypervisors or run on "bare-metal" due to a tightly integrated operating system, similar to type 1 hypervisors. It is important to understand that Linux-based system containers are NOT virtual machines, despite sharing *a lot* of similarities with that technology.

Container managers facilitate the launching, running, and deletion of Linux-based system containers which, like virtual machines, are used to contain operating systems. However, Linux-based system containers differ from virtual machines in that they share the kernel of the host operating system, or integrated OS, as the case may be. Additionally, application libraries and dependencies from the host/integrated operating system are bound to each system container. Using resources from the host/integrated operating system ensures that Linux-based system containers can provide a more streamlined, performant experience while reducing the container size.

These OS bindings offer substantial advantages when using Linux-based system containers over virtual machines, particularly in terms of compute resource efficiencies. These efficiencies encompass various aspects of the system, including CPU, GPU, RAM, and storage. The shared kernel and bound libraries contribute to a more lightweight and efficient system container, which is especially noticeable compared to virtual machines.

Interestingly, modern container managers can also create virtual machines, further expanding their versatility. Some notable container managers include Proxmox VE and LXD (LinuX Daemon). These container managers provide developers with access to the flexibility of Linux-based system containers.

## Proxmox VE: A Modern Container Manager.

At the core of Proxmox VE lies a powerful combination of two virtualization technologies: The Linux KVM (Kernel-based Virtual Machine) and Linux-based system containers. Proxmox VE boasts a user-friendly, browser-based graphical user interface (GUI) that simplifies the management of system containers, and virtual machines.

Another feature of Proxmox VE is the integration of a highly optimised operating system that requires a "bare-metal" installation. On the surface, the operating system integration makes Proxmox VE appear very similar to a type 1 hypervisor. However, hypervisors produce virtual machines. Proxmox VE, on the other hand, manages system containers... and virtual machines, if you need them.

As a modern container manager, Proxmox VE offers a seamless experience for developers seeking the versatility of Linux-based system containers, while also providing an option to utilize virtual machines if needed. This technology provides a more optimised virtualization solution that caters to a wide range of requirements.

## LXD: Another Modern Container Manager.

Unlike Proxmox VE, which features a highly optimized operating system, LXD operates as a background process, a daemon, that runs on any Debian-based operating system. However, LXD is typically run on Ubuntu Server or Ubuntu Desktop, as Canonical is the developer of both the LXD and Ubuntu technologies.

LXD is designed to cater to the diverse needs of developers seeking the flexibility, and versatility, of Linux-based system containers. This container manager is efficient at spinning up, managing, and deleting system containers, while also offering the capability of creating virtual machines through the use of the \`--vm\` flag. LXD provides a comprehensive virtualization solution that caters to a wide range of requirements.

In contrast to Proxmox VE, which features a browser-based graphical user interface, LXD employs a terminal-based interface for streamlined and efficient container management. This interface allows developers to have direct control over their virtual environments, while also reducing the complexity associated with graphical interfaces. LXD offers a modern solution to developers who want a contained foundation on which to build their projects.

## The Third Wave: Virtualization Evolved.

There is talk of a Third Wave building in the shallow seas of virtualization, an overwhelming flood of technical innovation, a tsunami threatening to engulf whole swathes of computer programmers and software developers.

Of course, I'm talking about WASM and WASI.

WASM, or web assembly, is a binary format and portable compilation target for programming languages like C/C++, Rust, and JavaScript. It is a memory-safe, sandboxed environment that can run inside existing JavaScript virtual machines. On the web, WASM adopts the same-origin and permissions security policies of the browser. Even non-web embeddings are possible, from minimal shells for testing to full-blown application environments like servers in datacenters, running on IoT devices, or built into mobile and desktop apps. Portability can be achieved either at compile-time (e.g. using the C/C++ `#ifdef` directive) or run-time (via feature detection and dynamic loading/linking). WASM has a lot of potential.

WASI, or web assembly system interface, is a WASM API that provides access to several operating-system-like features, including files and filesystems, Berkeley sockets, clocks, and random numbers. It is browser-independent so it doesn't depend on Web APIs or JavaScript, and isn't limited by the need to be compatible with JS. WASI has integrated capability-based security and extends WASM's characteristic sandboxing to include I/O. Two toolchains currently work well with WASI: The Rust toolchain and a specifically packaged C and C++ toolchain. The options for running WASI-based programs include [Wasmtime](https://wasmtime.dev/), [WasmEdge](https://wasmedge.org/), and the [browser polyfill](https://wasi.dev/polyfill/). Embeddings for highly constrained environments (e.g. Raspberry Pi) can be achieved with [Wasmer](https://wasmer.io/) (for PHP and V) and [Wasm3](https://github.com/wasm3/wasm3). [WASI Preview 2](https://github.com/WebAssembly/WASI) continues evolving as each working group achieves its goals.

WASM and WASI represent a currently undisputed future for application development where programmers take responsibility for virtualizing their programs. Such an impending wave can mean only one thing: Surf's Up.

> Attributions:
> 
> [https://webassembly.org/](https://webassembly.org/)
> 
> [https://wasi.dev/](https://wasi.dev/)
> 
> [https://www.fermyon.com/blog/2022-02-08-hello-world](https://www.fermyon.com/blog/2022-02-08-hello-world)
> 
> [https://nigelpoulton.com/webassembly-the-future-of-cloud-computing/](https://nigelpoulton.com/webassembly-the-future-of-cloud-computing/)
> 
> [https://thenewstack.io/webassembly-isnt-software-its-a-computer/](https://thenewstack.io/webassembly-isnt-software-its-a-computer/)

## The Results.

Hypervisors, virtual machine managers, and WASM/WASI. A type 1 "bare-metal" hypervisor includes an optimised operating system and runs directly on the server hardware. A Type 2 "hosted" hypervisor operates within a conventional operating system. Virtual machines, which are deployed by hypervisors, are software emulations that behave like physical computers. Virtual machines include their own kernels and operating systems. Application containers are lightweight, standalone software packages. Application containers encapsulate the necessary runtime components, libraries, and dependencies, that are needed to run an application. Container orchestrators for application containers are used to deploy, scale, and monitor multiple application containers. Container managers are used to create, manage, and delete system containers and virtual machines. Linux-based system containers are software emulations that behave like physical computers. Linux-based system containers behave like they have their operating system, but they share the kernel, libraries, and dependencies, of the host or integrated operating system. WASM and WASI offload virtualization duties to computer programmers and application developers.

## In Conclusion.

Over the past five decades, virtualization has emerged as a critical technology (1) for businesses who want to optimize their workloads, and (2) for developers who want to share their creations. Virtual machines, and application containers, have revolutionized the way services are provided, leading to improved resource utilization, and cost savings. Application containers, and their management tools, now facilitate the deployment, scaling, and monitoring of modern applications while also streamlining the publication of digital creations. WASM and WASI are new technologies that will complement existing virtualization methods.

The evolution of virtualization technologies has had a profound impact on the way resources are shared within corporations, and across the world. With the intense popularity of mobile devices, the future of virtualization requires even more efficiencies to be found by engineers, so that developers can cater to the ever-demanding needs of the mobile business sector, and general consumers alike.

Until next time: Be safe, be kind, be awesome.