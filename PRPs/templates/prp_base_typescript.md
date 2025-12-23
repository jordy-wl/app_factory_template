# TypeScript/UI PRP Template v3 - Implementation-Focused with Precision Standards

## Goal

**Feature Goal**: [Specific, measurable UI end state - e.g., "Implement responsive, accessible data table with server-side sorting"]

**Deliverable**: [Concrete artifact - Next.js 15 Page + React Server Components + Client-side Interactivity]

**Success Definition**: [How you'll know this is complete and working - e.g., "Table renders in <100ms and passes all ARIA accessibility checks"]

## User Persona (if applicable)

**Target User**: [e.g., Application End User / Data Analyst]

**Use Case**: [e.g., Viewing and managing complex datasets across multiple pages]

**User Journey**: [1. User navigates to page -> 2. RSC fetches initial data -> 3. User interacts with filters -> 4. UI updates optimistically]

**Pain Points Addressed**: [e.g., "Slow page loads when switching filters" or "Lack of mobile accessibility"]

## Why

- [Business value: Improve data visibility and decision-making speed for users]
- [Integration: Connects to existing Backend Search API and Supabase Auth]
- [Problems this solves and for whom]

## What

[User-visible behavior and technical requirements]

### Success Criteria

- [ ] [Next.js 15 App Router structure used correctly (Server/Client split)]
- [ ] [React 19 Server Components used for data fetching by default]
- [ ] [Zod schemas used for all form and API response validation]
- [ ] [Fully responsive UI using Tailwind CSS grid/flex patterns]

## All Needed Context

### Context Completeness Check

_Before writing this PRP, validate: "If someone knew nothing about this codebase, would they have everything needed to implement this successfully?"_

### Documentation & References

```yaml
# MUST READ - Include these in your context window
- url: [https://nextjs.org/docs/app/building-your-application/rendering/server-components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)
  why: Core architectural pattern for Next.js 15 rendering
  critical: MUST use Server Components for data fetching to maximize performance and security.

- file: src/frontend/components/shared/BaseComponent.tsx
  why: Pattern for standardizing component structure and prop types
  pattern: Use 'ReactElement' as return type; avoid 'JSX.Element'.
  gotcha: Requires 'use client' if using browser-only hooks like useEffect.

- docfile: PRPs/ai_docs/tailwind_design_system.md
  why: Standardized spacing, colors, and typography rules
Current Codebase tree
Bash

# Run 'tree -L 3 src/frontend' to get an overview
Desired Codebase tree
Bash

# Map the new files and their responsibilities:
# src/frontend/lib/validations/{feature}.ts (Zod Schemas)
# src/frontend/components/{feature}/FeatureItem.tsx (Pure UI)
# src/frontend/app/[feature-route]/page.tsx (Route/Entry)
Known Gotchas & Library Quirks
TypeScript

// CRITICAL: Next.js 15 requires async/await for App Router parameters (params, searchParams).
// CRITICAL: 'use client' directive must be at top of file, affects entire component tree.
// CRITICAL: Server Components cannot use browser APIs (window, localStorage) or event handlers.
// CRITICAL: Tailwind 'peer' and 'group' states must be used for complex CSS interactions.
Implementation Blueprint
Data models and structure
Create core data models to ensure type safety and consistency.

TypeScript

// Examples:
// - Zod schemas for API validation
// - TypeScript interfaces for Component props
// - Shared types in src/frontend/lib/types/
Implementation Tasks (ordered by dependencies)
YAML

Task 1: CREATE src/frontend/lib/validations/{feature}.ts
  - IMPLEMENT: Zod schemas for API responses and form inputs
  - FOLLOW pattern: src/frontend/lib/validations/existing.ts
  - NAMING: {Feature}Schema, type {Feature} = z.infer<typeof ...>
  - PLACEMENT: Validation schemas in src/frontend/lib/validations/

Task 2: CREATE src/frontend/components/{feature}/FeatureItem.tsx
  - IMPLEMENT: Pure UI presentation component with Tailwind
  - FOLLOW pattern: src/frontend/components/shared/BaseUI.tsx
  - NAMING: PascalCase for components, camelCase for props
  - DEPENDENCIES: Import types/schemas from Task 1
  - PLACEMENT: Presentation layer in src/frontend/components/{feature}/

Task 3: CREATE src/frontend/components/{feature}/FeatureMain.tsx
  - IMPLEMENT: Interactive logic component (Client Component)
  - PATTERN: Handle state and optimistic updates (React 19)
  - IMPORTS: Lucide-react icons for UI status
  - PLACEMENT: Feature logic in src/frontend/components/{feature}/

Task 4: CREATE src/frontend/app/{route}/page.tsx
  - IMPLEMENT: Next.js 15 Server Component Page
  - ACTION: Perform data fetching using Server Actions or fetch()
  - NAMING: Default export with Metadata export
  - PLACEMENT: Route entry in src/frontend/app/{route}/

Task 5: CREATE src/frontend/__tests__/{feature}.test.tsx
  - IMPLEMENT: React Testing Library tests for component rendering and events
  - FOLLOW pattern: src/frontend/__tests__/existing.test.tsx
  - COVERAGE: Test happy path and error states (Zod validation failure)
Implementation Patterns & Key Details
TypeScript

// Example: Next.js 15 Server Component Data Fetching
// PATTERN: Async page params and server-side fetching
export default async function Page({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params;
  const data = await fetchData(id);

  return <FeatureMain initialData={data} />;
}

// Example: React 19 Client Component with Optimistic UI
// PATTERN: 'use client' only for interactive islands
"use client"
export function FeatureMain({ initialData }: Props) {
  // GOTCHA: Use 'useActionState' or 'useOptimistic' for better UX
}
Integration Points
YAML

CONFIG:
  - add to: .env.local
  - pattern: "NEXT_PUBLIC_* for variables accessible in client components"

ROUTES:
  - file structure: src/frontend/app/feature-name/page.tsx
  - navigation: Update src/frontend/components/layout/Navigation.tsx

STYLES:
  - config: tailwind.config.ts (if adding custom colors/themes)
Validation Loop
Level 1: Syntax & Style (Immediate Feedback)
Bash

# Run after each file creation - fix before proceeding
npm run lint                     # ESLint checks with Next.js/React rules
npx tsc --noEmit                # Full TypeScript type checking
prettier --check src/frontend    # Formatting validation

# Expected: Zero errors. READ output and fix before proceeding.
Level 2: Unit & Component Tests
Bash

# Test each component as it's created
npm test -- src/frontend/components/{feature}

# Full test suite for affected areas
npm test -- src/frontend/__tests__/{feature}.test.tsx

# Expected: All tests pass. If failing, debug implementation or Zod schema.
Level 3: Integration Testing (System Validation)
Bash

# Development server validation
npm run dev &
sleep 5 # Allow Next.js 15 startup time

# Page load validation (Health Check)
curl -I http://localhost:3000/{feature-route}
# Expected: 200 OK

# Hydration & Responsive Check
# Manual: Verify no hydration mismatches in browser console
# Manual: Verify Tailwind layout at 375px, 768px, and 1440px

# Production Build Check
npm run build
# Expected: Successful build with no TypeScript warnings
Level 4: Creative & Domain-Specific Validation
Bash

# A11y & Performance Audits:
# Run Axe-core or Lighthouse for accessibility compliance
# Verify ARIA labels on interactive elements

# Security Audit:
# Verify sensitive API keys are NOT exposed in client components
# Check that all environment variables use the proper NEXT_PUBLIC_ prefixing

# Bundle Analysis:
# npm run analyze (if @next/bundle-analyzer is installed)
Final Validation Checklist
Technical Validation
[ ] All 4 validation levels completed successfully

[ ] No type errors: npx tsc --noEmit

[ ] No linting errors: npm run lint

[ ] Production build succeeds: npm run build

Feature Validation
[ ] All success criteria from "What" section met

[ ] Manual testing successful: [List specific routes tested]

[ ] User persona requirements satisfied (e.g., Mobile responsive)

Code Quality & Standards
[ ] Proper Server/Client component split followed

[ ] No hydration mismatches between server and client

[ ] No 'any' types used; strict interfaces for all props

Anti-Patterns to Avoid
❌ Don't use 'any' types; define strict Interfaces for all props.

❌ Don't use 'use client' unnecessarily; embrace Server Components for performance.

❌ Don't put business logic or heavy data fetching inside Presentation components.

❌ Don't use legacy 'pages' router patterns; use the App Router standard.

❌ Don't hardcode values that should be in the .env or config.