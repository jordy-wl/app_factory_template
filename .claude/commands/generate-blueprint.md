# Command: generate-blueprint
Perform deep research and generate a comprehensive technical PRP blueprint.

## Arguments: $ARGUMENTS (Path to requirement file, e.g., INITIAL.md)

## Execution Process

### 1. Context Sync & Deep Research
- **Requirement Analysis**: Read the file at $ARGUMENTS to extract technical constraints and feature goals.
- **Codebase Analysis**: Invoke the `@codebase-analyst` subagent to find existing patterns for:
    - FastAPI endpoint structures and dependency injection in `src/backend/`.
    - Next.js 15 App Router conventions and Tailwind component styles in `src/frontend/`.
    - Supabase schema migrations and RLS security policies in `supabase/`.
- **Library Research**: Invoke the `@library-researcher` subagent to fetch the latest context for Pydantic AI, React 19, and pgvector from `ai_docs/` or the web.

### 2. ULTRATHINK (Strategy Mapping)
- **Architectural Pause**: Synthesize the gathered research into a coherent end-to-end plan.
- **Task Mapping**: Use the `TodoWrite` tool to create a research checklist ensuring no "Gotchas" (like rate limits or security leaks) are missed.
- **Confidence Check**: Score the proposed implementation strategy from 1-10. If the score is below 8, stop and ask the user for more documentation or clarification.

### 3. Generate Implementation PRP
- **Blueprint Creation**: Use the `PRPs/templates/prp_base.md` template to create a new file in `PRPs/active/build_plan.md`.
- **Vertical Slice Tasks**: Break the feature into tactical tasks (e.g., Task 1: Supabase RLS, Task 2: Pydantic AI Agent, Task 3: Next.js UI).
- **Validation Gates**: Define specific, executable commands for every level (Syntax, Unit Tests, Sandbox Integration, Security).

### 4. Final Quality Review
- **Verification**: Cross-reference the final blueprint against the original requirements in $ARGUMENTS.
- **Completion**: Inform the user that the blueprint is ready for their approval in the `PRPs/active/` folder.