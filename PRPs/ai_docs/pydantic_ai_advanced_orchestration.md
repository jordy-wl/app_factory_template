# Law Book: Pydantic AI Advanced Orchestration & Multi-Agent Graphs

> This document defines the mandatory protocols for complex agentic workflows within the factory. All agents must follow these rules to ensure reliable, cost-controlled, and high-fidelity AI intelligence.

## 1. Multi-Agent Coordination Patterns
* **Cost Aggregation**: When a "Manager" agent delegates a task to a "Worker" agent, the worker MUST be called using `await worker_agent.run(..., usage=ctx.usage)` to ensure total session costs are tracked accurately.
* **Dependency Subsets**: Worker agents should receive a scoped subset of the Manager's `Deps` to prevent unnecessary data exposure and reduce context window pressure.
* **Hand-off Logic**: Use the `ResultType` in `models.py` to define explicit "Transfer" states. The application code (FastAPI) handles the transition between agents rather than agents calling each other directly in an unmanaged loop.

## 2. Graph-Based Control Flow (`pydantic_graph`)
* **State Machines**: For workflows requiring >3 iterative steps (e.g., code generation and linting), agents MUST use `pydantic_graph` to define a clear state machine.
* **Node Separation**: Every node in the graph must have a single responsibility (e.g., `ResearchNode`, `ImplementationNode`, `ValidationNode`).
* **History Management**: Graphs MUST utilize a `state` object to maintain continuity across nodes, preventing the LLM from repeating failed attempts.

## 3. Precision Validation & Self-Correction
* **Result Validators**: Utilize `@agent.result_validator` to perform secondary checks on structured outputs. If validation fails, the agent MUST be instructed to "Fix and retry" within its system prompt.
* **Usage Limits**: Every `agent.run()` call in a production environment MUST include a `UsageLimits` object with a `request_limit` (default: 5) and `total_tokens_limit`.

## 4. Documentation & Context Links
* **Multi-Agent Systems**: https://ai.pydantic.dev/multi-agent-applications/
* **Pydantic Graphs**: https://ai.pydantic.dev/graph/
* **Result Validation**: https://ai.pydantic.dev/results/#result-validators

## 5. Anti-Patterns
* ❌ **Recursive Prompting**: Forbidden to instruct an agent to "keep trying until successful" without a programmatic exit condition or `request_limit`.
* ❌ **Blind Delegation**: Worker agents should not have the same system prompt as the Manager; prompts must be specialized for the specific sub-task.
* ❌ **Implicit Context Leakage**: Do not pass the entire Supabase client to a worker agent if it only needs to read from one specific table.