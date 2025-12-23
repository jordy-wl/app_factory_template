# Law Book: pgvector & RAG Context Standards

> This document defines the mandatory protocols for semantic search and Retrieval-Augmented Generation (RAG). All agents must follow these precision standards to ensure AI responses are grounded in accurate, verified data.

## 1. Schema & Embedding Mandates
* **pgvector Extension**: Every RAG-enabled migration MUST explicitly enable the vector extension: `CREATE EXTENSION IF NOT EXISTS vector;`.
* **Deterministic Dimensions**: You MUST define the vector dimension based on the chosen model (e.g., `vector(1536)` for OpenAI `text-embedding-3-small` or `vector(768)` for Gemini embeddings).
* **Metadata Enrichment**: Table schemas for embeddings MUST include a `metadata` JSONB column to store citations, source URLs, and timestamps, ensuring the frontend can render accurate references.

## 2. Retrieval & Search Protocols
* **Similarity Thresholds**: Agents MUST implement a minimum similarity threshold (e.g., `match_threshold => 0.5`) in RPC functions to prevent the LLM from receiving irrelevant noise.
* **Hybrid Search**: For revenue-ready apps, prioritize "Hybrid Search" (combining pgvector similarity with Postgres Full-Text Search) to ensure keyword accuracy remains high.
* **Top-K Constraints**: Retrieval tools MUST limit the number of returned chunks (typically `match_count => 5`) to manage the LLM's context window and control costs.

## 3. Security & RLS for Vectors
* **Context Isolation**: RAG retrieval tools MUST honor Row Level Security (RLS). The RPC function used for searching MUST be executed with the user's JWT context to ensure users only search documents they own.
* **Dependency Injection**: Use the Pydantic AI `Deps` pattern to inject the authenticated Supabase client into retrieval tools, preventing "Context Leakage".

## 4. Documentation & Context Links
* **Supabase Vector Guide**: https://supabase.com/docs/guides/ai
* **pgvector Performance Tuning**: https://github.com/pgvector/pgvector#indexing
* **Pydantic AI RAG Patterns**: https://ai.pydantic.dev/multi-agent-applications/

## 5. Anti-Patterns
* ❌ **Context Stuffing**: Never pass more than 10 documents to an agent at once; use semantic reranking if a query returns too many matches.
* ❌ **Missing Indexes**: Implementing vector search without an `HNSW` or `IVFFlat` index is a performance failure that will lead to high latency.
* ❌ **Unvalidated Embeddings**: Forbidden to store embeddings without verifying the underlying text chunk hasn't changed. Implement a hashing mechanism to detect stale vectors.