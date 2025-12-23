# Tailwind CSS Design System & UI Consistency

> This document defines the mandatory visual standards for the Antigravity App Factory. All UI components must adhere to these tokens to ensure a professional, revenue-ready aesthetic.

## 1. Core Token Strategy
* **Configuration First**: All custom colors, spacing, and font scales MUST be defined in `tailwind.config.ts`.
* **No Magic Values**: Forbidden to use arbitrary values (e.g., `h-[123px]`) unless explicitly required by a specific third-party integration.
* **Semantic Naming**: Use semantic color names (e.g., `primary`, `secondary`, `accent`, `destructive`) rather than literal colors (e.g., `blue-600`) to support future white-labeling or theme switching.

## 2. Layout & Spacing Standards
* **Grid & Flex**: Use Tailwind's Grid for page-level layouts and Flexbox for component-level alignment.
* **Responsive Breakpoints**: Standard breakpoints are `sm` (640px), `md` (768px), `lg` (1024px), and `xl` (1280px). All components must be validated at these widths.
* **Containerization**: Main content must be wrapped in a `container` class with standardized horizontal padding for consistent edge alignment.

## 3. Interaction & Iconography
* **Lucide Icons**: Use `lucide-react` for all icons. Proactively check for appropriate sizing (default `w-5 h-5`) and stroke width.
* **States**: Implement `hover:`, `focus-visible:`, and `active:` states for all interactive elements to ensure accessibility and feedback.
* **Transitions**: Use `transition-colors` or `transition-all` with a standard `duration-200` for smooth UI interactions.

## 4. Documentation & Context Links
* **Tailwind Configuration**: https://tailwindcss.com/docs/configuration
* **Theme Customization**: https://tailwindcss.com/docs/theme
* **Lucide React Icons**: https://lucide.dev/guide/packages/lucide-react

## 5. Anti-Patterns
* ❌ **Inline Style Objects**: Never use the `style={{}}` prop for layout or colors. Use Tailwind classes exclusively.
* ❌ **Vague Class Names**: Avoid complex utility strings in a single line. Use the `cn()` utility (from `clsx` and `tailwind-merge`) to conditionally join classes.
* ❌ **Hardcoded Hex Codes**: All colors must be mapped to the Tailwind theme.