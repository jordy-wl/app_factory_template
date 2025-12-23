# Command: ship
Finalize implemented features, sync with GitHub, and trigger production deployment.

## Arguments: $ARGUMENTS (The commit message for this release)

## Execution Process

### 1. Final Pre-Flight Check
- **Verification**: Confirm that the `/test-sandbox` command was run and all 4 levels of validation passed.
- **State Audit**: Ensure `TASK.md` is updated with all completed items for this feature.
- **Clean Up**: Remove any temporary debug files or logs created during implementation.

### 2. Atomic Git Workflow
- **Staging**: Stage all modified files using `git add .`.
- **Commit**: Create a semantic commit using the message in $ARGUMENTS (e.g., `feat: [description]`).
- **Sync**: Push the local feature branch to the remote repository.

### 3. GitHub PR Orchestration
- **PR Creation**: Use `gh pr create` to open a new Pull Request.
- **Documentation**: Automatically generate a PR body that summarizes:
    - The Implementation Goal from the PRP.
    - The specific files changed.
    - A summary of the sandbox test results.

### 4. Production Deployment
- **Vercel**: Trigger a production build and deployment using the Vercel CLI.
- **Supabase**: If database changes were made, apply production migrations and verify RLS policies in the live environment.

### 5. Post-Ship Lifecycle
- **Archive**: Move the active PRP blueprint from `PRPs/active/` to `PRPs/completed/`.
- **Status**: Notify the user: "Ship complete. PR created and Vercel deployment triggered."