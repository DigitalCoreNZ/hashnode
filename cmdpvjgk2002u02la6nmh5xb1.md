---
title: "A Look into the BMAD Method."
seoDescription: "BMAD Method: AI framework with Agile methodology for customizable agents and flexible workflows that enhance efficiency and quality."
datePublished: Wed Jul 30 2025 11:20:10 GMT+0000 (Coordinated Universal Time)
cuid: cmdpvjgk2002u02la6nmh5xb1
slug: a-look-into-the-bmad-method
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753865265397/362312fb-8b6f-4a9d-adac-f37664c52de1.png
tags: software-development, agile-development, software-engineering, development-workflow, ai-integration, agile-methodologies, tech-innovation, techbestpractices, ai-framework, aiinsoftware, bmadmethod, aidrivendevelopment, customizableai, aiandagile, developmentefficiency

---

## TL;DR.

This post provides an overview of how the BMAD Method works, identifies key markdown files and their purpose, explains how these files can be changed to meet my requirements, and details the impact of making specific changes to these files.

> **Attributions:**
> 
> [***The BMAD GitHub Repository***](https://github.com/bmadcode/BMAD-METHOD) ***↗.***

---

## An Introduction.

Using AI for software development is a constantly evolving process. The BMAD method is yet another approach to keeping AI models focused on their programming tasks:

> The purpose of this post is to introduce the BMAD Method for AI-based software development.

---

## The Big Picture.

The Breakthrough Method of Agile AI-Driven Development (BMAD Method) is a powerful natural language framework designed to enhance software development and other domains through specialized AI agents. This guide provides a synthesized overview of how the BMAD Method works, its key components, and how you can customize it to meet your specific requirements.

---

## Prerequisites.

* A Debian-based Linux distro (I use Ubuntu).
    

---

## Updating my Base System.

* From the (base) terminal, I update my (base) system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

> NOTE: The Ollama LLM manager is already installed on my (base) system.

---

## What is the BMAD Method?

The BMAD Method, or Breakthrough Method for Agile AI-Driven Development, is a framework that integrates AI with agile methodologies to streamline software development. It utilizes specialized AI agents to manage various roles in the development process, enhancing efficiency and organization.

---

## 1\. Overview of the BMAD Method.

The BMAD Method addresses common challenges in AI-assisted development, such as planning inconsistency and context loss, through two core innovations:

### 1.1. Agentic Planning.

In this initial phase, dedicated AI agents like the Analyst, Product Manager (PM), and Architect collaborate to create highly detailed and consistent Product Requirement Documents (PRDs) and Architecture documents. This planning can optionally be performed using web-based agents for cost efficiency, leveraging powerful models and human-in-the-loop refinement to produce comprehensive specifications.

### 1.2. Context-Engineered Development.

Following the planning phase, a Scrum Master (SM) agent takes the detailed plans and transforms them into hyper-detailed development stories. These story files are crucial as they embed the full context, implementation details, and architectural guidance directly within them. The Development (Dev) agent then uses these self-contained story files to implement the actual code, ensuring complete understanding of what, how, and why to build.

This two-phase approach ensures that development proceeds with a clear, consistent vision, minimizing misinterpretations and maximizing efficiency.

---

## 2\. The BMAD Workflow.

The BMAD Method follows a structured workflow, typically starting with planning and moving into a continuous development cycle.

### 2.1. The Planning Workflow (Web UI or Powerful IDE Agents).

The planning phase focuses on defining the project scope, requirements, and technical architecture.

1. **Project Idea & Research:** Starts with a project idea, optionally involving an Analyst for brainstorming, market research, and competitor analysis to create a Project Brief.
    
2. **PRD Creation:** A PM agent creates the PRD (Product Requirement Document) from the Project Brief, detailing Functional Requirements (FRs), Non-Functional Requirements (NFRs), Epics, and Stories.
    
3. **UX Specification (Optional):** If User Experience (UX) is required, a UX Expert agent creates a Front End Specification and can generate UI prompts.
    
4. **Architecture Design:** An Architect agent designs the system architecture based on the PRD and optional UX specifications.
    
5. **Document Alignment:** A Product Owner (PO) agent runs a Master Checklist to ensure all documents (PRD, Architecture, UX Spec) are aligned. If not, the PO updates Epics and Stories, and the PRD/Architecture are revised.
    
6. **Transition to IDE:** Once planning is complete and documents are aligned, the process transitions from web UI (if used) to the IDE. The PO shards the PRD and Architecture documents, preparing them for the development cycle.
    

### 2.2. The Core Development Cycle (IDE).

This phase focuses on implementing the planned features and ensuring quality.

1. **Story Drafting:** The SM agent reviews previous development/QA notes and drafts the next story from the sharded Epic and Architecture documents.
    
2. **Story Review (Optional):** A QA agent can optionally review the story draft against existing artifacts.
    
3. **User Approval:** The user approves the story. If changes are needed, the SM revises the story.
    
4. **Development & Testing:** The Dev agent executes tasks sequentially, implements code and tests, and runs all validations.
    
5. **Ready for Review:** The Dev agent marks the story as "Ready for Review" and adds notes.
    
6. **User Verification & QA Review:** The user verifies the work. They can approve without QA (with a critical reminder to verify all regression tests and linting) or request a QA review.
    
7. **QA Review & Refactoring:** If requested, the QA agent performs a senior developer review, refactors code, adds tests, and documents notes.
    
8. **QA Decision:** QA decides if more Dev work is needed or if the story is approved.
    
9. **Commit Changes:** Crucially, all changes are committed before proceeding.
    
10. **Story Completion:** The story is marked as "Done," and the cycle repeats for the next story.
    

---

## 3\. Key Components and Their Customization.

The BMAD Method's flexibility comes from its natural language-based components, primarily Markdown and YAML files, which define agent behaviors, workflows, and content.

### 3.1. Agent Definition Files (`bmad-core/agents/*.md`)

* **Purpose:** Each Markdown file in `bmad-core/agents/` defines a specific AI agent's persona, role, style, identity, focus, and core principles. They also list the commands the agent can execute and its dependencies (tasks, templates, checklists, data). The `customization` field allows for specific overrides that take precedence over other instructions.
    
* **How to Change:**
    
    * **Refine Persona:** Modify the `persona` sections (role, style, identity, focus) to fine-tune how an agent "thinks" and communicates. For example, making a "Dev" agent's style "extremely concise" will result in shorter, more direct responses.
        
    * **Adjust Core Principles:** Add, remove, or modify bullet points under `core_principles` to instill specific guidelines or values. For instance, adding "Prioritize secure coding practices" to a `dev.md` agent's principles would make it focus more on security during implementation.
        
    * **Update Commands & Dependencies:** Add new commands or modify existing ones, ensuring they map to relevant tasks or templates. Update the `dependencies` section to include or exclude files the agent needs to access.
        
    * **Apply Customization Overrides:** Use the `agent.customization` field for powerful, explicit overrides that ensure specific behaviors or rules are always followed, even if they conflict with other instructions.
        
* **Impact of Changes:** Directly alters the agent's behavior, capabilities, and output. A modified agent will approach tasks differently, potentially leading to changes in the generated code, documentation, or planning artifacts.
    

### 3.2. Checklists (`bmad-core/checklists/*.md`).

* **Purpose:** These Markdown files provide structured lists of criteria or step-by-step procedures that agents (or users) must follow to ensure quality, completeness, or adherence to standards. They often include `[[LLM: INSTRUCTIONS]]` for the agent on how to process the checklist.
    
* **How to Change:**
    
    * **Add/Remove/Modify Items:** Directly edit the markdown list items to add new checks, remove irrelevant ones, or refine existing criteria.
        
    * **Update LLM Instructions:** Modify the `[[LLM: ...]]` blocks to guide the agent on how to interpret and apply the checklist items, or what kind of output to generate (e.g., "Be specific - list each requirement and whether it's complete").
        
* **Impact of Changes:** Directly impacts the quality and completeness of deliverables. A more rigorous `story-dod-checklist.md` will lead to higher quality story implementations. It also influences how agents report on their progress and adherence to standards.
    

### 3.3. Technical Preferences (`bmad-core/data/technical-preferences.md`).

* **Purpose:** This Markdown file allows users to inject their preferred technologies, design patterns, or other technical biases into the planning agents (e.g., PM, Architect).
    
* **How to Change:** Add markdown content describing your preferences. For example, you can specify preferred frontend frameworks, backend languages, database types, or architectural styles.
    
* **Impact of Changes:** Planning agents will consider these preferences when generating PRDs, architecture documents, and making technology recommendations, leading to plans more aligned with your specific technical stack and philosophy.
    

### 3.4. Core Configuration (`bmad-core/core-config.yaml`).

* **Purpose:** This YAML file contains critical configurations for the BMAD Method, such as the `devLoadAlwaysFiles` list.
    
* **How to Change:** Modify the `devLoadAlwaysFiles` list to specify which documents (e.g., coding standards, tech stack, project structure) the Dev agent should always load into its context.
    
* **Impact of Changes:** Crucial for managing the Dev agent's context. By including lean, focused documents here, you ensure the Dev agent has essential guidelines without unnecessary context bloat, leading to more efficient and compliant code generation.
    

### 3.5. Tasks (`bmad-core/tasks/*.md`).

* **Purpose:** These Markdown files define step-by-step procedures that an agent follows to complete a specific piece of work. They are the "how-to" guides for agents.
    
* **How to Change:** Modify the instructions within a task file to alter the steps an agent takes to perform a function. For example, changing `create-doc.md` would change how documents are generally created by agents.
    
* **Impact of Changes:** Directly affects the execution flow and output of specific agent commands.
    

### 3.6. Templates (`bmad-core/templates/*.yaml`).

* **Purpose:** These YAML files define the structured output format for documents generated by agents (e.g., PRD, Architecture, Story). They include metadata, workflow configuration, and sections with instructions for content generation.
    
* **How to Change:** Modify the YAML structure to define new sections, change existing section titles, or update the `instruction` fields that guide the LLM on what content to generate for each section.
    
* **Impact of Changes:** Determines the structure and content of the documents produced by agents, ensuring consistency and adherence to desired formats.
    

---

## 4\. Best Practices for Using and Customizing the BMAD Method.

* **Keep Dev Agents Lean:** Adhere to the principle of minimal context for development agents. Only load essential files (`devLoadAlwaysFiles`) to maximize coding efficiency.
    
* **Leverage Natural Language:** Since everything is Markdown and natural language, focus on clear, concise, and unambiguous instructions in agent definitions, tasks, and templates.
    
* **Use Expansion Packs for Specialization:** For domain-specific needs (e.g., game development, DevOps) or non-technical applications, create or use expansion packs to avoid bloating the core agents.
    
* **Iterative Refinement:** Continuously refine agent definitions, checklists, and preferences based on the quality of the AI-generated output and your evolving project needs.
    
* **Commit Regularly:** Especially during the development cycle, commit your changes frequently to maintain version control and track progress.
    
* **Understand the Workflows:** Familiarize yourself with both the Planning and Development workflows to effectively guide the agents and intervene when necessary.
    

By understanding these core components and their interplay, you can effectively leverage and customize the BMAD Method to streamline your AI-assisted development processes and achieve higher quality outcomes.

---

## The Results.

I have explored the BMAD Method, a revolutionary framework integrating AI with Agile methodologies to enhance software development. I learned about its key components, customization options, and best practices to streamline my AI-assisted development processes for higher quality outcomes.

---

## In Conclusion.

The BMAD Method offers a transformative approach to software development by integrating AI with Agile methodologies. By understanding and customizing its key components, such as agent definitions, checklists, and templates, I can streamline my processes and achieve higher quality outcomes. The method's flexibility and emphasis on natural language make it accessible and adaptable to various project needs, ensuring that AI-assisted development is both efficient and effective. As I continue to explore and implement the BMAD Method, I must remember to iterate and refine my approach to maximize its benefits.

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#BMADMethod #AIDrivenDevelopment #AgileDevelopment #SoftwareDevelopment

#AIIntegration #TechInnovation #DevelopmentWorkflow #AIFramework

#CustomizableAI #SoftwareEngineering #AgileMethodologies #AIInSoftware

#TechBestPractices #AIandAgile #DevelopmentEfficiency