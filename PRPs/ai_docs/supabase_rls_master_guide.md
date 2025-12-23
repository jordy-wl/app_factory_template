# Law Book: Supabase RLS Master Guide & Security Protocols

> This document is the final authority on database security. Row Level Security (RLS) is NOT optional. Every table created in the factory must have a verified security policy before it is eligible for shipping.

## 1. Mandatory RLS Initialization
* **Default Deny**: Every new table migration MUST begin by enabling RLS: `ALTER TABLE {table_name} ENABLE ROW LEVEL SECURITY;`.
* **Authenticated Access**: By default, all policies must be scoped `TO authenticated` to prevent anonymous public access unless the feature goal explicitly requires it.
* **Owner-Only Logic**: The primary policy for every user-facing table must ensure that `(auth.uid() = user_id)` to enforce strict data isolation.

## 2. Pydantic AI Integration (The 'Deps' Pattern)
* **Secure Client Injection**: Agents MUST utilize the `RunContext[Deps]` pattern to inject an authenticated Supabase client.
* **No Service Role in Frontend**: Forbidden to use the `service_role` key in the Next.js frontend or client components. All high-privilege operations must occur in the `src/backend/` logic layer.
* **JWT Verification**: The backend must verify the Supabase JWT before performing any operation that depends on `auth.uid()`.

## 3. Migration & Verification Protocol
* **Surgical Migrations**: All RLS policies must be defined within the `supabase/migrations/` folder using the Supabase CLI standard.
* **Policy Audit**: The `@devops-specialist` agent must run a verification check (`npx supabase db verify --rls-policies`) before any PR is created.
* **Atomic Security**: Do not mix schema changes and security policies in a way that allows a "security-less" window during deployment.

## 4. Documentation & Context Links
* **Supabase RLS Documentation**: https://supabase.com/docs/guides/auth/row-level-security
* **Postgres Policy Syntax**: https://www.postgresql.org/docs/current/sql-createpolicy.html
* **Auth Helper Reference**: https://supabase.com/docs/guides/auth/auth-helpers/nextjs

## 5. Anti-Patterns
* ❌ **Missing Policies**: Shipping a table without an RLS policy is a blocking failure.
* ❌ **Selective Logic**: Relying on application-level filters (e.g., `WHERE user_id = ...`) instead of RLS policies. RLS must be the primary gate.
* ❌ **Service Role Leakage**: Using the `service_role` key to bypass RLS in an agent tool without documenting the specific security trade-off.