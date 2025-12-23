Master Template: prp_fullstack_feature.md
This master template unifies the database, backend, and frontend implementation into a single "Vertical Slice" implementation plan. It is designed to ensure one-pass implementation success for revenue-ready features by enforcing the monorepo architecture and security protocols defined in your factory's "Law Books".

File Path: PRPs/templates/prp_fullstack_feature.md

Markdown

# Full-Stack Feature PRP: [Feature Name] - End-to-End Production Standard

> Ingest this blueprint to implement a complete vertical slice. You must coordinate the Supabase schema, Pydantic AI agent logic, and Next.js 15 UI according to factory protocols.

## 🎯 Goal
**Feature Goal**: [Specific end state - e.g., "Implement an automated AI invoice processing system"]
**Deliverables**: 
- [ ] **Database**: Supabase migrations with mandatory RLS
- [ ] **Backend**: Pydantic AI agent with structured `ResultType` and FastAPI endpoints
- [ ] **Frontend**: Next.js 15 App Router pages with React 19 Server Components and Zod validation

**Success Definition**: [e.g., "Users can upload a PDF and receive a validated, structured invoice record in their dashboard with 95% accuracy"]

## 👤 User Persona & Journey
**Target User**: [e.g., Small Business Owner]
**User Journey**:
1. [User Action] -> 2. [Database Record Created] -> 3. [AI Agent Processes Task] -> 4. [UI Updates via Server Action]

## 💡 Why & Revenue Impact
- **Business Value**: [How this drives revenue or reduces churn]
- **Integration**: [Connections to Stripe or existing data feeds]

---

## 📋 All Needed Context

### Context Completeness Check
_Before execution, validate: "Does the AI have the exact Supabase table schemas, Pydantic AI 'Deps' requirements, and UI design tokens?"_

### Documentation & References (High-Fidelity)
```yaml
# MUST READ - Implementation Protocols
- docfile: PRPs/ai_docs/nextjs_15_react_19_standards.md
  why: Mandatory frontend rendering and validation rules
- docfile: PRPs/ai_docs/pydantic_ai_patterns.md
  why: Strict backend agent and dependency injection standards
- docfile: PRPs/ai_docs/supabase_rls_master_guide.md
  why: Non-negotiable security protocols for data isolation
- docfile: PRPs/ai_docs/revenue_readiness_stripe.md
  why: Protocols for payment and subscription lifecycle management
- url: [Specific API or Library URL]
  why: Precision syntax for external integrations
Current Codebase State
Backend Architecture: agent.py, tools.py, models.py trinity.

Frontend Architecture: Server Component default with use client interactivity islands.

🏗️ Implementation Blueprint
Data Models & Contracts
Define the bridge between Backend Pydantic models and Frontend Zod schemas.

Step-by-Step Implementation Tasks
Task 1: [DB] CREATE supabase/migrations/{feature}_schema.sql

ACTION: Define table structure and enable RLS immediately.

SECURITY: Implement auth.uid() = user_id policy.

VALIDATE: npx supabase db verify --rls-policies

Task 2: [BE] CREATE src/backend/features/{feature}/ trinitiy

ACTION: Implement agent.py, tools.py, and models.py.

LOGIC: Use RunContext[Deps] for Supabase client injection.

VALIDATE: uv run pytest tests/backend/test_{feature}_agent.py

Task 3: [FE] CREATE src/frontend/app/{feature}/page.tsx

ACTION: Build route entry using Next.js 15 Server Components.

VALIDATE: npx tsc --noEmit and npm run lint

🧪 Validation Loop
Level 1: Component Integrity
Syntax: ruff check --fix (BE) and npm run lint (FE).

Types: mypy . (BE) and npx tsc --noEmit (FE).

Level 2: Unit Logic
Agent: Test structured outputs using TestModel.

UI: Verify component rendering with Vitest.

Level 3: System Integration (Sandbox)
Health: curl -f http://localhost:8000/health.

End-to-End: Run /test-sandbox to verify the "Core User Journey".

Level 4: Production Audit
Security: Audit RLS policies and verify zero exposure of secret keys.

Performance: Check Vercel build output for optimal bundle sizes.

🚫 Full-Stack Anti-Patterns
❌ No Mixed Logic: Never put database queries directly in React components.

❌ No Bypass RLS: Forbidden to use service_role keys in client-side code.

❌ No Vibe Coding: If the API contract is missing a field, you MUST ask for clarification.

✅ Ready to Ship? Run /ship only after 100% validation success.