# AI Agents Capstone Project: Student Instructions

## 🎯 Project Overview

Welcome to your **AI Agents Capstone Project**! You'll be building a sophisticated multi-agent system that creates blog posts automatically. This project demonstrates everything you've learned about AI agents, the ReAct framework, and agentic workflows.

### What You're Building

A **Dynamic Blog Writer** system with 5 specialized agents:
1. **🎭 Persona Architect** - Creates writer personas and search strategies
2. **🔍 Research Analyst** - Conducts web research and gathers information  
3. **✍️ Content Synthesizer** - Writes blog posts based on persona and research
4. **🔍 Critic** - Evaluates drafts against quality principles
5. **✏️ Editor** - Manages iterative improvement workflow

This implements the **Evaluator-Optimizer** pattern you learned about in [Session 3](session_course_notes.html)!

---

## 🚀 Getting Started

### Prerequisites
- Completed Session 1 (Prompt Engineering)
- Completed Session 2 (RAG)
- Completed Session 3 (AI Agents)
- Basic Python knowledge
- Gemini API key (free from https://ai.google.dev/)

### Setup Instructions

#### Option 1: Google Colab (Recommended)
1. Open `agent_capstone_exercises.ipynb` in Google Colab
2. Click the 🔑 key icon in the left sidebar
3. Add secret: `GEMINI_API_KEY` with your API key
4. Enable notebook access for the secret
5. Run all setup cells

#### Option 2: Local Jupyter
1. Install required packages: `pip install google-generativeai beautifulsoup4 requests`
2. Set environment variable: `export GEMINI_API_KEY=your_key_here`
3. Open `agent_capstone_exercises.ipynb` in Jupyter
4. Run all setup cells

---

## 📚 Learning Objectives

By completing this project, you will:

### Technical Skills
- ✅ Implement multi-agent systems with specialized roles
- ✅ Apply the ReAct framework (Thought → Action → Observation)
- ✅ Build iterative improvement workflows (Evaluator-Optimizer pattern)
- ✅ Integrate external tools (web search) with LLMs
- ✅ Handle structured data and JSON communication between agents
- ✅ Implement quality control and evaluation systems

### Course Concept Application
- ✅ **Session 1 Skills**: Advanced prompt engineering for specialized agents
- ✅ **Session 2 Skills**: Research integration and knowledge synthesis
- ✅ **Session 3 Skills**: Complete agent system with tools and workflows

---

## 🎯 Exercise Structure

### Exercise 1: Persona Architect (30 minutes)
**Goal**: Create an agent that generates writer personas and search queries

**What You'll Learn**:
- How to design specialized agent personalities
- JSON output formatting for agent communication
- Strategic search query generation

**Key Implementation**: Complete the `generate_persona_and_queries` method

### Exercise 2: Research Analyst (45 minutes)
**Goal**: Build an agent that conducts real web research

**What You'll Learn**:
- Integrating external tools (web search) with LLMs
- Data synthesis and consolidation techniques
- Handling API responses and error cases

**Key Implementation**: Complete the `conduct_research` method

### Exercise 3: Content Synthesizer (45 minutes)
**Goal**: Create an agent that writes high-quality blog posts

**What You'll Learn**:
- Multi-input content generation (persona + research)
- Quality principle adherence
- Iterative content improvement

**Key Implementation**: Complete the `write_blog_post` method

### Exercise 4: Critic Agent (30 minutes)
**Goal**: Build an agent that evaluates content quality

**What You'll Learn**:
- Systematic quality evaluation
- Structured feedback generation
- Quality principle assessment (P1-P5)

**Key Implementation**: Complete the `evaluate_draft` method

### Exercise 5: Editor & Orchestration (60 minutes)
**Goal**: Orchestrate all agents in a complete workflow

**What You'll Learn**:
- Multi-agent workflow coordination
- Iterative improvement loops
- Decision-making logic for agent systems

**Key Implementation**: Complete the `EditorAgent` and `BlogWorkflowOrchestrator` classes

---

## 🛠️ Implementation Guide

### Code Structure

Each exercise follows this pattern:
1. **Class Definition**: Pre-built class with method signatures
2. **TODO Sections**: Clearly marked areas for your implementation
3. **Hints**: Guidance on what to implement
4. **Test Assertions**: Automatic validation of your work

### Working with TODOs

Look for these patterns in the code:
```python
# TODO: Write your prompt here
# HINT: Include these specific elements...
prompt = f"""
# Your implementation goes here
"""

# TODO: Make the API call
response = None  # Replace with actual call
```

### Getting Help

1. **Read the Hints**: Each TODO has specific hints about what to implement
2. **Review Course Notes**: Refer back to `session_course_notes.html`
3. **Check Assertions**: Error messages will guide you to what's missing
4. **Study Examples**: The notebook includes example data and expected formats

---

## ✅ Validation and Testing

### Exercise Completion Checks

Each exercise has built-in assertions that will:
- ✅ Verify your implementation works
- ✅ Check output formats and types
- ✅ Validate integration with other components
- ❌ Show specific error messages if incomplete

### Success Indicators

You'll know you're succeeding when you see:
- `✅ Exercise X completed successfully!`
- No assertion errors when running cells
- Realistic output from your agents

### Final Integration Test

Once all exercises are complete, run the final integration test to see your complete multi-agent system in action!

---

## 🎓 Assessment Criteria

Your project will be evaluated on:

### Functionality (60%)
- [ ] All 5 agents implemented correctly
- [ ] Proper JSON communication between agents
- [ ] Successful workflow execution
- [ ] Error handling and edge cases

### Code Quality (25%)
- [ ] Clean, readable implementations
- [ ] Proper use of provided data structures
- [ ] Following TODO instructions precisely
- [ ] Appropriate use of hints and guidance

### Understanding (15%)
- [ ] Demonstrates grasp of ReAct framework
- [ ] Shows understanding of agent roles and responsibilities
- [ ] Applies course concepts correctly
- [ ] Implements iterative improvement pattern

---

## 🚨 Common Issues and Solutions

### API Key Problems
**Issue**: `GEMINI_API_KEY not found`
**Solution**: Make sure you've added the API key to Colab secrets or environment variables

### JSON Parsing Errors
**Issue**: `JSONDecodeError when parsing response`
**Solution**: Clean the response text by removing ```json``` markers before parsing

### Import Errors
**Issue**: `ModuleNotFoundError`
**Solution**: Run the package installation cell at the top of the notebook

### Empty Search Results
**Issue**: Web search returns no results
**Solution**: This is normal sometimes - your code should handle empty results gracefully

### Agent Communication Issues
**Issue**: Agents can't communicate with each other
**Solution**: Make sure you're returning the correct data types (PersonaResult, ResearchResult, etc.)

---

## 💡 Tips for Success

### Start Simple
- Implement basic functionality first
- Add error handling after core logic works
- Test each exercise before moving to the next

### Use the Course Concepts
- Think about **Thought → Action → Observation** for each agent
- Remember the **Evaluator-Optimizer** pattern for the review loop
- Apply **prompt engineering** techniques from Session 1

### Debug Effectively
- Print intermediate results to understand what's happening
- Check the assertions carefully - they tell you exactly what's expected
- Use the sample data provided to test your implementations

### Be Patient with API Calls
- Gemini API calls can take a few seconds
- Web searches may occasionally fail - this is normal
- Don't worry if you need multiple attempts to get it right

---

## 🏆 What Success Looks Like

When you complete this project, you'll have:

1. **A Working Multi-Agent System**: 5 agents that communicate and collaborate
2. **Real Blog Generation**: Your system will create actual blog posts on any topic
3. **Quality Control**: Built-in evaluation and improvement mechanisms
4. **Practical Experience**: Hands-on implementation of everything from the course

### Example Output
Your completed system will generate:
- 📁 A timestamped project folder
- 📝 Draft blog posts (multiple versions)
- 📋 Quality reviews and feedback
- 📄 A polished final blog post
- 🔍 Research documentation with real web sources

---

## 🎉 Next Steps After Completion

Once you finish this capstone:

1. **Experiment**: Try different topics and style requirements
2. **Extend**: Add new agents or tools to the system
3. **Share**: Show your working multi-agent system to others
4. **Apply**: Use these patterns in your own AI projects

Remember: You're not just completing an assignment - you're building a real AI system that demonstrates cutting-edge agent technology!

---

**Good luck with your capstone project! You've got this! 🚀**

---

*For technical support or questions, refer to your TA instructions or course materials.*