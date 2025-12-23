# Technical Spec PRP: [System/Logic Name] - Precision Backend Standards

> Ingest the information from this file, implement the Low-Level Tasks, and generate the code that will satisfy the High and Mid-Level Objectives.

## 🎯 Objectives
**High-Level Objective**: [High level goal - e.g., "Implement a multi-tool Pydantic AI agent for automated database analysis"]

**Mid-Level Objectives**:
- [ ] [Concrete step 1: Define type-safe Pydantic schemas for tool inputs/outputs]
- [ ] [Concrete step 2: Implement core agent logic with tool orchestration and RunContext]
- [ ] [Concrete step 3: Integrate dependency injection (Deps) for Supabase access]

**Success Definition**: [e.g., "Agent correctly selects and executes tools with 95%+ accuracy in TestModel simulations"]

## 💡 Why & Who
- **Persona**: [e.g., AI Engineer / Backend Developer]
- **Value**: [e.g., "Automate complex SQL generation, reducing data team manual load by 50%"]
- **Problem**: [e.g., "Manual querying requires deep schema knowledge that end-users lack"]

## 📋 Context (The Delta)
### Context Completeness Check
_Before writing, validate: "Does the AI have the exact database schema, Pydantic AI documentation, and API contracts it needs?"_

### Documentation & References
```yaml
# MUST READ - Include these in your context window
- url: [https://ai.pydantic.dev/tools/](https://ai.pydantic.dev/tools/)
  why: Reference for tool registration patterns and RunContext usage
  critical: Use @agent.tool for context-aware tools; @agent.tool_plain for stateless ones.

- file: src/backend/agents/base_agent.py
  why: Pattern for model provider abstraction and agent configuration
  pattern: Follow the 'get_llm_model()' abstraction for provider-agnostic code.

- docfile: PRPs/ai_docs/pydantic_ai_patterns.md
  why: Custom guide for complex multi-step agent workflows
Beginning Context (Current State)
Bash

# Run 'tree -L 3 src/backend' and paste here to show existing files.
Ending Context (Desired State)
Bash

# List the exact files that WILL exist at the end of this implementation:
# src/backend/agents/{feature}/agent.py
# src/backend/agents/{feature}/tools.py
# src/backend/agents/{feature}/models.py
Known Gotchas & Library Quirks
CRITICAL: Pydantic AI agents require highly descriptive tool docstrings; the LLM uses these for selection logic.

CRITICAL: Use RunContext[Deps] for all database interactions to ensure thread-safe dependency injection.

CRITICAL: FastAPI requires async functions for agent endpoints to prevent blocking the event loop.

🏗️ Implementation Blueprint
Implementation Notes
Coding Standards: Follow PEP 8; use strict type hinting; all agent methods must be async.

Patterns: Use ResultType for structured outputs; implement @field_validator for data integrity.

Low-Level Tasks (Ordered Start to Finish)
For every task, the AI must answer these four questions before generating code:

1. [Task Name - e.g., Schema Definition]

- What prompt would you run to complete this task?
- What file do you want to CREATE or UPDATE?
- What function or class do you want to CREATE or UPDATE?
- What specific validation details (e.g., Zod/Pydantic rules) will drive the code?
2. [Task Name - e.g., Tool Implementation]

- What prompt would you run to complete this task?
- What file do you want to CREATE or UPDATE?
- What function or class do you want to CREATE or UPDATE?
- How will this tool use RunContext to interact with the database?
🧪 Validation Loop
Level 1: Syntax & Type Integrity
uv run ruff check src/backend --fix

uv run mypy src/backend

Level 2: Unit Logic (Mocked LLM)
uv run pytest tests/backend/test_{feature}_agent.py -v

Pattern: Use TestModel or FunctionModel to verify agent handling of structured data without hitting a real API.

Level 3: Integration (Real LLM)
Check: Verify Supabase queries are sanitized and return correct data.

Check: Run 5 standard queries through the agent and verify tool selection accuracy.

Level 4: Performance & Security
Security: Verify that Deps do not leak API keys into agent logs or tool outputs.

Performance: Measure "Time to First Token" (TTFT) and total execution time for complex tool chains.

🚫 Anti-Patterns to Avoid
❌ No Hardcoded Models: Do not use "gpt-4o" strings; use the environment-based model provider.

❌ No Tool Bloat: Do not create >10 tools per agent; use agent composition or nested agents.

❌ No Missing Docstrings: Never skip tool descriptions; the LLM will fail to select them correctly.

✅ Final Validation Checklist
[ ] All Low-Level Tasks completed in sequence.

[ ] npx tsc --noEmit and mypy return zero errors.

[ ] ResultType validation prevents malformed LLM responses.

[ ] Success Definition met (e.g., 95% tool accuracy).