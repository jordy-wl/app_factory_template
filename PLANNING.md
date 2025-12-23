# 🏛️ Planning: Architectural Control Center

> This document is the source of truth for the project's high-level architecture and strategic goals. Agents MUST consult this file before starting any feature implementation to ensure alignment with existing patterns.

## 🎯 Project Vision & Success Definition
- **Core Goal**: [Describe the primary problem this application solves in 1-2 sentences]
- **Revenue Target**: [e.g., "Subscription-based B2B SaaS for automated invoice processing"]
- **KPIs**: [e.g., "99.9% Webhook reliability", "Average AI response latency < 2s"]

## 🏗️ System Architecture Summary
- **Backend**: Python FastAPI with Pydantic AI agents following "The Trinity" (agent, tools, models).
- **Frontend**: Next.js 15 (App Router) + React 19 + Tailwind CSS.
- **Data & Security**: Supabase (Postgres) with mandatory Row Level Security (RLS).
- **Performance**: Redis-based rate limiting and hot-path caching.

## 🤖 Multi-Agent Orchestration Strategy
- **@ai-architect**: Responsible for Pydantic AI agentic loops and backend type safety.
- **@ui-engineer**: Responsible for Next.js 15 rendering patterns and Zod validation parity.
- **@devops-specialist**: Responsible for Supabase migrations, RLS audits, and Vercel deployment integrity.

## 🗺️ Roadmap & Active Milestones
- [ ] **Phase 1: Foundation**: [Core auth and database schema initialized].
- [ ] **Phase 2: MVP Features**: [List primary implementation goals].
- [ ] **Phase 3: Revenue Readiness**: [Stripe integration and observability verified].

## 📜 High-Level Architectural Decisions (ADR)
| Date | Decision | Rationale | Status |
| :--- | :--- | :--- | :--- |
| [Date] | [e.g., "Use TanStack Query for frontend"] | [e.g., "Need robust server-state caching"] | [Accepted] |
| [Date] | [e.g., "Strict Pydantic AI Graph"] | [e.g., "Managing complex iterative loops"] | [Pending] |

## 🔗 Context References
- **Master Protocol**: [CLAUDE.md](./CLAUDE.md).
- **Implementation Status**: [TASK.md](./TASK.md).
- **Security Standards**: [supabase_rls_master_guide.md](./PRPs/ai_docs/supabase_rls_master_guide.md).

## 🚫 Planning Anti-Patterns
- ❌ **Silent Architecture Changes**: Agents must not change core technologies without updating this file first.
- ❌ **Context Fragments**: Never keep major architectural goals only in a single PRP; mirror them here for project-wide awareness.