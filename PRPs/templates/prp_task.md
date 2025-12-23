To complete your Antigravity App Factory toolset, we are merging the high-density task execution logic of the reference repository with your production-grade maintenance standards.

This high-fidelity version of prp_task.md moves beyond simple checklists. It implements a Surgical Execution Syntax—specifically designed to handle maintenance, dependency updates, and minor fixes with "Self-Healing" debug patterns that prevent the AI from getting stuck in an error loop.

Master Template 7: PRPs/templates/prp_task.md
File Path: .claude/templates/prp_task.md

Markdown

# Technical Task PRP: [Task Name] - High-Fidelity Implementation

---
Intended for surgical maintenance, configuration updates, and technical refinements.
---

## 🎯 Goal
**Task Goal**: [Specific, measurable technical outcome - e.g., "Upgrade Pydantic AI and fix breaking changes"]
**Deliverable**: [Concrete artifact - e.g., "Updated requirements.txt + resolved import errors"]
**Success Definition**: [e.g., "Application builds successfully and all core agent tests pass"]

## 💡 Why
- **Value**: [e.g., "Access latest streaming features and patch security vulnerabilities"]
- **Problem**: [e.g., "Current version has a known memory leak in long-running agent loops"]

## 📋 Standard Actions Keywords
- **READ**: Understand existing patterns before modifying.
- **CREATE**: New file with specific content.
- **UPDATE**: Modify existing file with surgical precision.
- **FIND**: Search for specific code patterns or signatures.
- **TEST**: Verify behavior using specific commands.
- **FIX**: Debug and repair identified issues.

---

## 📑 All Needed Context
### Context Completeness Check
_Before starting: "Do I have the exact version numbers, changelogs, and target file paths?"_

### Documentation & References
```yaml
# MUST READ - Include these in your context window
- url: [Official Docs/Changelog URL]
  why: [Specific method/section focus for the upgrade]
- file: [path/to/pattern/file.py]
  why: [Existing pattern for configuration or dependency management]
- gotchas:
    - issue: "Library X requires Y env var"
      fix: "Ensure .env.local is updated before testing"
Known Gotchas & Library Quirks
CRITICAL: Always use uv for Python updates to ensure deterministic, fast builds.

CRITICAL: Verify environment variables in the local sandbox after any config change.

CRITICAL: For Next.js config changes, a full npm run build is required to validate.

🏗️ Implementation Blueprint
1. Implementation Tasks (Granular Execution Format)
Every task must follow this strict syntax for machine-readable reliability:

[ACTION] {path/to/file}:
  - [OPERATION]: [Detailed description of the change]
  - VALIDATE: [Specific terminal command to prove this change works]
  - IF_FAIL: [Specific debug hint - e.g., "Check for circular imports in __init__.py"]
2. Implementation Archetypes (Quick Reference)
Add Feature: 1. READ similar -> 2. CREATE (COPY pattern) -> 3. UPDATE registry -> 4. TEST.

Fix Bug: 1. CREATE failing test -> 2. TEST (Confirm fail) -> 3. FIX code -> 4. TEST (Pass).

Refactor: 1. TEST baseline -> 2. UPDATE incrementally -> 3. DELETE old -> 4. TEST suite.

🧪 Validation Loop & Checkpoints
CHECKPOINT 1: Syntax & Style (Immediate)
RUN: uv run ruff check . --fix AND uv run mypy . (Backend)

RUN: npm run lint AND npx tsc --noEmit (Frontend)

REQUIRE: Zero errors before moving to logic validation.

CHECKPOINT 2: Logic & Component Tests
RUN: uv run pytest {path/to/affected/test}.py -v

IF_FAIL: Use the DEBUG test_failure pattern below.

CHECKPOINT 3: System Integration
RUN: Start services and run curl -f http://localhost:8000/health

EXPECT: "200 OK" or specific healthy JSON response.

🛠️ Debug Patterns (Self-Healing)
If a validation step fails, the AI must apply these patterns before asking for help:

DEBUG import_error:

CHECK: File exists at path.

CHECK: __init__.py presence in parent directories.

TRY: python -c "import path.to.module".

DEBUG test_failure:

RUN: uv run pytest -vvs {test_name}.

ACTION: Add print(f"DEBUG: {var}") to implementation.

IDENTIFY: Is it an assertion issue or a logic regression?

DEBUG api_error:

CHECK: Server status (ps aux | grep uvicorn or next).

READ: Last 50 lines of logs/app.log.

🚫 Maintenance Anti-Patterns
❌ No "Latest" Tags: Never use library: latest; always pin to a specific version.

❌ No Dirty Suites: Never commit configuration changes without running the full test suite.

❌ No Scope Creep: Do not mix feature development with maintenance tasks in the same PRP.