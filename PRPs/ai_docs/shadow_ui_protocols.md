# Law Book: shadcn/ui Component Protocols & Extension Standards

> This document defines the mandatory protocols for utilizing and extending the shadcn/ui component library. All agents must follow these rules to ensure component accessibility, modularity, and high-fidelity styling.

## 1. Core Architecture (The Registry)
* **Installation Protocol**: All components MUST be initialized using the `npx shadcn@latest add` command to ensure the latest accessible primitives (Radix UI) are used.
* **Local Ownership**: Once a component is added to `src/frontend/components/ui/`, it is considered local code. Agents MUST NOT overwrite these files unless explicitly performing a library-wide upgrade.
* **Registry Compliance**: The `components.json` file at the root is the source of truth for component aliases and path configurations.

## 2. Extension & Customization Standards
* **CVA for Variants**: Use `class-variance-authority` (cva) for all component variations. Logic for variants (size, color, state) MUST be kept at the top of the component file.
* **Prop Forwarding**: All interactive components MUST utilize `React.forwardRef` to ensure proper integration with third-party libraries like `react-hook-form` and `framer-motion`.
* **Tailwind Composition**: Use the `cn()` utility utility (combining `clsx` and `tailwind-merge`) for all class merging to prevent CSS specificity conflicts.

## 3. Accessibility & UX Mandates
* **Radix Primitives**: Never bypass the underlying Radix UI primitives. If a component requires custom logic (e.g., a specific modal behavior), extend the Radix primitive instead of building from scratch.
* **ARIA & Roles**: Proactively ensure every component includes appropriate `aria-` labels and `role` attributes, especially when modifying default shadcn templates.
* **Keyboard Navigation**: Components MUST maintain full keyboard navigability as provided by the Radix base.

## 4. Documentation & Context Links
* **shadcn/ui Documentation**: https://ui.shadcn.com/docs
* **Radix UI Primitives**: https://www.radix-ui.com/primitives
* **CVA Documentation**: https://cva.style/docs

## 5. Anti-Patterns
* ❌ **Component Bloat**: Do not add business logic (API calls) directly into UI components. Keep them as "Presentational" islands.
* ❌ **Manual Refactoring**: Avoid manual CSS file creation. All styling must be handled via Tailwind classes within the component file.
* ❌ **Shadowing Primitives**: Never hide Radix UI accessibility warnings. If a warning appears in the console, it is a blocking failure.