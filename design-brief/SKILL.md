---
name: design-brief
description: Create a design brief through an interactive interview, codebase exploration, and experience design decisions. Saved as a markdown file in the project. Use when user wants to write a design brief, plan a new feature or page, define a UI direction, or mentions "brief".
---

This skill creates a design brief through structured conversation. You may skip steps if they are not necessary.

## Example prompts

- "Write a brief for the onboarding flow"
- "I need to plan a settings page before I start building"
- "Help me define the direction for a marketing landing page"
- "Brief this: a dashboard that shows project health metrics"

## Process

1. Ask the user for a detailed description of what they want to build, who it is for, and any constraints or ideas they already have.

2. Explore the existing codebase to understand the current state. Scan for each of the following specifically:
   - **CSS variables / tokens**: files named `tokens.css`, `variables.css`, `theme.css`, or `:root` declarations with custom properties
   - **Tailwind config**: `tailwind.config.js` or `tailwind.config.ts`, check `theme.extend` for custom values
   - **UI framework themes**: Material UI `createTheme`, Chakra `extendTheme`, shadcn `globals.css` and `components.json`
   - **Component directories**: `components/`, `ui/`, `shared/`, or any folder containing reusable UI pieces
   - **Storybook**: `.storybook/` directory or `*.stories.*` files indicating a documented component library
   - **Design token files**: JSON token files (Style Dictionary format, Figma token exports)
   - **Package.json UI dependencies**: tailwindcss, @mui/material, @chakra-ui/react, @radix-ui, lucide-react, framer-motion, etc.
   - **Font loading**: Google Fonts links in HTML, `@font-face` declarations, font imports in CSS/config
   - **Existing pages/layouts**: route files, layout components, page templates that show established patterns
   - If components exist, treat them as the starting vocabulary. The brief should extend, not replace.

3. Interview the user relentlessly about every aspect of the design until you reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one by one. For each question, provide your recommended answer.

   Cover at minimum:
   - Who is the primary user their JTBD and what are they trying to accomplish?
   - What does success look like for this interface?
   - What is the emotional tone? (calm, urgent, playful, authoritative, warm, clinical)
   - What existing products, sites, or styles should this feel like? What should it NOT feel like?
   - What are the hard constraints? (devices, accessibility requirements, performance budgets, brand guidelines)
   - What content will this interface contain? What is placeholder vs. real?

4. Once you have a complete understanding, write the brief using the template below.

## File Output

Save the brief to `.design/<feature-slug>/DESIGN_BRIEF.md` where `<feature-slug>` is a short, lowercase, hyphenated name derived from the feature or page being designed (e.g., `onboarding-flow`, `settings-page`, `project-dashboard`).

This folder structure ensures that running the design flow multiple times for different features does not overwrite previous work. All subsequent skills (information-architecture, design-tokens, brief-to-tasks, design-review) will read from and write to this same subfolder.

Example:

```
.design/
├── onboarding-flow/
│   └── DESIGN_BRIEF.md
└── settings-page/
    └── DESIGN_BRIEF.md
```

## Brief Template

```markdown
# Design Brief: [Feature/Page Name]

## Problem

What problem is the user facing, described from their perspective. Not technical. Not business metrics. The human friction.

## Solution

What this interface does to solve that problem, described as an experience, not a feature list.

## Experience Principles

Three principles maximum that guide every design decision. Each principle should resolve a tension.
Example: "Progressive disclosure over upfront complexity" or "Confidence over speed."

1. [Principle] -- [What this means in practice]
2. [Principle] -- [What this means in practice]
3. [Principle] -- [What this means in practice]

## Aesthetic Direction

- **Philosophy**: [Named philosophy or described vibe. See /frontend-design skill for reference.]
- **Tone**: [Emotional register]
- **Reference points**: [Existing products, sites, or styles this should feel like]
- **Anti-references**: [What this should NOT feel like]

## Existing Patterns

Components, tokens, and conventions already in the codebase that this design must respect or extend.

- Typography: [what is currently used]
- Colors: [current palette/variables]
- Spacing: [current scale]
- Components: [existing components that will be reused or extended]

## Component Inventory

A list of the UI components this feature requires. For each, note whether it exists already, needs modification, or is new.

| Component | Status                | Notes    |
| --------- | --------------------- | -------- |
| [name]    | Exists / Modify / New | [detail] |

## Key Interactions

The critical interaction patterns. Describe what the user does and what the interface does in response. Focus on state changes, transitions, and feedback.

## Responsive Behavior

How the layout adapts across breakpoints. Note any components that change behavior (not just size) on mobile.

## Accessibility Requirements

Minimum requirements for this interface. Include contrast ratios, keyboard navigation, screen reader considerations, and focus management.

## Out of Scope

Things this brief explicitly does not cover. Be specific. This prevents scope creep during build.
```
