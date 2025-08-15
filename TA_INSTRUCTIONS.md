# AI Agents Capstone Project: TA Instructions & Solution Guide

## 📋 Overview for Teaching Assistants

This guide provides comprehensive instructions for supporting students through the AI Agents Capstone Project. The project is designed as 5 progressive exercises that build a complete multi-agent system for automated blog generation.

### Project Structure
- **Notebook**: `agent_capstone_exercises.ipynb` - Main student workspace
- **Student Guide**: `STUDENT_INSTRUCTIONS.md` - Complete student documentation
- **TA Guide**: This document - Solutions and support guidance
- **Reference**: `session_course_notes.html` - Course concept review

---

## 🎯 Learning Assessment Framework

### Course Concept Mapping
| Exercise | Course Session | Key Concepts Applied |
|----------|----------------|---------------------|
| Exercise 1 | Session 1 & 3 | Prompt engineering, JSON output, agent personas |
| Exercise 2 | Session 2 & 3 | RAG concepts, web search integration, data synthesis |
| Exercise 3 | Session 1 & 3 | Advanced prompting, multi-input generation, quality adherence |
| Exercise 4 | Session 3 | Evaluation agents, structured feedback, quality assessment |
| Exercise 5 | Session 3 | ReAct framework, Evaluator-Optimizer pattern, workflow orchestration |

### Expected Completion Times
- **Exercise 1**: 30 minutes (Persona Architect)
- **Exercise 2**: 45 minutes (Research Analyst)
- **Exercise 3**: 45 minutes (Content Synthesizer)
- **Exercise 4**: 30 minutes (Critic Agent)
- **Exercise 5**: 60 minutes (Editor & Orchestration)
- **Total**: ~3.5 hours

---

## 💡 Exercise-by-Exercise Support Guide

### Exercise 1: Persona Architect

**What Students Need to Implement**:
```python
def generate_persona_and_queries(self, topic: str, style_and_background: str) -> PersonaResult:
```

**Key Implementation Points**:
1. Create a comprehensive prompt that requests both persona and search queries
2. Use proper JSON output formatting
3. Handle JSON parsing and error cases
4. Return PersonaResult with correct data types

**Sample Solution Structure**:
```python
prompt = f"""
You are a Persona Architect. Create a detailed writer persona and search queries.

TOPIC: {topic}
STYLE REQUIREMENTS: {style_and_background}

Generate a JSON response with:
1. "persona_prompt": Detailed writer persona (expertise, style, voice)
2. "search_queries": Array of 3-5 targeted search queries

Output format:
{{
  "persona_prompt": "Detailed persona description...",
  "search_queries": ["query1", "query2", "query3"]
}}
"""

response = self.model.generate_content(prompt)
response_text = response.text.strip()

# Clean JSON markers
if response_text.startswith('```json'):
    response_text = response_text[7:-3].strip()

data = json.loads(response_text)
return PersonaResult(
    persona_prompt=data['persona_prompt'],
    search_queries=data['search_queries']
)
```

**Common Student Issues**:
- **JSON Parsing Errors**: Help them clean the response text properly
- **Missing Fields**: Ensure they request both persona and queries in the prompt
- **Type Errors**: Check they're returning PersonaResult with correct types

**Key Learning Points**:
- [ ] Prompt includes both persona and query generation
- [ ] JSON output is properly formatted and parsed
- [ ] PersonaResult is returned with valid data
- [ ] Error handling is implemented

### Exercise 2: Research Analyst

**What Students Need to Implement**:
```python
def conduct_research(self, search_queries: List[str]) -> ResearchResult:
```

**Key Implementation Points**:
1. Execute web searches for each query
2. Format search results for LLM analysis
3. Create synthesis prompt for research analysis
4. Handle empty search results gracefully

**Sample Solution Structure**:
```python
# Execute searches
all_results = []
for query in search_queries:
    results = self.web_searcher.search(query)
    all_results.extend(results)

if not all_results:
    return ResearchResult(content="No results found", source_count=0)

# Format for analysis
search_content = ""
for i, result in enumerate(all_results, 1):
    search_content += f"\n=== RESULT {i} ===\n"
    search_content += f"Title: {result.title}\n"
    search_content += f"URL: {result.url}\n"
    search_content += f"Content: {result.snippet}\n"

# Analysis prompt
analysis_prompt = f"""
Analyze these search results and create a comprehensive research summary.

SEARCH RESULTS:
{search_content}

Synthesize into coherent research content with --- RESEARCH START/END --- markers.
"""

response = self.model.generate_content(analysis_prompt)
return ResearchResult(content=response.text, source_count=len(all_results))
```

**Common Student Issues**:
- **Web Search Integration**: Help them use `self.web_searcher.search(query)`
- **Result Formatting**: Ensure they structure search data for LLM consumption
- **Empty Results**: Verify they handle cases with no search results
- **Synthesis Prompt**: Check they ask for analysis, not just compilation

**Key Learning Points**:
- [ ] Web searches are executed for all queries
- [ ] Search results are properly formatted
- [ ] LLM synthesis produces coherent research content
- [ ] ResearchResult includes content and source count
- [ ] Empty result cases are handled

### Exercise 3: Content Synthesizer

**What Students Need to Implement**:
```python
def write_blog_post(self, persona_prompt: str, research_content: str, 
                   topic: str, style_requirements: str, 
                   editorial_feedback: Optional[str] = None) -> BlogDraft:
