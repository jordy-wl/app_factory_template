# Redis Caching Strategy & Production Performance

> This document defines the mandatory protocols for utilizing Redis within the Antigravity App Factory. All agents must follow these precision standards to ensure high-performance data access and reliable rate limiting.

## 1. Architectural Mandates (The Speed Layer)
* **Async Connectivity**: All Redis operations in the backend MUST utilize `redis-py` (aioredis) to prevent blocking the FastAPI event loop.
* **Connection Pooling**: Agents MUST implement connection pooling via `async_from_url` to manage resources efficiently under high concurrency.
* **Scoped Keys**: All keys MUST be namespaced using the format `factory:{feature}:{version}:{key}` (e.g., `factory:auth:v1:user_id`) to prevent key collisions in shared environments.

## 2. Backend Rate Limiting (FastAPI)
* **Tiered Throttling**: Every revenue-ready endpoint MUST implement rate limiting based on the user's subscription tier (e.g., BASIC = 100/hr, PRO = 1000/hr).
* **Middleware Integration**: Use FastAPI dependencies to inject the limiter, ensuring that rate-limit checks occur before any expensive AI or database logic.
* **Custom Headers**: Production responses MUST include headers indicating `X-RateLimit-Limit`, `X-RateLimit-Remaining`, and `X-RateLimit-Reset`.

## 3. Frontend & Data Caching (Next.js 15)
* **Hot Path Caching**: Use Redis to store frequently accessed data that is expensive to query from Supabase (e.g., global configuration or processed RAG context).
* **Cache-Aside Pattern**: Implement the "Look-Aside" pattern: 1. Check Redis -> 2. If miss, Fetch from DB -> 3. Populate Redis with a defined TTL.
* **Deterministic TTL**: Forbidden to set infinite TTLs. Standard TTLs are: `SESSION` (1h), `FREQUENT_DATA` (5m), `STATIC_CONFIG` (24h).

## 4. Documentation & Context Links
* **redis-py (aioredis) Patterns**: https://redis.io/docs/latest/develop/clients/python/
* **FastAPI Rate Limiting Guide**: https://fastapi.tiangolo.com/advanced/custom-response/#custom-headers
* **Redis Caching Best Practices**: https://redis.io/docs/latest/develop/use/caching/

## 5. Anti-Patterns
* ❌ **Blocking the Loop**: Never use synchronous Redis commands in an `async def` function.
* ❌ **The Thundering Herd**: Avoid setting all cache items to expire at the exact same time; use small random jitters to prevent database spikes.
* ❌ **Plaintext Secrets**: Forbidden to store raw JWTs or PII in Redis without hashing or encryption.