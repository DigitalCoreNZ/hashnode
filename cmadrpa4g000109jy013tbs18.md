---
title: "CrewAI: Generating a Report."
seoTitle: "CrewAI Report Generation Guide"
seoDescription: "Learn to deploy and use CrewAI agents effectively with a step-by-step guide inspired by Tyler Reed's tutorial. Enhance your understanding of AI agents."
datePublished: Wed May 07 2025 10:00:22 GMT+0000 (Coordinated Universal Time)
cuid: cmadrpa4g000109jy013tbs18
slug: crewai-generating-a-report
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1746576039843/07af5bd8-d217-4724-b0f4-5019a236f5b5.png
tags: ai, ubuntu, vs-code, ai-community, open-source, ai-tools, tech-blog, ai-integration, ai-projects, tech-tutorial, crewai, ai-research, learning-by-doing, practical-ai

---

## TL;DR.

The post provides a step-by-step guide on deploying and utilising CrewAI agents by following a part of Tyler Reed's YouTube tutorial. This article emphasises learning by doing, documenting the process, and sharing my insights. I highlight the importance of experimenting and creating posts that enhance my understanding of CrewAI's functionalities.

> **Attributions:**
> 
> [https://www.youtube.com/watch?v=ONKOXwucLvE](https://www.youtube.com/watch?v=ONKOXwucLvE&list=PLZSsCXMJ6wBI4yU5YvxuGZXfeTP8CoHo5&index=1&t=931s&pp=gAQBiAQB) ***from*** [***Tyler AI***](https://www.youtube.com/@TylerReedAI) ***↗.***

---

## An Introduction.

Although I will be deploying CrewAI agents, my main objective is to show the results of converting hands-on processes into documentation:

> The purpose of this post is to show how practical experiences are captured as documented events.

---

## The Big Picture.

This is the first project (in a series of projects) where I cover part of a YouTube video from Tyler Reed.

![](https://yt3.ggpht.com/tzaY1P_SQIJ6edyXBAtouVgG_4ydxgCYalMsba6ZIXPR9PTZ5xtFBy858mT6jcZYWDzjcNmfPcM=s88-c-k-c0x00ffffff-no-rj align="left")

[Tyler AI](https://www.youtube.com/@TylerReedAI)

If you are new to CrewAI (like me), then I **STRONGLY** suggest you do *EXACTLY* what I did: Follow Tyler’s instructions, make detailed notes about his process, turn your notes into a blog post, and publish your results. You will learn by doing *and* you will end up with a post that you can reference. Copying and pasting my post is *not* a learning process. You will ultimately cheat yourself, and fail to understand how CrewAI works.

Here is a link to Tyler’s video:

[https://www.youtube.com/watch?v=ONKOXwucLvE&t=0](https://www.youtube.com/watch?v=ONKOXwucLvE&t=0) ***↗.***

---

## Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [CrewAI](https://solodev.app/local-ai-toolkit-for-developers#heading-what-is-crewai).
    

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

## What is the Report Project?

The Report Project shows how to deploy existing tools for CrewAI agents to use. A list of existing tools can be found within the [CrewAI documentation](https://docs.crewai.com/tools/) ***↗***.

---

### Creating the Report Project.

* From the terminal, I navigate to my projects directory:
    

```bash
cd ~/AI
```

* I start a new project:
    

```bash
crewai create crew report
```

* From the first list of options, I choose the ollama option.
    
* From the next list of options, I choose the ollama/llama3.1 option.
    

### Opening the Report Project in VS Code.

* I open the Report Project in VS Code:
    

```bash
code ./report
```

### Editing the `.env` File.

* I open the `.env` file and replace the contents with the following:
    

```nix
OPENAI_API_BASE=https://openrouter.ai/api/v1 # openrouter url here
OPENAI_MODEL_NAME=openrouter/google/gemini-2.0-flash-001 # openrouter/path/model_name here
OPENROUTER_API_KEY=your_api_key # API key here
```

> NOTE: By default, these settings provide this project with access to the OpenRouter.ai API.

### Editing the `main.py` File.

* Under the `src/report` directory, I open the `main.py` file.
    
* I replace the contents of the `main.py` file with the following:
    

```python
#!/usr/bin/env python
import sys
import warnings

from datetime import datetime

from crew import Report

warnings.filterwarnings("ignore", category=SyntaxWarning, module="pysbd")

# This main file is intended to be a way for you to run your
# crew locally, so refrain from adding unnecessary logic into this file.
# Replace with inputs you want to test with, it will automatically
# interpolate any tasks and agents information

def run():
    """
    Run the crew.
    """
    inputs = {
        'topic': 'AI LLMs',
        'current_year': str(datetime.now().year)
    }
    
    try:
        Report().crew().kickoff(inputs=inputs)
    except Exception as e:
        raise Exception(f"An error occurred while running the crew: {e}")

run()
```

**What changed:**

* Near the top, I changed `from report.crew import Report` to `from crew import Report`,
    
* I deleted the `train()`, `replay()`, and `test()` functions, and
    
* At the bottom of the file, I added the `run()` function.
    

### Editing the `crew.py` File.

* Under the `src/report` directory, I open the `crew.py` file.
    
* I replace the contents of the `crew.py` file with the following:
    

```python
from crewai import Agent, Crew, Process, Task, LLM
from crewai.project import CrewBase, agent, crew, task
from dotenv import load_dotenv

load_dotenv()

# If you want to run a snippet of code before or after the crew starts,
# you can use the @before_kickoff and @after_kickoff decorators
# https://docs.crewai.com/concepts/crews#example-crew-class-with-decorators

@CrewBase
class Report():
    """Report crew"""

    # Learn more about YAML configuration files here:
    # Agents: https://docs.crewai.com/concepts/agents#yaml-configuration-recommended
    # Tasks: https://docs.crewai.com/concepts/tasks#yaml-configuration-recommended
    agents_config = 'config/agents.yaml'
    tasks_config = 'config/tasks.yaml'

    ollama_llm = LLM(
        model = 'ollama/deepseek-r1:14b',
        base_url = 'http://localhost:11434'
    )

    # If you would like to add tools to your agents, you can learn more about it here:
    # https://docs.crewai.com/concepts/agents#agent-tools
    @agent
    def researcher(self) -> Agent:
        return Agent(
            config=self.agents_config['researcher'],
            verbose=True,
            llm = self.ollama_llm
        )

    @agent
    def reporting_analyst(self) -> Agent:
        return Agent(
            config=self.agents_config['reporting_analyst'],
            verbose=True,
            llm = self.ollama_llm
        )

    # To learn more about structured task outputs,
    # task dependencies, and task callbacks, check out the documentation:
    # https://docs.crewai.com/concepts/tasks#overview-of-a-task
    @task
    def research_task(self) -> Task:
        return Task(
            config=self.tasks_config['research_task'],
        )

    @task
    def reporting_task(self) -> Task:
        return Task(
            config=self.tasks_config['reporting_task'],
            output_file='report.md'
        )

    @crew
    def crew(self) -> Crew:
        """Creates the Report crew"""
        # To learn how to add knowledge sources to your crew, check out the documentation:
        # https://docs.crewai.com/concepts/knowledge#what-is-knowledge

        return Crew(
            agents=self.agents, # Automatically created by the @agent decorator
            tasks=self.tasks, # Automatically created by the @task decorator
            process=Process.sequential,
            verbose=True,
            # process=Process.hierarchical, # In case you wanna use that instead https://docs.crewai.com/how-to/Hierarchical/
        )
```

**What changed:**

* At the top of the page and the end of the line `from crewai import Agent, Crew, Process, Task` I added `LLM`,
    
* Near the top, I added `from dotenv import load_dotenv` and `load_dotenv()`, and
    
* Within the Report() class, after `tasks_config = 'config/tasks.yaml'` I added the following:
    
    ```python
    ollama_llm = LLM(
            model = 'ollama/deepseek-r1:14b',
            base_url = 'http://localhost:11434'
        )
    ```
    
* Within the `researcher()` and `reporting_analyst()` agents, I added `llm = self.ollama_llm` to override the OpenRouter.ai settings in the `.env` file.
    

### Editing the `agents.yaml` File.

* Under the `src/report/config` directory, I open the `agents.yaml` file.
    
* I replace the contents of the `agents.yaml` file with the following:
    

```python
researcher:
  role: >
    {topic} Senior Data Researcher
  goal: >
    Uncover cutting-edge developments in {topic}
  backstory: >
    You are a seasoned researcher with a knack for uncovering the latest
    developments in {topic}. Known for your ability to find the most relevant
    information and present it in a clear and concise manner.

reporting_analyst:
  role: >
    {topic} Reporting Analyst
  goal: >
    Create detailed reports based on {topic} data analysis and research findings
  backstory: >
    You are a meticulous analyst with a keen eye for detail. You are known for
    your ability to turn complex data into clear and concise reports, making
    it easy for others to understand and act on the information you provide.
```

**What changed:**

* No changes made.
    

### Editing the `tasks.yaml` File.

* Under the `src/report/config` directory, I open the `tasks.py` file.
    
* I replace the contents of the `tasks.py` file with the following:
    

```python
research_task:
  description: >
    Conduct a thorough research about {topic}
    Make sure you find any interesting and relevant information given
    the current year is {current_year}.
  expected_output: >
    A list with 10 bullet points of the most relevant information about {topic}
  agent: researcher

reporting_task:
  description: >
    Review the context you got and expand each topic into a full section for a report.
    Make sure the report is detailed and contains any and all relevant information.
  expected_output: >
    A fully fledged report with the main topics, each with a full section of information.
    Formatted as markdown without '```'
  agent: reporting_analyst
```

**What changed:**

* No changes made.
    

---

## The Results.

This CrewAI project provides a comprehensive guide to deploying and utilising CrewAI agents effectively. By watching Tyler Reed's video, following his instructions, and documenting the process, I gained a deeper understanding of CrewAI's functionalities. This hands-on approach not only enhanced my learning but also resulted in a valuable reference post. As I embark on this journey, I must experiment, document my findings, and share my insights with the community.

---

## In Conclusion.

I discovered how to deploy, and utilise, CrewAI agents. I followed along with (some of) Tyler Reed's video tutorial, learned by doing, and enhanced my understanding of CrewAI's functionalities. This process is perfect for me as I look to document my journey while sharing my insights.

Until next time: Be safe, be kind, be awesome.

---

## Hash Tags.

#CrewAI #AI #AI-Projects #AI-Tools #AI-Research #AI-Community

#AI-Integration #Tech-Tutorial #Tech-Blog #Open-Source

#VS-Code #Ubuntu #Learning-By-Doing #Practical-AI