```

**Key Implementation Points**:
1. Combine all inputs (persona, research, topic, style) in comprehensive prompt
2. Reference quality principles (P1-P5)
3. Handle optional editorial feedback for revisions
4. Return BlogDraft with proper version numbering

**Sample Solution Structure**:
```python
base_prompt = f"""
You are a Content Synthesizer. Write a high-quality blog post.

WRITER PERSONA: {persona_prompt}
RESEARCH CONTENT: {research_content}
TOPIC: {topic}
STYLE REQUIREMENTS: {style_requirements}

QUALITY PRINCIPLES TO FOLLOW:
{QUALITY_PRINCIPLES}

Write approximately 500 words in Markdown format with title.
Ensure all claims are traceable to research content.
"""

if editorial_feedback:
    base_prompt += f"""
    
EDITORIAL FEEDBACK TO ADDRESS:
{editorial_feedback}

Revise the content to specifically address these comments.
"""

response = self.model.generate_content(base_prompt)
version = 1 if editorial_feedback is None else 2

return BlogDraft(content=response.text.strip(), version=version)
```

**Common Student Issues**:
- **Input Integration**: Help them include all required inputs in the prompt
- **Quality Principles**: Ensure they reference QUALITY_PRINCIPLES variable
- **Editorial Feedback**: Check they handle the optional revision case
- **Version Logic**: Verify version = 1 for new, 2+ for revisions

**Key Learning Points**:
- [ ] All inputs are properly integrated into the prompt
- [ ] Quality principles are referenced
- [ ] Editorial feedback handling is implemented
- [ ] BlogDraft is returned with correct version
- [ ] Output is in Markdown format

### Exercise 4: Critic Agent

**What Students Need to Implement**:
```python
def evaluate_draft(self, draft_content: str, research_content: str, 
                  topic: str) -> QualityReview:
```

**Key Implementation Points**:
1. Create evaluation prompt that checks each quality principle (P1-P5)
2. Request structured JSON feedback
3. Parse JSON response with approval status and feedback
4. Handle evaluation errors gracefully

**Sample Solution Structure**:
```python
evaluation_prompt = f"""
You are a Critic Agent. Evaluate this blog draft against quality principles.

BLOG DRAFT: {draft_content}
RESEARCH CONTENT: {research_content}
TOPIC: {topic}

QUALITY PRINCIPLES TO EVALUATE:
{QUALITY_PRINCIPLES}

Evaluate each principle (P1-P5) and provide specific feedback.

Output as JSON:
{{
  "is_approved": true/false,
  "feedback": "Detailed feedback text",
  "issues_found": ["list", "of", "specific", "issues"]
}}
"""

response = self.model.generate_content(evaluation_prompt)
response_text = response.text.strip()

# Clean JSON markers
if response_text.startswith('```json'):
    response_text = response_text[7:-3].strip()

data = json.loads(response_text)
return QualityReview(
    is_approved=data['is_approved'],
    feedback=data['feedback'],
    issues_found=data['issues_found']
)
```

**Common Student Issues**:
- **Quality Principle Reference**: Ensure they include QUALITY_PRINCIPLES in prompt
- **JSON Structure**: Help them request the correct JSON format
- **Specific Feedback**: Check they ask for actionable, specific feedback
- **Error Handling**: Verify they handle JSON parsing errors

**Key Learning Points**:
- [ ] Evaluation prompt checks all quality principles
- [ ] JSON output is properly structured and parsed
- [ ] QualityReview is returned with all required fields
- [ ] Feedback is specific and actionable
- [ ] Error handling is implemented

### Exercise 5: Editor Agent & Orchestration

**What Students Need to Implement**:
1. `EditorAgent.make_editorial_decision()` method
2. All agent initialization in `BlogWorkflowOrchestrator.__init__()`
3. Complete workflow logic in `generate_blog_post()` method

**Key Implementation Points**:
1. Editorial decision logic based on critic feedback and cycle count
2. Proper agent initialization
3. Sequential workflow execution with iteration
4. File management and result tracking

**Sample Solution Structure**:

```python
# EditorAgent decision logic
def make_editorial_decision(self, quality_review, current_cycle, max_cycles):
    if quality_review.is_approved:
        return EditorReview(
            is_approved=True,
            comments=f"Excellent work! Draft approved after {current_cycle} cycles."
        )
    elif current_cycle >= max_cycles:
        return EditorReview(
            is_approved=True,
            comments=f"Maximum cycles reached. Approving current draft."
        )
    else:
        return EditorReview(
            is_approved=False,
            comments=f"Revision needed. Issues to address: {quality_review.feedback}"
        )

