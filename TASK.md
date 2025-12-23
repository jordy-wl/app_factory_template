# 📋 Task Tracker: Implementation Ground Truth

> This file tracks the real-time status of the current implementation. Agents MUST update the status of each task immediately upon successful validation.

## 🚀 Current Feature: [Feature Name from INITIAL.md]
- **Branch**: `feat/[feature-slug]`
- **PRP Blueprint**: `PRPs/active/[feature-blueprint].md`
- **Overall Progress**: [0]%

---

## 🛠️ Vertical Slice Implementation
*Tasks are ordered by dependency. Validation must pass before marking as [DONE].*

### 1. Data Layer (Supabase)
- [ ] **Task 1.1**: Create Migration `supabase/migrations/[date]_add_[feature].sql`
  - *Validation*: `npx supabase db verify --rls-policies`
- [ ] **Task 1.2**: Audit RLS Policies for `auth.uid()` isolation
  - *Validation*: `audit-security` command success

### 2. Logic Layer (FastAPI & Pydantic AI)
- [ ] **Task 2.1**: Define `models.py` (Pydantic v2 schemas)
- [ ] **Task 2.2**: Implement `tools.py` (Agent functions with RunContext)
- [ ] **Task 2.3**: Implement `agent.py` (Orchestration logic)
- [ ] **Task 2.4**: Register API Router in `main.py`
  - *Validation*: `uv run pytest tests/backend/test_[feature].py`

### 3. Visual Layer (Next.js 15 & React 19)
- [ ] **Task 3.1**: Sync Contracts (Zod validation parity)
  - *Validation*: `sync-contracts` command success
- [ ] **Task 3.2**: Build Server Components for data fetching
- [ ] **Task 3.3**: Build Client Components with `useActionState`
- [ ] **Task 3.4**: Implement `error.tsx` and `loading.tsx` handlers
  - *Validation*: `npx tsc --noEmit && npm run lint`

### 4. Revenue & Shipping
- [ ] **Task 4.1**: Verify Stripe Webhook Idempotency
- [ ] **Task 4.2**: Full Sandbox Integration Test (`/test-sandbox`)
- [ ] **Task 4.3**: Create Pull Request (`/prp-core-pr`)

---

## 🚫 Blockers & Critical Notes
- [List any technical debt or unresolved clarifications here]

## ✅ Definition of Done
- [ ] All 4 validation levels pass.
- [ ] RLS policies verified by `@devops-specialist`.
- [ ] Zero TypeScript `any` types used.
- [ ] Commit message follows conventional format.