# Command: test-sandbox
Perform comprehensive system validation in a local sandbox environment.

## Arguments: $ARGUMENTS (Optional: specific folder to test, e.g., src/backend)

## Execution Process

### 1. Environment Readiness
- **Read**: Check for any recently modified files in the path specified by $ARGUMENTS.
- **Subagent Sync**: Invoke `@devops-specialist` to ensure the local Supabase container is running and migrations are up to date.
- **Dependency Refresh**: Verify all Python (`venv_linux`) and Node dependencies are installed.

### 2. ULTRATHINK (Validation Strategy)
- **Map Gates**: Identify every validation command listed in the active PRP.
- **Safety Analysis**: Specifically plan an "RLS Breach Test" to prove a user cannot access data they don't own.
- **TodoWrite**: Create a validation checklist using the four levels of the PRP framework.

### 3. Level 1 & 2: Component Integrity
- **Syntax**: Run `ruff check --fix` and `mypy .` for the backend.
- **Frontend Hygiene**: Run `npm run lint` and `npm run type-check` for Next.js.
- **Unit Logic**: Execute `pytest` and `npm test`.
- **Fix Forward**: If any command fails, fix the code immediately and re-run this step.

### 4. Level 3 & 4: System & Security Verification
- **Integration**: Start the FastAPI and Next.js dev servers and perform a `curl` health check.
- **RLS Verification**: Use the Supabase CLI to verify that `SELECT` and `INSERT` policies are active on new tables.
- **End-to-End**: Simulate the "Core User Journey" from the PRP using a local browser check or script.

### 5. Validation Report
- **Summarize**: Report the status of all four validation levels.
- **Ship Readiness**: If all levels pass, explicitly notify the user: "Sandbox validated. Ready for `/ship`.".