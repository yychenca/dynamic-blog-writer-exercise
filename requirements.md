Project Requirements: Dynamic Micro-Blog Writer
Document Version: 1.1
Date: August 12, 2025
Author: Gemini

1. Introduction
1.1. Project Overview
The Dynamic Micro-Blog Writer is an autonomous multi-agent system designed to generate a high-quality, short-form blog post on a user-specified topic. The system will dynamically generate a writer persona, conduct web research, write a draft, and then iteratively refine the draft based on editorial feedback from a critic agent.

1.2. Project Goal
To create a portfolio-ready capstone project for students who have completed modules on Prompt Engineering, Retrieval-Augmented Generation (RAG), and AI Agents. The project will demonstrate the student's ability to integrate these concepts into a cohesive, functional application that mimics a real-world content creation workflow.

1.3. Target User
The primary user of this system is the student developer. The student will provide the initial inputs and run the system, which will then operate autonomously to produce the final output.

2. System Architecture & Workflow
2.1. High-Level Workflow
The system operates as a sequential pipeline with an internal review loop.

Initialization: The user provides an initial Topic and a Style & Background guide.

Persona Generation: The Persona Architect agent creates a writer persona and a set of search queries.

Research: The Research Analyst agent executes the search queries to gather relevant information.

Drafting: The Content Synthesizer agent writes the first draft based on the persona and research.

Review Loop (Iterative Refinement):
a. The Critic/Editor agent reviews the draft against a set of quality principles.
b. If the draft is approved, the loop terminates.
c. If the draft is not approved, the Critic/Editor provides feedback. The Content Synthesizer receives this feedback and writes a revised draft.
d. This loop can run for a maximum of three cycles.

Finalization: The system outputs the final approved (or last revised) version of the blog post.

2.2. Architectural Diagram
This diagram illustrates the flow of information and control between the different agents in the system. The central "Review Loop" is the core of the iterative refinement process.

graph TD
    subgraph "Phase 1: Setup"
        A[User Input: Topic & Style] --> B(Persona Architect);
        B -->|Generates Persona & Queries| C(Research Analyst);
    end

    subgraph "Phase 2: Content Generation & Review"
        C -->|Provides Research Content| D(Content Synthesizer);
        D -->|Writes/Revises Draft| E(Critic / Editor);
        E --o|Provides Feedback| D;
        E -->|Approves Final Draft| F[Final Output];
    end

    linkStyle 3 stroke-width:2px,fill:none,stroke:red,stroke-dasharray: 3 3;
    linkStyle 4 stroke-width:2px,fill:none,stroke:green;

    note right of E
      Iterative Review Loop
      (Max 3 Cycles)
    end note

3. Core Components & Functional Requirements
3.1. Fundamental Principles of Quality Writing
A set of non-negotiable principles must be defined and used as a core reference by both the Content Synthesizer and the Critic/Editor agents.

P1: Evidentiary Support: All claims must be directly traceable to the provided research material.

P2: Clarity and Conciseness: Writing must be precise, unambiguous, and free of unnecessary jargon.

P3: Engaging Narrative: The post must feature a strong hook, a logical flow, and a memorable conclusion.

P4: Structural Integrity: The output must be well-organized with a clear title, introduction, body, and conclusion.

P5: Intellectual Honesty: Information must be represented accurately, even when adopting a specific persona.

3.2. Agent: Persona Architect
FR-1.1: Must accept a topic (string) and style_and_background (string) as inputs.

FR-1.2: Must generate a detailed, topic-specific writer persona suitable for a mainstream publication.

FR-1.3: Must generate a list of at least three optimized web search queries relevant to the topic.

FR-1.4: Must output a single, valid JSON object containing persona_prompt (string) and search_queries (list of strings).

3.3. Agent: Research Analyst
FR-2.1: Must accept a list of search queries as input.

FR-2.2: Must execute each search query using a web search tool.

FR-2.3: Must consolidate the findings into a single block of text. For this project, this step will be simulated by an LLM to ensure consistency and manage costs.

FR-2.4: The output text must be clearly delineated (e.g., with --- RESEARCH START --- and --- RESEARCH END --- markers).

3.4. Agent: Content Synthesizer
FR-3.1: Must accept the persona_prompt, researched_content, the original topic, and optional editorial_feedback as inputs.

FR-3.2: Must generate a blog post of approximately 500 words.

FR-3.3: Must adhere to the persona and the Fundamental Principles of Quality Writing.

FR-3.4: When provided with editorial_feedback, the agent must revise the previous draft to specifically address the editor's comments.

3.5. Agent: Critic/Editor
FR-4.1: Must accept the draft_blog, research_content, and the Fundamental Principles as inputs.

FR-4.2: Must evaluate the draft for adherence to the principles and for factual consistency with the research material.

FR-4.3: Must output a single, valid JSON object containing is_approved (boolean) and comments (string).

FR-4.á4: The comments must be clear, constructive, and actionable for the Content Synthesizer. If is_approved is true, the comments can be a simple affirmation.

4. Technical & Non-Functional Requirements
NFR-1 (Environment): The entire system must be implemented within a single Python notebook (Jupyter or Google Colab).

NFR-2 (Language & Libraries): The project will use Python 3. The primary LLM interaction will be via the google-generativeai library.

NFR-3 (LLM): The system will use a gemini-1.5-flash model or a similar capable model.

NFR-4 (Cost-Effectiveness): The Research Analyst agent's web search functionality will be simulated by an LLM call to avoid the complexity and potential costs of live search APIs.

NFR-5 (File Management):

The system must create a unique output folder for each run, named using the convention YYYYMMDD_topic_abbreviation.

Each draft blog must be saved as a separate Markdown file (e.g., draft_1.md, draft_2.md).

Each set of editorial comments must be saved as a separate Markdown file (e.g., review_1.md, review_2.md).

The final version of the blog must be saved as final_blog.md.

NFR-6 (Error Handling): The system should gracefully handle potential errors during LLM calls or JSON parsing and print informative status messages to the console.

5. Acceptance Criteria
The project will be considered complete and successful when the following criteria are met:

AC-1: The user can successfully run the entire workflow by providing only a topic and style guide in the notebook.

AC-2: All four agents execute their functions as defined in Section 3.

AC-3: The system correctly performs the iterative review loop, generating and saving drafts and reviews for each cycle.

AC-4: The system terminates correctly after either editor approval or three review cycles.

AC-5: All output files are correctly generated and saved to a uniquely named folder as per NFR-5.

AC-6: The final generated blog post is coherent, stylistically appropriate, and factually consistent with the simulated research.