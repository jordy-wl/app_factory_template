## Goal

**Feature Goal**: [Specific, measurable end state - e.g., "Implement RAG-powered customer support chat"]

**Deliverable**: [Vertical slice: Database schema + Pydantic AI Agent + Next.js UI]

**Success Definition**: [How you'll know it's working - e.g., "Agent answers queries with 90%+ accuracy based on provided docs"]

## User Persona

**Target User**: [e.g., End-user customer]

**Use Case**: [e.g., Asking questions about order status or product features]

**User Journey**: [1. User types query -> 2. Agent fetches context from Supabase -> 3. User receives streaming response]

## Why

- [Business value: Reduce support ticket volume by 40%]
- [Integration: Connects to existing Order Management database]
- [Problem: Customers currently wait 24h for email responses]

## What

### Success Criteria

- [ ] [Structured response includes citations from documentation]
- [ ] [UI supports Markdown rendering and code snippets]
- [ ] [Security: Users can only query their own data via RLS]

## All Needed Context

### Context Completeness Check

_Before writing this PRP, validate: "If someone knew nothing about this codebase, would they have everything needed to implement this successfully?"_

### Documentation & References

```yaml
- url: [https://ai.pydantic.dev/](https://ai.pydantic.dev/)
  why: Implementation of Agentic loops and Dependency Injection
  critical: MUST use 'Deps' for Supabase client injection to ensure thread safety.

- file: src/backend/agents/base_agent.py
  why: Class structure for Pydantic AI agents
  pattern: Use the 'Agent' class with 'ResultType' for structured output validation.

- docfile: PRPs/ai_docs/supabase_rls_guide.md
  why: Security standards for new tables
Current Codebase Tree
Bash

# Run 'tree -L 3' in the root and paste output here
Desired Codebase Tree
Bash

# Map the new files:
# supabase/migrations/[date]_add_feature.sql
# src/backend/agents/feature_agent.py
# src/frontend/app/feature/page.tsx
Known Gotchas & Library Quirks
CRITICAL: Next.js 15 Server Components are the default; use "use client" ONLY for the Chat Input.

CRITICAL: FastAPI agents must be async to prevent blocking the event loop.

Implementation Blueprint
Data models and structure
[Define Pydantic Schemas for input/output and Supabase Table Types]

Implementation Tasks (ordered by dependencies)
YAML

Task 1: CREATE supabase/migrations/{feature}_schema.sql
  - IMPLEMENT: Table structure and Row Level Security (RLS) policies
  - FOLLOW pattern: supabase/migrations/existing_table.sql
  - SECURITY: Use 'auth.uid()' to restrict data access

Task 2: CREATE src/backend/models/{feature}_models.py
  - IMPLEMENT: Pydantic schemas for Agent Input and Structured Output
  - NAMING: snake_case for fields, CamelCase for classes

Task 3: CREATE src/backend/agents/{feature}_agent.py
  - IMPLEMENT: Pydantic AI Agent with system prompts and tools
  - DEPENDENCIES: Import models from Task 2; Inject Supabase via Deps
  - PLACEMENT: src/backend/agents/

Task 4: CREATE src/frontend/components/{feature}/FeatureUI.tsx
  - IMPLEMENT: React 19 Client Component for interactivity
  - FOLLOW pattern: src/frontend/components/shared/BaseUI.tsx

Task 5: INTEGRATE src/backend/main.py
  - ACTION: Register new FastAPI route for the feature agent
Validation Loop
Level 1: Syntax & Style
uv run ruff check src/backend --fix

npm run lint (Frontend)

uv run mypy src/backend

Level 2: Unit Tests
uv run pytest tests/backend/test_{feature}.py -v

npm test src/frontend/components/{feature}

Level 3: Sandbox Integration
DB Check: supabase db verify (Check RLS status)

API Check: curl -X POST http://localhost:8000/api/{feature} -d '{"input": "test"}'

UI Check: Verify Next.js page loads without hydration errors.

Level 4: Domain-Specific Validation
Security: Attempt to fetch 'User B' data while logged in as 'User A' (Must return 403).

Agent Accuracy: Run 10 sample queries and verify structured output matches schema.

Anti-Patterns to Avoid
❌ Do not bypass RLS by using the 'service_role' key in the frontend.

❌ Do not use 'any' types in Python logic; use Pydantic models.


---



