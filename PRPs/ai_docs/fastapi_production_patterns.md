# Law Book: FastAPI Production Patterns & Async Orchestration

> This document defines the mandatory protocols for backend development within the factory. All agents must follow these precision standards to ensure high-performance, asynchronous, and revenue-ready backend services.

## 1. Architectural Mandates
* **Monorepo Alignment**: All backend code must reside in `src/backend/`.
* **Async by Default**: Every endpoint, database utility, and agent tool MUST be defined using `async def` to prevent blocking the event loop.
* **Vertical Slice Registry**: Organize code by feature (e.g., `src/backend/features/auth/`). Each feature must register its router in `src/backend/main.py` using a versioned prefix (e.g., `/api/v1/auth`).

## 2. Type Safety & Validation (Pydantic v2)
* **Pydantic Enforcement**: All request bodies and response models MUST use Pydantic v2 `BaseModel` or `ConfigDict`.
* **Strict Typing**: No `any` types; utilize Python 3.12+ type hinting for all function signatures.
* **ResultType Consistency**: Pydantic AI agent outputs MUST map directly to FastAPI response models to ensure contract parity with the frontend.

## 3. Security & Auth Protocols
* **Supabase JWT Validation**: Use the `@devops-specialist` approved middleware to validate Supabase JWTs on all protected routes.
* **Dependency Injection**: Utilize FastAPI's `Depends` for shared logic, such as retrieving the current user or the Supabase `service_role` client.
* **Sensitive Data**: Forbidden to log API keys, user PII, or raw database credentials.

## 4. Documentation & Context Links
* **FastAPI Advanced Patterns**: https://fastapi.tiangolo.com/advanced/
* **Security & JWT**: https://fastapi.tiangolo.com/tutorial/security/
* **Pydantic v2 Models**: https://docs.pydantic.dev/latest/concepts/models/

## 5. Anti-Patterns
* ❌ **Sync Blocking**: Never use `time.sleep()` or synchronous database drivers. Use `anyio.sleep()` or async counterparts exclusively.
* ❌ **Global State**: Avoid global database connections. Inject clients via the `Deps` or `Depends` pattern.
* ❌ **Vague Error Codes**: Do not return generic `500` errors. Use `HTTPException` with specific status codes and descriptive detail for the frontend.