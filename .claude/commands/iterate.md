# Command: iterate
Implement iterative updates, bug fixes, or platform upgrades based on an UPDATES.md file.

## Arguments: $ARGUMENTS (The path to your update file, usually UPDATES.md)

## Execution Process

### 1. Context Sync & Diff Analysis
- **Read**: Load the update requirement from $ARGUMENTS.
- **Codebase Research**: Identify the "Affected Areas" by searching `src/` for existing logic.
- **Dependency Check**: If the update involves a platform upgrade or new API, research the corresponding files in `ai_docs/`.
- **Conflict Analysis**: Proactively check if the proposed change breaks existing features or security rules (RLS).

### 2. ULTRATHINK (Tactical Mapping)
- **Story Breakdown**: Do not create a full Base PRP. Instead, break the update into small, executable "Story Tasks".
- **TodoWrite**: Use `TodoWrite` to list the specific lines of code to be modified and any new files to be added.
- **Safety Gate Plan**: Identify exactly which tests in the Sandbox must pass to prove the update is successful.

### 3. Generate Iteration PRP
- **Draft**: Create a new Story PRP in `PRPs/updates/iteration_task.md` using the Story template patterns.
- **Tasks**: Include specific `UPDATE` and `CREATE` tasks with inline validation for each.
- **Integration**: If adding a data feed, define the exact API mapping and Auth secret requirements.

### 4. Implementation & Feedback Loop
- **Execute**: SEQUENTIALLY implement the changes.
- **Validate-as-you-go**: Run the inline validation command for EVERY task immediately after finishing it.
- **Auto-Fix**: If validation fails, fix the code and re-run until you see a success message.

### 5. Transition to Sandbox
- Once implemented, inform the user that the update is ready for full system verification using the `/test-sandbox` command.