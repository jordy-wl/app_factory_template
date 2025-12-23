To ensure your Antigravity App Factory maintains the highest velocity for tactical updates and bug fixes, we are merging the "Surgical Strike" task format from the reference repository with the User Persona and Story Metadata of your production-ready version.

This version of prp_story_task.md focuses on Traceability (Original Story) and Execution Density. By using specific keywords like IMPLEMENT, PATTERN, and IMPORTS within each task block, you force the AI to verify dependencies and logic patterns before it begins coding, drastically reducing "ImportError" loops.

Master Template 6: PRPs/templates/prp_story_task.md
File Path: .claude/templates/prp_story_task.md

Markdown

# Story PRP Template - Task Implementation Focus

---
name: "Story PRP Template - Task Implementation Focus"
description: "High-fidelity template for converting user stories into surgical, executable tasks"
---

## 📝 Original Story
> Paste the raw user story/task description from Jira, Linear, or Slack here.

[User story/task description]


## 📊 Story Metadata
**Story Type**: [Feature/Bug/Enhancement/Refactor]
**Estimated Complexity**: [Low/Medium/High]
**Primary Systems Affected**: [e.g., User Agent, Dashboard UI, Supabase Migrations]

---

## 🎯 Goal & Persona
**Feature Goal**: [e.g., "Implement pagination for the User Dashboard table"]
**Target User**: [e.g., Application Admin]
**User Journey**: 
1. [User navigates to list] -> 2. [Clicks 'Next'] -> 3. [New data loads via Server Action]

## 💡 Why
- **Business Value**: [e.g., "Improve performance by limiting initial data fetch to 20 items"]
- **Problem**: [e.g., "Current 500+ item fetches cause significant UI lag"]

---

## 📑 CONTEXT REFERENCES
_Auto-discovered documentation and patterns to follow_

```yaml
- file: {target_file_path}
  why: {Why this pattern/file is relevant}
  pattern: {Specific pattern to extract - e.g., 'Async tool definition'}
- docfile: {ai_docs_path}
  why: {Specific sections needed for implementation}
- external_url: {Library documentation or examples}
🏗️ IMPLEMENTATION TASKS
[Task blocks in dependency order - each block is atomic and testable]

Concept For Tasks
Information-Dense Keywords: Be specific about implementation steps.

Atomic & Testable: The developer (AI) should be able to complete a task using ONLY the context here.

Format Pattern:
[ACTION] {target_file}:
  - IMPLEMENT: {Specific logic detail}
  - PATTERN: {Reference existing codebase logic}
  - IMPORTS: {Required dependencies}
  - GOTCHA: {Known issues or constraints to avoid}
  - VALIDATE: `{executable validation command}`
1. Task Sequence
[MODIFY] src/backend/agents/{domain}_agent.py:

IMPLEMENT: Update {tool_name} to accept page and limit arguments.

PATTERN: Follow src/backend/agents/existing_agent.py for tool argument structure.

IMPORTS: from pydantic_ai import RunContext

GOTCHA: Supabase .range() is inclusive; calculate offsets carefully.

VALIDATE: uv run pytest tests/backend/test_{domain}_agent.py -v

[CREATE] src/frontend/components/{domain}/PaginationControls.tsx:

IMPLEMENT: Pagination UI with 'Next/Prev' buttons using Tailwind.

PATTERN: Use src/frontend/components/shared/Button.tsx for styling.

IMPORTS: import { useActionState } from 'react' (React 19)

VALIDATE: npm test src/frontend/components/{domain}/PaginationControls

[UPDATE] src/frontend/app/{route}/page.tsx:

IMPLEMENT: Connect the new Pagination component to the Server Action.

FIND: const data = await getItems()

INSERT: const data = await getItems({ page: searchParams.page })

VALIDATE: grep -q "PaginationControls" src/frontend/app/{route}/page.tsx

🧪 Validation Loop
Level 1 & 2: Integrity & Logic
Syntax: ruff check {file} --fix / npm run lint

Unit: uv run pytest {test} -v / npm test {test}

Level 3: Integration (System)
Data Flow: Verify RSC data passes correctly to Client Components.

State Check: Verify URL query parameters drive the UI state.

Service: curl -f http://localhost:8000/health || echo "Fail"

Level 4: Creative & Domain-Specific (MCP)
Leverage MCP servers for the "Self-Closing Loop":

Playwright MCP: playwright-mcp --url http://localhost:8000 --test-user-journey

Database MCP: database-mcp --validate-schema --test-queries

✅ COMPLETION CHECKLIST
[ ] All implementation tasks completed sequentially.

[ ] Each task validation command passed successfully.

[ ] Full project test suite passes (pytest / npm test).

[ ] No linting or type errors (mypy / tsc).

[ ] Story acceptance criteria (Success Criteria) met.

🚫 Anti-Patterns to Avoid
❌ No File Rewrites: Use targeted modifications to preserve existing logic.

❌ No Missing Imports: Always define required IMPORTS in the task block.

❌ No Skipped Audits: Never bypass Level 4 system/security audits.