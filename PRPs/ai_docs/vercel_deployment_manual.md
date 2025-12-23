Law Book 10: vercel_deployment_manual.md
This document establishes the "Deployment Law" for the factory. It provides deterministic protocols for managing environments, branch-specific deployments, and production synchronization using Vercel and GitHub, ensuring that every scaffolded application can be shipped to a revenue-ready production state with zero manual configuration errors.

File Path: PRPs/ai_docs/vercel_deployment_manual.md

Monorepo Root Detection: Agents MUST configure the Vercel "Root Directory" to src/frontend/ while ensuring the src/backend/ directory is accessible for server-side API proxying or standalone deployment if required.

Environment Variable Sync: All variables defined in .env.example MUST be mirrored in the Vercel Dashboard before a production build is triggered. Never commit .env files to GitHub.

Edge Runtime vs. Node.js: Use the edge runtime for high-performance landing pages and the standard nodejs runtime for complex AI agentic loops that require heavy dependencies like pydantic-ai.

Preview Deployments: Every GitHub Pull Request MUST trigger a Vercel Preview Deployment. The @ui-engineer and @devops-specialist MUST verify the preview URL before marking a task as "Ready to Ship".

Production Promotion: Only merges into the main branch are eligible for production promotion. The /ship command automates this transition once sandbox validation is complete.

Supabase Integration: Production deployments MUST use the "Supabase Vercel Integration" to automatically sync NEXT_PUBLIC_SUPABASE_URL and NEXT_PUBLIC_SUPABASE_ANON_KEY across environments.

Log Drains: Revenue-ready apps MUST configure Vercel Log Drains to an external observability provider (e.g., BetterStack or Datadog) to capture runtime errors that occur during payment or agent loops.

Build Optimization: Agents MUST utilize Next.js output: 'standalone' in next.config.ts for optimized Docker-ready Vercel builds.

Deployment Protection: Enable "Deployment Protection" (Vercel Authentication) for all non-production branches to prevent unauthorized access to draft features.

Vercel Framework Docs: https://vercel.com/docs/frameworks/nextjs

Environment Variable Management: https://vercel.com/docs/projects/environment-variables

Vercel CLI Reference: https://vercel.com/docs/cli

❌ Manual Env Updates: Never manually edit Vercel production variables without updating the local .env.example file to maintain factory alignment.

❌ Bypassing Preview: Forbidden to ship directly to production without a verified Preview Deployment.

❌ PII in Logs: Never log STRIPE_SECRET_KEY or user authentication tokens during the deployment or build phase.