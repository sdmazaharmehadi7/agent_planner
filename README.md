# agent_planner
Characteristic,Description Generative,Creates a novel plan from scratch based on the input. Hierarchical,"Plans can often be structured into layers (e.g., a high-level plan and detailed sub-plans for each step)." Dynamic,It can modify the plan mid-execution based on real-time feedback or new information. Efficient,It aims to create the shortes
## Project Overview - Agent planner

NOTE: This is a **capstone project submssion** for the [Kaggle Agents Intensive Capstone project](https://www.kaggle.com/competitions/agents-intensive-course-capstone-2025/) 

This project contains the core logic for Agent planner, a multi-agent system designed to assist users in creating various types of day_plan posts. The agent is built using Google Agent Development Kit (ADK) and follows a modular architecture.


### Problem Statement

Writing day_plans manually is laborious because it requires significant time investment in research, drafting, editing, and formatting each piece of content from scratch. The repetitive nature of structuring posts and maintaining consistent tone across multiple articles can quickly become mentally exhausting and drain creative energy. Manual blog writing also struggles to scale when content demands increase, forcing writers to choose between quality and quantity or invest in hiring additional staff. Automation can streamline research gathering, generate initial drafts, handle formatting consistency, and maintain publishing schedules, allowing human writers to focus their expertise on strategic direction, creative refinement, and adding unique insights that truly require human judgment.

### Solution Statement

Agents can automatically research topics by gathering information from multiple sources, synthesizing key insights, and identifying trending themes relevant to your target audience. They can generate initial draft outlines or full articles based on specific parameters like tone, length, significantly reducing the time spent on the blank page problem. Additionally, agents can manage the entire publishing workflow by scheduling posts, distributing content across multiple platforms, monitoring performance metrics, and even suggesting improvements based on engagement data—transforming plan management from a manual chore into a streamlined, data-driven process.

### Architecture
Core to Agent planner is the `planner_agent` -- a prime example of a multi-agent system. It's not a monolithic application but an ecosystem of specialized agents, each contributing to a different stage of the day_plan creation process. This modular approach, facilitated by Google's Agent Development Kit, allows for a sophisticated and robust workflow. The central orchestrator of this system is the `interactive_blogger_agent`.

The `planner_agent` is constructed using the `Agent` class from the Google ADK. Its definition highlights several key parameters: the `name`, the `model` it uses for its reasoning capabilities, and a detailed `description` and `instruction` set that governs its behavior. Crucially, it also defines the `sub_agents` it can delegate tasks to and the `tools` it has at its disposal.

The real power of the `planner_agent` lies in its team of specialized sub-agents, each an expert in its domain.

**Content Strategist: `robust_planner`**

This agent is responsible for creating a well-structured and comprehensive outline for the post. If a codebase is provided, it will intelligently incorporate sections for code snippets and technical deep dives. To ensure high-quality output, it's implemented as a `LoopAgent`, a pattern that allows for retries and validation. The `OutlineValidationChecker` ensures that the generated outline meets predefined quality standards.

**Technical Writer: `robust_writer`**

Once the outline is approved, the `robust_blog_writer` takes over. This agent is an expert technical writer, capable of crafting in-depth and engaging articles for a sophisticated audience. It uses the approved outline and codebase summary to generate the blog post, with a strong emphasis on detailed explanations and illustrative code snippets. Like the planner, it's a `LoopAgent` that uses a `BlogPostValidationChecker` to ensure the quality of the written content.

**Editor: `plan_editor`**

The `plaan_editor` is a professional technical editor that revises the blog post based on user feedback. This allows for an iterative and collaborative writing process, ensuring the final article meets the user's expectations.
