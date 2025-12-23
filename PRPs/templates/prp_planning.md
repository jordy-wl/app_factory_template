# Planning PRP: [System Name] - Strategic PRD & Roadmap

## 🎯 Planning Goal
**Goal**: [Define the architectural milestone - e.g., "Design the Multi-Agent Support Orchestrator"]
**Deliverable**: [e.g., "Technical PRD + Mermaid Diagrams + Vertical Implementation PRPs"]
**Success Definition**: [e.g., "Architecture approved with technical confidence > 8/10 and clear API contracts"]

## 🤖 Multi-Agent Orchestration
**Orchestration Strategy**: [How will agents collaborate? e.g., "Hierarchical: Architect delegates to UI and DevOps"]

**Agent Roles**:
- **@ai-architect**: Responsible for Pydantic AI agentic loops, tool definitions, and backend logic.
- **@ui-engineer**: Responsible for Next.js 15 App Router structure, React 19 state, and Tailwind UI.
- **@devops-specialist**: Responsible for Supabase RLS, database schema, and deployment pipelines.

## 💡 Why (Strategic Intent)
- **Business Impact**: [e.g., "Reduce server load by 30% through edge-side caching"]
- **User Needs**: [Identify specific pain points this architecture solves]
- **Risk Mitigation**: [Identify potential bottlenecks like LLM latency or Supabase connection limits]

---

## 🏗️ Phase 1: Idea Expansion & Research

### Context Gathering
```yaml
research_areas:
  technical_research:
    - existing_patterns: [Search codebase for similar agent implementations]
    - libraries: [Verify Next.js 15 / Pydantic AI compatibility for the use case]
    - patterns: [Identify Zod/Pydantic validation parity requirements]
  internal_context:
    - current_system: [Describe how this integrates with existing Supabase tables]
    - constraints: [e.g., "Must stay within Vercel serverless function timeouts"]
Initial Exploration
WEB_SEARCH: "{concept} best practices for Next.js 15 and Pydantic AI"

ANALYZE existing codebase: Find patterns for [similar feature] in src/backend/agents/.

🗺️ Phase 2: PRD Structure & Visual Thinking
1. User Stories & Primary Flow
Code snippet

graph LR
    A[User Trigger] --> B{Agent Decision}
    B -->|Query Data| C[Supabase pgvector]
    B -->|Call Tool| D[External API]
    C --> E[Final Response]
    D --> E
    E --> F[UI Optimistic Update]
2. High-Level Architecture
Code snippet

graph TB
    subgraph "Frontend (Next.js 15)"
        UI[User Interface]
        Actions[React 19 Server Actions]
    end
    
    subgraph "Backend (FastAPI/Pydantic AI)"
        Agent[Orchestrator Agent]
        Tools[Agent Tools]
    end
    
    subgraph "Data (Supabase)"
        DB[(PostgreSQL)]
        RLS[Row Level Security]
    end
    
    UI --> Actions
    Actions --> Agent
    Agent --> Tools
    Tools --> DB
    DB -.-> RLS
3. API & Data Flow Specifications
Code snippet

sequenceDiagram
    participant U as User
    participant F as Next.js Page
    participant A as Pydantic Agent
    participant D as Supabase
    
    U->>F: Input Query
    F->>A: Invoke Agent (Server Action)
    A->>D: Fetch Context (Vector Search)
    D-->>A: Context Data
    A->>A: Process & Validate (Zod)
    A-->>F: Streamed Markdown Result
    F-->>U: Final UI Render
🏗️ Phase 3: Strategic Implementation Phases
Phase 1: Foundation (The Skeleton)
Action: Define Shared Types, Pydantic Models, and Supabase Migrations.

Outcome: src/shared and supabase/migrations initialized.

Phase 2: Core Logic (The Brain)
Action: Implement Pydantic AI Agents and Tools.

Outcome: Backend logic passing unit tests via TestModel.

Phase 3: User Interface (The Skin)
Action: Build Next.js 15 Pages and Components.

Outcome: Full UI integration with Server Actions.

😈 Phase 4: Devil's Advocate (Validation & Risk)
Challenge Analysis
YAML

technical_risks:
  - risk: "Supabase RLS might block Agent tool access"
    mitigation: "Use 'Deps' pattern to inject authenticated client"
  - risk: "Next.js hydration mismatch on streaming responses"
    mitigation: "Implement Suspense boundaries for AI components"

edge_cases:
  - scenario: "LLM returns invalid JSON for structured output"
    handling: "Use ResultType with Pydantic validators and retry logic"
  - scenario: "Database connection spike during parallel agent runs"
    handling: "Implement connection pooling or rate limiting"
Strategic Validation Gates
Level 1: Interface Integrity: Verify Backend Pydantic models match Frontend Zod schemas.

Level 2: Security Modeling: Audit Supabase RLS policies for potential data leakage.

Level 3: Scalability: Verify async streaming doesn't block the FastAPI event loop.

🚫 Strategic Anti-Patterns
❌ No Giant Monoliths: Avoid creating agents with >10 tools; decompose if complex.

❌ No Direct DB Access: Frontend should never bypass Server Actions/RLS.

❌ No Vague Metrics: Avoid "Faster UI"; use "Page Load < 200ms".

✅ Definition of Done
[ ] PRD includes all 3 Mermaid diagrams.

[ ] Multi-agent roles are clearly defined.

[ ] Implementation phases are mapped to specific prp_base.md targets.

[ ] "Devil's Advocate" mitigations are documented in the code comments.