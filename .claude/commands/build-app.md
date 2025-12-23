# Command: build-app
Initialize the project environment and scaffold a new application.

## Arguments: $ARGUMENTS (The path to your requirements file, usually INITIAL.md)

## Execution Process

### 1. Requirement Deep-Dive
- **Read**: Load the requirement file specified in $ARGUMENTS.
- **Context Harvest**: Identify the Feature Goal, User Journey, and Data Models.
- **Clarify**: If any core technical detail (like Auth method or specific API version) is missing, you MUST prompt the user for details before proceeding.

### 2. ULTRATHINK (Scaffolding Logic)
- **Think Hard**: Analyze how to split this requirement into a Next.js frontend, FastAPI backend, and Supabase schema.
- **Plan**: Use the `TodoWrite` tool to list the folders to be created and the initial tracking files needed.
- **Pattern Match**: If this is a monorepo upgrade, scan existing folders for naming conventions.

### 3. Execute Scaffolding
- **Directories**: Create `src/frontend/`, `src/backend/`, and `supabase/` folders.
- **Core Logs**: Initialize `PLANNING.md` (architecture summary) and `TASK.md` (to-do list).
- **Environment**: Create `.env.example` files in the backend and frontend folders.

### 4. Validate Environment
- **Tree Check**: Run `tree -L 3` to verify the structure matches the Antigravity factory standard.
- **Rule Verification**: Confirm `CLAUDE.md` is present and active in the root.

### 5. Complete
- Summarize the scaffolded environment.
- **Ready State**: Inform the user that the project is "Primed" and ready for the `/generate-blueprint` command.