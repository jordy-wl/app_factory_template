To ensure your Antigravity App Factory can validate ideas at high velocity without polluting your production code, we have merged the exhaustive "concept validation" framework of the reference repository with your specific Next.js 15 and React 19 stack.

This high-fidelity version of prp_poc_react.md is designed to be a "Sandbox Contract." It explicitly defines what the AI should not build (Won't Have) and how to manage Mock Data effectively, ensuring that "working over excellent" becomes a repeatable process.

Master Template 4: PRPs/templates/prp_poc_react.md
File Path: .claude/templates/prp_poc_react.md

Markdown

# React POC Template v1 - Rapid Prototype Development

## 🧪 Goal
**POC Goal**: [Specific concept to validate - e.g., "AI-driven Drag-and-Drop Kanban"]
**Deliverable**: [Concrete artifact - e.g., "Isolated route /poc/kanban with state-sync demo"]
**Success Definition**: [How you'll know the concept is validated - e.g., "Stakeholders can navigate core workflow with realistic data"]

## 🛠️ POC Scope & Constraints
**Fidelity Level**: [Demo (Stakeholder Presentation) / MVP (User Testing)]

**Must Have**: [Core functionality that proves the concept]
- [ ] [Primary user interaction works end-to-end]
- [ ] [Key data displays correctly with mock data]
- [ ] [Critical user flow is navigable]

**Nice to Have**: [Features that enhance but aren't critical]
- [ ] [Secondary interactions / Mobile responsiveness / Visual polish]

**Won't Have (Explicitly Excluded)**: 
- ❌ **Real API/Supabase integration**: Use mock data exclusively to save time.
- ❌ **Complex Error Handling**: Focus on the "Happy Path".
- ❌ **Performance Optimization**: Use raw Tailwind; avoid complex refactors.
- ❌ **Comprehensive Testing**: Use basic smoke tests only.

## 💡 Why
- **Concept Validation Need**: [What hypothesis are you testing?]
- **UX Question**: [What interaction assumption needs validation?]
- **Technical Feasibility**: [What specific library or logic needs proving?]
- **Business Value**: [How does this POC drive decision making?]

## 🗺️ What (The Journey)
**Primary User Journey**:
1. [User action/page load] -> 2. [User interaction with data/UI] -> 3. [Outcome/completion state]

**Key Interactions**:
- [Interaction type]: [Expected behavior with mock data]
- [UI element]: [User feedback/system response]

**Visual Requirements**:
- [Layout/component requirements - e.g., "Three-column grid with Lucide icons"]

## 📑 All Needed Context (POC-Optimized)

### Context Completeness Check
_Before starting: "Does this context enable building a working prototype that validates the core concept in <4 hours?"_

### React Technology Stack
```yaml
# Current Tech Stack Requirements
framework: [Next.js 15 / React 19]
styling: [Tailwind CSS]
components: [shadcn/ui / Lucide Icons]
typescript: [Strict mode / Zod validation]

# POC-Specific Choices
mock_data: [MSW / Static JSON / faker.js]
state_management: [useState / useActionState / useOptimistic]
routing: [Next.js 15 App Router]
Mock Data Strategy
YAML

strategy: [e.g., Static JSON files / Hardcoded objects]
entities: [List key data models - e.g., User, Order, AgentResponse]
realistic_data: [e.g., "Use faker.js for realistic names and timestamps"]
🏗️ Implementation Blueprint
POC Architecture (Isolated)
Bash

# All POC files MUST stay in this isolated directory:
src/frontend/app/poc-{name}/
├── components/          # Feature-specific UI
├── data/               # Mocks and local schemas
├── hooks/              # usePocState.ts (Optimistic hooks)
└── page.tsx            # Main Entry Point
Implementation Tasks (Surgical Format)
YAML

Task 1: CREATE src/frontend/app/poc-{name}/ foundation
  - ACTION: Setup directory structure and local Zod schemas for mock data.
  - VALIDATE: `npx tsc --noEmit` on the new folder.

Task 2: CREATE src/frontend/app/poc-{name}/data/mocks.ts
  - ACTION: Implement realistic mock data objects using the defined schemas.
  - VALIDATE: `node src/frontend/app/poc-{name}/data/mocks.ts` (if testable).

Task 3: CREATE src/frontend/app/poc-{name}/components/
  - ACTION: Implement core UI elements using Tailwind and shadcn.
  - GOTCHA: Skip complex accessibility audits; focus on visual hierarchy.

Task 4: CREATE src/frontend/app/poc-{name}/page.tsx
  - ACTION: Implement main entry point; connect components to mock data.
  - VALIDATE: `npm run dev` and manual visual check of the "Happy Path".
🧪 Validation Loop (POC Grade)
Level 1: Syntax & Build
npm run lint / npx tsc --noEmit

Expected: No TypeScript errors in the POC directory.

Level 2: Demo Validation (User Experience)
Check: Primary user flow is navigable end-to-end?

Check: Key interactions work with mock data (e.g., clicking 'Submit' shows a mock result)?

Check: UI renders correctly on Desktop (1440px)?

Level 3: Concept Validation (Stakeholder Readiness)
Check: Demo script prepared with talking points?

Check: Known limitations documented (e.g., "This button is just a visual placeholder")?

🚫 POC Anti-Patterns
❌ Don't over-engineer: Skip complex architecture patterns (e.g., Context API) for simple state.

❌ Don't build for scalability: This is a single-user, demo-focused "island."

❌ Don't implement edge cases: If a user enters invalid data, the POC can simply crash or show a static alert.

❌ Don't present as production-ready: Ensure the UI includes a "POC / Concept Only" badge if needed.

✅ Final Validation Checklist
[ ] TypeScript: All mock data and props properly typed.

[ ] Visual Clarity: UI effectively communicates the core concept.

[ ] Fast Iteration: Development completed within the defined timebox.

[ ] Parallel Safe: Directory is isolated; no impact on production src/ files.