# Orchestrator initialization
def __init__(self, model, web_searcher):
    self.persona_architect = PersonaArchitect(model)
    self.research_analyst = ResearchAnalyst(model, web_searcher)
    self.content_synthesizer = ContentSynthesizer(model)
    self.critic_agent = CriticAgent(model)
    self.editor_agent = EditorAgent(model)

# Workflow execution
def generate_blog_post(self, topic, style_and_background):
    # Phase 1: Persona generation
    persona_result = self.persona_architect.generate_persona_and_queries(topic, style_and_background)
    
    # Phase 2: Research
    research_result = self.research_analyst.conduct_research(persona_result.search_queries)
    
    # Phase 3: Iterative content generation
    current_draft = None
    for cycle in range(1, 4):  # max 3 cycles
        if current_draft is None:
            draft = self.content_synthesizer.write_blog_post(
                persona_result.persona_prompt, research_result.content, topic, style_and_background
            )
        else:
            draft = self.content_synthesizer.write_blog_post(
                persona_result.persona_prompt, research_result.content, 
                topic, style_and_background, last_feedback
            )
        
        current_draft = draft
        
        quality_review = self.critic_agent.evaluate_draft(
            draft.content, research_result.content, topic
        )
        
        editorial_review = self.editor_agent.make_editorial_decision(
            quality_review, cycle, 3
        )
        
        if editorial_review.is_approved:
            break
        
        last_feedback = editorial_review.comments
    
    return current_draft.content, file_path
```

**Common Student Issues**:
- **Agent Initialization**: Help them create all agent instances
- **Workflow Logic**: Ensure they implement the iterative review loop
- **Data Flow**: Check that data flows correctly between agents
- **File Management**: Verify they use the FileManager properly

**Key Learning Points**:
- [ ] All agents are properly initialized
- [ ] Editorial decision logic handles all cases
- [ ] Workflow executes all phases sequentially
- [ ] Iterative improvement loop works correctly
- [ ] File management is implemented
- [ ] Integration test passes

---

## 🔧 Technical Support Guide

### Common Setup Issues

**Gemini API Key Problems**:
```python
# Help students add to Colab secrets:
# 1. Click key icon in left sidebar
# 2. Add secret: GEMINI_API_KEY
# 3. Enable notebook access
# 4. Restart runtime if needed
```

**Package Installation Issues**:
```python
# If imports fail, help students run:
!pip install google-generativeai beautifulsoup4 requests
```

**Web Search Problems**:
```python
# DuckDuckGo search may occasionally fail
# This is normal - help students implement error handling:
if not search_results:
    return ResearchResult(content="No results found", source_count=0)
```

### Debugging Strategies

**JSON Parsing Errors**:
1. Print the raw response to see format issues
2. Check for ```json``` markers that need cleaning
3. Verify the prompt asks for proper JSON structure

**Agent Communication Issues**:
1. Check return types match expected data classes
2. Verify all required fields are populated
3. Ensure proper error handling for edge cases

**Integration Problems**:
1. Test each agent individually before full workflow
2. Check that data flows correctly between phases
3. Verify file management creates output correctly

---

## 🚨 Student Support Strategies

### For Struggling Students

**Scaffolding Approach**:
1. Start with Exercise 1 and ensure solid understanding
2. Provide additional hints or code snippets if needed
3. Focus on one exercise at a time, don't overwhelm
4. Pair programming with stronger students

**Common Support Needs**:
- Help with prompt engineering for clear agent instructions
- Guidance on JSON parsing and data structure usage
- Assistance with debugging API calls and responses
- Support with understanding the workflow pattern

### For Advanced Students

**Extension Activities**:
- Add additional agents (fact-checker, SEO optimizer)
- Implement parallel processing for research
- Create more sophisticated evaluation criteria
- Build a user interface for the system

### Office Hours Preparation

**Key Topics to Review**:
1. ReAct framework application in each agent
2. JSON communication between agents
3. Iterative improvement patterns
4. Error handling strategies
5. API integration best practices

---

## 📝 Sample Feedback Templates

### Exercise Completion Feedback
```
Exercise [X] Review:

Strengths:
- [Specific positive implementations]
- [Good application of course concepts]

Areas for Improvement:
- [Specific technical issues]
- [Missing error handling]
- [Suggested enhancements]

Next Steps:
- [Specific action items]
- [Resources to review]

Status: [Complete/Needs Revision] - [Comments]
```

### Final Project Feedback
```
Capstone Project Evaluation:

Technical Implementation:
- Agent Design: [Comments]
- Workflow Integration: [Comments]
- Error Handling: [Comments]

Code Quality:
- Clean Implementation: [Comments]
- Following Instructions: [Comments]

Course Concept Application:
- ReAct Framework: [Comments]
- Agent Patterns: [Comments]

Overall Comments:
[Comprehensive feedback on the complete project]

Suggestions for Future Development:
[Ideas for extending the project]

Project Status: [Complete/Needs Additional Work]
```

---

**Remember**: This project represents the culmination of the entire AI Agents course. Students should feel proud of building a real, working multi-agent system that demonstrates cutting-edge AI capabilities!

---

*For additional support or questions about this TA guide, please refer to the course coordinator.*