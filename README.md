# Designer Skills for Claude Code & Cursor

A collection of agent skills for designers who prototype and build with AI coding tools. These skills encode design process so AI follows a structured path instead of producing random output.

## The Flow

The skills follow a deliberate sequence. You can use any skill individually, or run **`/design-flow`** to be guided through the entire sequence automatically.

```mermaid
flowchart LR
    DF(["/design-flow — orchestrates the full sequence"])
    DF -.->|runs| GM
    GM[grill-me] --> DB[design-brief] --> IA[information-architecture] --> DT[design-tokens] --> BT[brief-to-tasks] --> FE[frontend-design] --> DR[design-review]
    DR -->|iterate| GM
```

0. **`/design-flow`** -- Run the full workflow as a guided sequence. Orchestrates all skills in order, lets you skip phases, confirms between each step. Start here if you want the complete process.
1. **`/grill-me`** -- Get interrogated about your plan until every design decision is resolved.
2. **`/design-brief`** -- Turn the grilling session into a structured design brief. Includes codebase exploration so the AI respects what already exists.
3. **`/information-architecture`** -- Define the structural skeleton: navigation, content hierarchy, page structure, URL patterns, user flows.
4. **`/design-tokens`** -- Generate a complete token system (colors, spacing, typography, motion) with light and dark mode palettes, based on the chosen aesthetic philosophy.
5. **`/brief-to-tasks`** -- Break the brief into an ordered checklist of independently buildable vertical slices.
6. **`/frontend-design`** -- Build with a named aesthetic philosophy. Mobile-first. Dark mode included. 8 design philosophies with concrete implementation parameters.
7. **`/design-review`** -- Run a structured critique against the brief. Supports code review and screenshot-based review. Checks hierarchy, consistency, responsiveness, accessibility, dark mode, and aesthetic fidelity.

## Key Principles

### Respect Existing Code

Every skill that touches the codebase includes a detailed detection checklist: CSS variables, Tailwind config, UI framework themes, component directories, Storybook stories, token files, font loading, and package.json dependencies. This prevents the AI from generating a new button when one exists, or inventing a color that clashes with the established palette.

### Mobile-First

The `/frontend-design` skill mandates building mobile layout first (375px), then scaling up with `min-width` media queries. Touch targets, text sizing, and navigation patterns are all specified for mobile.

### Dark Mode by Default

The `/design-tokens` skill generates both light and dark palettes. The `/frontend-design` skill builds with CSS custom properties that support both `prefers-color-scheme` and manual toggle. The `/design-review` skill checks that dark mode is implemented correctly.

### You Don't Need to Name a Style

The aesthetic philosophies in `/frontend-design` are a menu, not a requirement. If you name one ("build this in a Dieter Rams style"), the AI follows those parameters. If you describe a vibe ("warm and clean"), it maps to the closest philosophy. If you say nothing, it picks one based on context and tells you which it chose.

## Installation

### One command (recommended)

Install all eight skills at once using the [Vercel skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add julianoczkowski/designer-skills --all
```

This works with Claude Code, Cursor, Codex, Windsurf, and 40+ other agents.

### Install a single skill

```bash
npx skills add julianoczkowski/designer-skills --skill design-flow
npx skills add julianoczkowski/designer-skills --skill grill-me
npx skills add julianoczkowski/designer-skills --skill design-brief
npx skills add julianoczkowski/designer-skills --skill information-architecture
npx skills add julianoczkowski/designer-skills --skill design-tokens
npx skills add julianoczkowski/designer-skills --skill brief-to-tasks
npx skills add julianoczkowski/designer-skills --skill frontend-design
npx skills add julianoczkowski/designer-skills --skill design-review
```

### Install to a specific agent

```bash
npx skills add julianoczkowski/designer-skills --all -a claude-code
npx skills add julianoczkowski/designer-skills --all -a cursor
```

### Manual installation

Copy the skill folders into your project's `.claude/skills/` directory (Claude Code) or equivalent configuration for your tool.

```
your-project/
├── .claude/
│   └── skills/
│       ├── design-flow/
│       │   └── SKILL.md
│       ├── grill-me/
│       │   └── SKILL.md
│       ├── design-brief/
│       │   └── SKILL.md
│       ├── information-architecture/
│       │   └── SKILL.md
│       ├── design-tokens/
│       │   └── SKILL.md
│       ├── brief-to-tasks/
│       │   └── SKILL.md
│       ├── frontend-design/
│       │   └── SKILL.md
│       └── design-review/
│           └── SKILL.md
```

### Project vs Global Install

By default, `npx skills add` installs to the **current project directory**. This means the skills live inside your project and only apply when you're working in that folder. The CLI puts them in the right place automatically: `.claude/skills/` for Claude Code, `.cursor/skills/` for Cursor, and the equivalent for other agents. Works on Mac, Windows, and Linux.

```bash
# Project-level (default) — run this from inside your project folder
npx skills add julianoczkowski/designer-skills --all

# Global/user-level — available in every project on your machine
npx skills add julianoczkowski/designer-skills --all -g
```

**For teams:** project-level install is the better choice. If you commit the `.claude/skills/` folder to git, every collaborator gets the same skills automatically. Install once, push, and the whole team benefits. No individual setup required.

## Aesthetic Philosophies (in `/frontend-design`)

The frontend-design skill includes concrete implementation parameters for 8 named design philosophies:

- **Dieter Rams** -- Less but better. Functional. No decoration without purpose.
- **Swiss / International Typographic** -- Grid-locked. Strong type hierarchy. Objective.
- **Japanese Minimalism (Ma)** -- Negative space is content. Quiet. Restrained.
- **Brutalist** -- Raw structure visible. Anti-polish. Content-first.
- **Scandinavian** -- Warmth plus restraint. Rounded. Accessible by default.
- **Art Deco** -- Geometric luxury. Bold symmetry. Statement typography.
- **Neo-Memphis** -- Playful chaos. Clashing color. Anti-corporate.
- **Editorial / Magazine** -- Content-led. Display typography. Print-inspired.

Each philosophy defines specific parameters for typography (font families, scale, spacing), color (palette approach, accent strategy), layout (grid type, composition rules), spacing (base unit, density), motion (duration, easing, what to animate), and detail treatment (borders, shadows, texture).

## Credits

- Grill-me concept by [Matt Pocock](https://github.com/mattpocock/skills)
- Design tree concept from _The Design of Design_ by Frederick P. Brooks Jr.
- Adapted for designers by [Julian Oczkowski](https://youtube.com/@aiforwork_app)
