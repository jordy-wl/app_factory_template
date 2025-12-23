# Pydantic AI: Production Agentic Framework & Multi-Agent Standards

> This document is the primary authority for building AI agents. All backend logic must follow these high-fidelity patterns to ensure modularity, cost control, and type safety.

## 1. Modular Architecture (The Trinity)
To prevent "Context Fog" and maintain the 500-line limit, every agent must be split across three files:
* **`agent.py`**: Orchestration logic and Agent instance.
* **`tools.py`**: Function definitions using `@agent.tool` (context-aware) or `@agent.tool_plain` (stateless).
* **`models.py`**: Pydantic schemas for `ResultType` and input validation.

## 2. Dependency Injection (`Deps` Architecture)
Agents MUST NOT use global variables or singleton clients. Use the `Deps` pattern to inject the Supabase client and user context. This ensures thread safety and allows for easier testing with `TestModel`.

```python
@dataclass
class Deps:
    supabase: Client        # Injected via FastAPI middleware
    user_id: str           # Extracted from JWT
    http_client: httpx.AsyncClient

# Mandatory: Use 'deps_type' for static type checking
agent = Agent('openai:gpt-4o', deps_type=Deps)
3. Multi-Agent Applications (Coordination Patterns)
The factory supports three levels of multi-agent complexity:

A. Agent Delegation (Recursive Tasks)
A "Manager" agent uses a "Worker" agent as a tool.

Cost Transparency: You MUST pass ctx.usage to the delegate run so costs aggregate to the parent.

Dependency Subsets: Worker agents should use a subset of the Manager's Deps.

Python

@manager_agent.tool
async def run_search(ctx: RunContext[Deps], query: str) -> str:
    # Aggregated usage tracking is mandatory
    result = await search_agent.run(query, deps=ctx.deps, usage=ctx.usage)
    return result.output
B. Programmatic Hand-off (State Machine)
One agent finishes, and the application code (FastAPI) decides which agent to call next based on the ResultType.

C. Graph-based Control Flow
For complex workflows (e.g., iterative code generation), use pydantic_graph to define a state machine.

4. Structured Output (ResultType)
Plain strings are for prototypes only. Production agents MUST use result_type to ensure the frontend receives validated JSON.

Constraint: Always use Field descriptions; the LLM uses these to understand the schema.

Validation: Use @field_validator in models.py to ensure data integrity before the response leaves the agent.

5. Usage Limits & Fail-Safes
To prevent cost spikes and infinite tool loops, all production agent.run() calls MUST implement UsageLimits.

Python

from pydantic_ai import UsageLimits

result = await agent.run(
    prompt,
    deps=deps,
    usage_limits=UsageLimits(
        request_limit=10, 
        total_tokens_limit=10000,
        tool_calls_limit=5
    )
)
🧪 Validation Gates (Evaluation Protocol)
Unit Tests: Use TestModel or FunctionModel to verify that agents handle structured data correctly without hitting live APIs.

Security Audit: Verify that Deps do not leak service_role keys into agent logs.