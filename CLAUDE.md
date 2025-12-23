# 🚀 Antigravity App Factory: Master Protocol

## 🔄 Project Awareness & Context
- **Always read `INITIAL.md` or `UPDATES.md`** first. These are the source of truth for all requirements.
- **Consult `PLANNING.md`** for architecture goals and **`TASK.md`** for current progress before starting any task.
- **PRP Workflow**: No coding without a validated blueprint in `PRPs/active/`. Use `/generate-prp` to create one.
- **Git Hygiene**: Always create a new branch for every task. Commit format: `feat: [description]` or `fix: [description]`.

## 🧱 Code Structure & Modularity
- **Monorepo Split**:
  - `src/frontend/`: Next.js 15 (App Router), React 19, Tailwind CSS.
  - `src/backend/`: Python FastAPI with Pydantic AI Agents.
  - `supabase/`: Postgres logic with mandatory **Row Level Security (RLS)**.
- **File Limits**: Never exceed 500 lines per file or 200 lines per component. Split logic into modules if it gets too large.
- **Specialized Files**: For AI Agents, always separate `agent.py` (logic), `tools.py` (functions), and `prompts.py` (system instructions).

## 🧪 Testing & Reliability (Zero-Vibe Coding)
- **Validation Gates**: Every task MUST conclude with an executable validation command (e.g., `pytest`, `npm run lint`, `ruff check`).
- **Sandbox Testing**: All updates must be verified in a local sandbox using `/test-sandbox` before being deployed.
- **Type Safety**: Enforce strict TypeScript for frontend and Pydantic validation for backend. **NEVER use 'any'**.

## 🧠 AI Behavior Rules
- **No Vibe Coding**: If instructions are vague, you MUST ask for clarification. Do not guess.
- **Proactive Context**: Use `rg` (ripgrep) to find existing patterns before creating new ones.
- **Atomic Commits**: Create small, logical commits with clear descriptions.
- **Documentation**: Write Google-style docstrings for Python and JSDoc for TypeScript exports.

## 📋 Custom Command Reference
- `/build-app`: Scans INITIAL.md to generate a full-stack PRP.
- `/iterate {file}`: Analyzes existing code to plan an upgrade via UPDATES.md.
- `/test-sandbox`: Triggers local integration/RLS verification.
- `/ship`: Automates Git PR creation and production deployment to Vercel.