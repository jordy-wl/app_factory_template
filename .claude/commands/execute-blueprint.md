# Command: execute-blueprint
Implement the software feature using the specified PRP blueprint.

## Arguments: $ARGUMENTS (The path to your blueprint, e.g., PRPs/active/build_plan.md)

## Execution Process

### 1. Load PRP & Context Internalization
- **Read**: Load the PRP file specified in $ARGUMENTS.
- **Absorb**: Internalize the Goal, Success Criteria, and Implementation Blueprint.
- **Verify Context**: Confirm you have access to every file mentioned. If a file path is missing or incorrect, use `rg` to find it.
- **Research Extension**: If the PRP mentions a library (like Pydantic AI) but lacks specific version context, search `ai_docs/` or the web to ensure production-grade implementation.

### 2. ULTRATHINK (Deep Task Mapping)
- **Pause**: Do not write code yet.
- **Checklist**: Use the `TodoWrite` tool to create a granular, step-by-step implementation plan.
- **Pattern Alignment**: Identify exact class structures and error-handling patterns from existing code in `src/` to follow.

### 3. Atomic Implementation
- **Execute**: Implement the code changes sequentially as defined in your Todo list.
- **Subagent Delegation**: 
    - Use `@ui-engineer` for Next.js/Tailwind components.
    - Use `@ai-architect` for Pydantic AI agent logic.
- **Standard**: Follow the monorepo split (Frontend vs. Backend) and RLS security rules.

### 4. Recursive Validation Loop
- **Execute**: Run every validation command defined in the PRP (Syntax, Unit, Integration).
- **Debug**: If any test fails, use the "Known Gotchas" section of the PRP to identify the root cause, fix it, and re-run.
- **Success Check**: You are NOT finished until 100% of the validation gates pass.

### 5. Completion & Review
- **Final Audit**: Re-read the PRP one last time to ensure every single requirement has been implemented.
- **Report**: Summarize the changes made and the test results.