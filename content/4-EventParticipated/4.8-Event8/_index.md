---
title: "Event 8"
date: 2025-09-09
weight: 1
chapter: false
pre: " <b> 4.8. </b> "
---

# Event Report: Building Agentic AI & Context Optimization with Amazon Bedrock

### Event Objectives
-   **Explore Agentic AI Architecture**: Provide a comprehensive view of the AI Agent trend, shifting from passive Large Language Models (LLMs) to active AI systems capable of executing tasks.
-   **Master Amazon Bedrock Agents**: Gain deep understanding of this core AWS service to build and deploy secure Agents capable of connecting to data sources and performing actions.
-   **Advanced Orchestration Techniques**: Learn in-depth techniques (Level 300) regarding multi-agent orchestration and Context Optimization to solve complex problems.
-   **Hands-on Implementation**: Experience the real-world process of building an Agentic Workflow from concept to deployment through the CloudThinker Hack session.

### Speaker List
-   Nguyen Gia Hung - Head of Solutions Architect (AWS)
-   Kien Nguyen - Solutions Architect (AWS)
-   Viet Pham - Founder & CEO
-   Thang Ton - Co-Founder & COO (CloudThinker)
-   Henry Bui - Head of Engineering (CloudThinker)
-   Kha Van - Community Leader

### Key Content & Highlights

#### Technology Foundation: AWS Bedrock Agent Core
-   **Focus**: This session laid the technical groundwork, explaining how Amazon Bedrock Agent functions as a bridge between LLMs, data sources (Knowledge Bases), and actions (Action Groups).
-   **Content**:
    -   How Bedrock Agent analyzes user requests, plans the execution (Chain of Thought), and calls the necessary APIs to execute tasks.
    -   The distinction between standard RAG (Retrieval-Augmented Generation) and an Agentic Workflow (RAG + Action).
-   **Key Highlight**: Bedrock's ability to manage memory and conversational context without building complex infrastructure, significantly simplifying the agent development process.

#### Real-world Application: Building Agentic Workflows
-   **Focus**: Moving from theory to practice with specific Use Cases.
-   **Content**:
    -   The thought process for designing an Agent workflow: Define Goal -> Define Tools -> Design Logic Flow.
    -   Demo of how an Agent solves a specific business problem (e.g., automating Customer Service processes or order processing) rather than just answering questions.
-   **Key Highlight**: Clear proof that modern AI is not just for "chatting" but for "working" (Doers, not just Talkers).

#### Technical Deep Dive: Orchestration & Context Optimization (L300)
-   **Focus**: This was the deepest technical section (Level 300) presented by the CloudThinker Engineering team, focusing on resolving the limitations of single agents.
-   **Content**:
    -   **Multi-Agent Orchestration**: How to orchestrate an "army" of Agents, where each Agent specializes in a task (e.g., 1 Retrieval Agent, 1 Calculation Agent, 1 Summarization Agent) to handle complex requests.
    -   **Context Optimization**: Techniques to keep the conversation context clean, accurate, and prevent "drift" (hallucination) during long conversations or handovers between Agents.
-   **Key Highlight**: The mindset regarding "CloudThinker Agentic Orchestration" opens a path for building sustainable, high-accuracy enterprise-grade AI systems.

#### Hands-on: CloudThinker Hack
-   **Focus**: A practical workshop session for attendees to build a product themselves.
-   **Content**: Step-by-step guidance on initializing the environment, configuring Bedrock Agents, writing Lambda functions for Action Groups, and integrating them into an application.
-   **Result**: Attendees could see a functioning Agent operating right in the classroom.

### Key Takeaways

#### On Agentic AI Architecture
-   **Mindset Shift**: You understood that Agentic AI is not just about writing prompts for ChatGPT. It requires system architecture thinking: knowing when the AI needs to use which tool and how to control its output.
-   **The Power of Orchestration**: You learned that for complex tasks, a "know-it-all" Agent is less effective than a system of multiple specialized Agents orchestrated seamlessly.

#### On Tools & Skills
-   **Amazon Bedrock Mastery**: Mastered the configuration of Agents, Knowledge Bases, and Action Groups on the AWS console.
-   **Context Optimization**: Learned strategies to manage the context window efficiently, helping to save token costs and increase answer accuracy.

#### On Applicability
-   **Design Patterns**: Grasped common design patterns when building AI applications for enterprises, ranging from internal data retrieval to action execution on ERP/CRM systems.

### Event Experience
The event "A Comprehensive Journey through Agentic AI" was a complete journey, moving from the big picture (High-level architecture) down to every line of code (Hands-on implementation). The combination of AWS's robust infrastructure foundation and CloudThinker's deep practical deployment experience provided immense value. In particular, the Level 300 session on Orchestration answered many questions about how to make AI work stably in a Production environment, rather than just serving as experimental demos.