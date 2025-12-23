# Base PRP Template - Implementation-Focused with Precision Standards

## Goal
**Feature Goal**: [Specific, measurable end state - e.g., "Implement RAG-powered customer support chat"]
**Deliverable**: [Vertical slice: Database schema + Pydantic AI Agent + Next.js UI]
**Success Definition**: [e.g., "Agent answers queries with 90%+ accuracy based on provided docs"]

## User Persona
**Target User**: [e.g., End-user customer]
**Use Case**: [e.g., Asking questions about order status or product features]
**User Journey**: 
1. [User types query] -> 2. [Agent fetches context from Supabase] -> 3. [User receives streaming response]
**Pain Points Addressed**: [e.g., "Customers currently wait 24h for email responses; this reduces latency to seconds"]

## Why
- [Business value: Reduce support ticket volume by 40%]
- [Integration: Connects to existing Order Management database]
- [Problems this solves and for whom]

## What
[User-visible behavior and technical requirements]

### Success Criteria
- [ ] [Structured response includes citations from documentation]
- [ ] [UI supports Markdown rendering and code snippets]
- [ ] [Security: Users can only query their own data via RLS]

## All Needed Context

### Context Completeness Check
_Before writing this PRP, validate: "If someone knew nothing about this codebase, would they have everything needed to implement this successfully?"_

### Documentation & References
```yaml
# MUST READ - Include these in your context window
- url: [https://ai.pydantic.dev/](https://ai.pydantic.dev/)
  why: Implementation of Agentic loops and Dependency Injection
  critical: MUST use 'Deps' for Supabase client injection to ensure thread safety.

- file: src/backend/agents/base_agent.py
  why: Class structure for Pydantic AI agents
  pattern: Use the 'Agent' class with 'ResultType' for structured output validation.

- docfile: PRPs/ai_docs/supabase_rls_guide.md
  why: Security standards for new tables
  section: "Best Practices for auth.uid() policies"
Current Codebase Tree
Bash

# Run 'tree -L 3' in the root and paste output here
Desired Codebase Tree
Bash

# Map the new files and their responsibilities:
# supabase/migrations/[date]_add_feature.sql (DB Schema)
# src/backend/agents/feature_agent.py (AI Logic)
# src/frontend/app/feature/page.tsx (UI Entry)
Known Gotchas & Library Quirks
Python

# CRITICAL: Next.js 15 Server Components are the default; use "use client" ONLY for interactive Chat Input.
# CRITICAL: FastAPI agents must be async to prevent blocking the event loop.
# CRITICAL: Pydantic AI tools require descriptive docstrings for the LLM to select them correctly.
Implementation Blueprint
Data models and structure
[Define Pydantic Schemas for input/output and Supabase Table Types]

Implementation Tasks (ordered by dependencies)
YAML

Task 1: CREATE supabase/migrations/{feature}_schema.sql
  - IMPLEMENT: Table structure and Row Level Security (RLS) policies
  - FOLLOW pattern: supabase/migrations/existing_table.sql
  - SECURITY: Use 'auth.uid()' to restrict data access; apply 'TO authenticated'.

Task 2: CREATE src/backend/models/{feature}_models.py
  - IMPLEMENT: Pydantic schemas for Agent Input and Structured Output
  - NAMING: snake_case for fields, CamelCase for classes

Task 3: CREATE src/backend/agents/{feature}_agent.py
  - IMPLEMENT: Pydantic AI Agent with system prompts and tools
  - DEPENDENCIES: Inject Supabase client via RunContext[Deps]
  - PLACEMENT: src/backend/agents/

Task 4: CREATE src/frontend/components/{feature}/FeatureUI.tsx
  - IMPLEMENT: React 19 Client Component with Tailwind styling
  - FOLLOW pattern: src/frontend/components/shared/BaseUI.tsx

Task 5: INTEGRATE src/backend/main.py
  - ACTION: Register new FastAPI route for the feature agent

Task 6: CREATE tests/backend/test_{feature}_agent.py
  - IMPLEMENT: Unit tests using Pydantic AI 'TestModel'
Implementation Patterns & Key Details
Python

# Example: Pydantic AI Agent Tool Pattern
@agent.tool
async def search_docs(ctx: RunContext[Deps], query: str) -> str:
    # PATTERN: Use dependency-injected client for DB access
    results = await ctx.deps.supabase.table('docs').select('*').text_search('content', query).execute()
    return format_results(results)

# Example: Next.js 15 Server Action Pattern
"use server"
export async function submitPrompt(formData: FormData) {
    // PATTERN: Server Action for secure backend calls
    const response = await fetch(`${process.env.BACKEND_URL}/chat`, { ... });
    return response.json();
}
Integration Points
YAML

DATABASE:
  - migration: "CREATE TABLE chat_history (id uuid DEFAULT uuid_generate_v4()...)"
  - security: "ALTER TABLE chat_history ENABLE ROW LEVEL SECURITY;"

CONFIG:
  - add to: src/backend/settings.py
  - pattern: "AGENT_MODEL = os.getenv('AGENT_MODEL', 'gpt-4o')"

ROUTES:
  - add to: src/backend/main.py
  - pattern: "app.include_router(chat_router, prefix='/api/chat')"
Validation Loop
Level 1: Syntax & Style (Immediate Feedback)
Bash

# Backend Check
ruff check src/backend --fix
mypy src/backend

# Frontend Check
npm run lint
npm run type-check
Level 2: Unit Tests (Component Validation)
Bash

# Run agent tests (Pydantic AI)
uv run pytest tests/backend/test_{feature}_agent.py -v

# Run component tests (Vitest)
npm test src/frontend/components/{feature}
Level 3: Integration Testing (System Validation)
Bash

# Service Health Check
curl -f http://localhost:8000/health || echo "FastAPI failed"

# Agent Accuracy Test (Real LLM)
# Run a sample query and verify the citations in the JSON response
curl -X POST http://localhost:8000/api/{feature} -d '{"query": "When is my order arriving?"}' | jq .
Level 4: Creative & Domain-Specific Validation
Bash

# Security: RLS Breach Test
# Attempt to access another user's ID via the Supabase client (Must return empty/403)
npx supabase db verify --rls-policies

# UI: Hydration & Performance Check
# Verify Next.js page loads without hydration errors and TTFT < 500ms
playwright test src/frontend/e2e/{feature}.test.ts
Final Validation Checklist
Technical Validation
[ ] All 4 validation levels completed successfully

[ ] No linting errors: ruff check / npm run lint

[ ] All tests pass: pytest / npm test

Feature Validation
[ ] All success criteria from "What" section met

[ ] Agent correctly uses citations in responses

[ ] User persona requirements satisfied

Code Quality & Security
[ ] RLS policies confirmed for all new tables

[ ] Pydantic AI 'Deps' used for all external client access

[ ] No 'any' types used in Logic or UI

Anti-Patterns to Avoid
❌ Don't bypass RLS by using the 'service_role' key in the frontend.

❌ Don't skip validation because "it should work".

❌ Don't use sync functions in an async FastAPI context.

❌ Don't hardcode model strings; use the environment-based configuration.