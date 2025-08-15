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
1. **Open the notebook**: Upload `agent_capstone_exercises.ipynb` to Google Colab or open directly
2. **Add API Key Secret**:
   - Click the 🔑 key icon in the left sidebar
   - Add new secret: `GEMINI_API_KEY` 
   - Paste your API key from https://ai.google.dev/
   - **Important**: Enable "Notebook access" for this secret
3. **Run Setup**: Execute all setup cells in order (they'll install packages automatically)
4. **Start Exercises**: Begin with Exercise 1

#### Option 2: Local Development (VS Code, Cursor, PyCharm, etc.)

**Step 1: Project Setup**
```bash
# Clone or download the project files
# Navigate to the project directory
cd path/to/BlogWriterExercise
```

**Step 2: Install Dependencies**
```bash
# Install all required packages
pip install -r requirements.txt

# Alternative: Install packages individually
pip install google-generativeai beautifulsoup4 requests jupyter ipykernel
```

**Step 3: Set Up API Key (Choose one method)**

**Method A: Environment Variable (Recommended)**
```bash
# Linux/Mac
export GEMINI_API_KEY=your_actual_api_key_here

# Windows (Command Prompt)
set GEMINI_API_KEY=your_actual_api_key_here

# Windows (PowerShell)
$env:GEMINI_API_KEY="your_actual_api_key_here"
```

**Method B: VS Code Settings**
```json
// In your workspace settings.json
{
    "terminal.integrated.env.linux": {
        "GEMINI_API_KEY": "your_actual_api_key_here"
    },
    "terminal.integrated.env.windows": {
        "GEMINI_API_KEY": "your_actual_api_key_here"
    },
    "terminal.integrated.env.osx": {
        "GEMINI_API_KEY": "your_actual_api_key_here"
    }
}
```

**Method C: .env file (Optional)**
```bash
# Create .env file in project root
echo "GEMINI_API_KEY=your_actual_api_key_here" > .env
```

**Step 4: Launch Jupyter**
```bash
# Start Jupyter Notebook
jupyter notebook agent_capstone_exercises.ipynb

# Or use Jupyter Lab
jupyter lab agent_capstone_exercises.ipynb
```

**Step 5: Verify Setup**
- Run the first few cells to verify everything works
- The configuration cell will prompt for API key if not found in environment

### Troubleshooting Common Issues

#### API Key Problems
- **Issue**: `GEMINI_API_KEY not found`
- **Solution**: Double-check you've set the environment variable or Colab secret correctly
- **Test**: In a Python cell, run `import os; print(os.environ.get('GEMINI_API_KEY'))` (should not show None)

#### Package Installation Issues
```bash
# If packages fail to install
pip install --upgrade pip
pip install --force-reinstall -r requirements.txt

# For specific import errors
pip install --upgrade google-generativeai
```

#### Jupyter Notebook Issues
```bash
# If kernel doesn't start
jupyter kernelspec list
python -m ipykernel install --user --name=python3

# Restart Jupyter after installing packages
```

#### VS Code Jupyter Issues
- Install the Jupyter extension for VS Code
- Select the correct Python interpreter (Ctrl+Shift+P → "Python: Select Interpreter")
- Restart VS Code after installing packages

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