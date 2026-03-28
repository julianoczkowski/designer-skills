---
name: information-architecture
description: Define the structural layer of a product or site before visual design begins. Covers navigation, content hierarchy, page structure, URL patterns, and user flows. Use when user wants to plan site structure, define navigation, map user flows, organize content, or mentions "IA" or "information architecture".
---

This skill defines the structural skeleton of a product or site. It sits between the design brief and the build. Run this after the brief is written and before tasks are created.

## Example prompts

- "Plan the IA for this app before I start building"
- "Map out the navigation and page structure"
- "I need to organize the content for a documentation site"
- "Define user flows for the onboarding experience"

## Process

1. Look for an existing design brief at `.design/*/DESIGN_BRIEF.md`. If multiple subfolders exist, use the most recently modified one, or ask the user which feature they are working on. If no brief exists, ask the user what they are building and for whom.

2. Explore the existing codebase to understand what structure already exists:
   - **Routing**: Next.js `app/` or `pages/` directory, React Router config, Vue Router, SvelteKit routes, or static HTML page files
   - **Navigation components**: header, sidebar, navbar, breadcrumb, footer components
   - **Layout components**: root layouts, nested layouts, page wrappers, container components
   - **Page directories**: how pages are currently organized in the file system
   - **URL patterns**: existing slugs, dynamic segments, query parameter conventions
   - **CMS or data layer**: content models, API routes, data fetching patterns, MDX/content directories
   - If structure exists, this skill extends and improves it. Do not propose a new architecture that ignores what is already built.

3. Interview the user about structural decisions. For each question, provide your recommended answer.

   Cover at minimum:
   - What are the primary things a user needs to find or do? Rank by frequency.
   - How many levels of navigation depth are acceptable?
   - What content will grow over time vs. what is fixed?
   - Are there distinct user types who need different entry points?
   - What is the one page/view where the user spends 80% of their time?

4. Once you have a shared understanding, produce the IA document using the template below and save it as `INFORMATION_ARCHITECTURE.md` in the same `.design/<feature-slug>/` subfolder as the design brief.

## IA Document Template

```markdown
# Information Architecture: [Product/Site Name]

## Site Map

A hierarchical map of every page or view. Use indentation to show nesting. Include the URL pattern for each.

- Home `/`
  - Feature A `/feature-a`
    - Sub-page `/feature-a/detail`
  - Feature B `/feature-b`
- Settings `/settings`
  - Profile `/settings/profile`

## Navigation Model

Describe the navigation system:
- **Primary navigation**: What appears in the main nav? Maximum items.
- **Secondary navigation**: Sidebar, tabs, or contextual links within sections.
- **Utility navigation**: Account, settings, help, and anything outside the main content hierarchy.
- **Mobile navigation**: How navigation adapts. Hamburger, bottom tabs, or something else.

## Content Hierarchy

For each major page or view, define the content priority:

### [Page Name]
1. [Highest priority content] -- Why this comes first
2. [Second priority] -- Why this comes second
3. [Third priority] -- Rationale
4. [Below the fold / secondary]

## User Flows

The critical paths through the product. Each flow is a sequence of steps with decision points noted.

### [Flow Name] (e.g., "New user onboarding" or "Create a project")
1. User lands on [page]
2. User sees [content/prompt]
3. User takes action: [action]
   - If [condition A] -> [outcome]
   - If [condition B] -> [outcome]
4. User arrives at [destination]

## Naming Conventions

A glossary of terms used in the interface. Consistency matters. Pick one word and use it everywhere.

| Concept | Label in UI | Notes |
|---------|-------------|-------|
| [thing] | [what we call it] | [why this word] |

## Component Reuse Map

Which structural components (layouts, containers, navigation elements) are shared across pages.

| Component | Used on | Behavior differences |
|-----------|---------|---------------------|
| [layout/component] | [pages] | [any variations] |

## Content Growth Plan

Which sections of the site will accumulate content over time and how the IA accommodates that growth (pagination, filtering, search, archive patterns).

## URL Strategy

Rules for URL construction:
- Pattern: [e.g., `/section/subsection/item-slug`]
- Dynamic segments: [what is parameterized]
- Query parameters: [filtering, sorting, pagination]
```
