---
name: design-flow
description: Run the full design-to-build workflow as a guided sequence. Orchestrates all designer skills in order, from grilling through review. Use when user wants to go through the complete design process, start a project from scratch, run the full flow, or mentions "design flow" or "full workflow".
---

This skill orchestrates the full designer workflow by running each skill in sequence. You are a guide walking the designer through each phase. Do not rush. Each phase must be completed and confirmed before moving to the next.

## Example prompts

- "Run the full design flow"
- "Walk me through the complete process for a new project"
- "Start from scratch and take me through everything"
- "Design flow for a dashboard app"

## The Sequence

```
1. Grill Me          → Clarify thinking
2. Design Brief      → Document intent
3. Info Architecture  → Define structure
4. Design Tokens     → Establish visual system
5. Brief to Tasks    → Plan the build
6. Frontend Design   → Build it
—
7. Design Review     → Run separately when ready
```

## Rules

1. **At the start**, tell the designer what the full sequence looks like (phases 1-6, with review available separately) and ask if they want to skip any phases. Common skip patterns:
   - Already have a clear idea → skip grill-me
   - Single component, not a full page → skip information-architecture
   - Existing project with tokens → skip design-tokens

2. **Before each phase**, announce which phase you are entering and what it will produce. Example: "Phase 2: Design Brief. I'll interview you about the project and produce a DESIGN_BRIEF.md file. Ready?"

3. **During each phase**, read the corresponding SKILL.md file and follow its full instructions. Do not summarize or abbreviate the skill. Run it properly.

4. **After each phase**, summarize what was produced (the file name, the key decisions, any open questions) and ask: "Ready to move to the next phase?" Wait for confirmation.

5. **Between phases**, check if the output from the previous phase changes anything about the next phase. For example, if the brief names a philosophy, mention that the tokens phase will use it.

6. **The designer can stop at any point.** If they say "that's enough for now," summarize where they are in the sequence and what the next phase would be when they return.

## Phase Details

### Phase 1: Grill Me

Read the `grill-me` skill (grill-me/SKILL.md) and follow its instructions.
**Produces**: Shared understanding of the project. No file output.
**Transition**: "We've resolved the key decisions. Ready to capture this as a design brief?"

### Phase 2: Design Brief

Read the `design-brief` skill (design-brief/SKILL.md) and follow its instructions.
**Produces**: `.design/<feature-slug>/DESIGN_BRIEF.md`.
**Transition**: "The brief is saved. Next is information architecture, where we'll define the page structure and navigation. Skip this if you're building a single component. Continue?"

### Phase 3: Information Architecture

Read the `information-architecture` skill (information-architecture/SKILL.md) and follow its instructions.
**Produces**: `.design/<feature-slug>/INFORMATION_ARCHITECTURE.md`.
**Transition**: "IA is defined. Next we'll generate design tokens (colors, spacing, typography) based on the philosophy from the brief. Continue?"

### Phase 4: Design Tokens

Read the `design-tokens` skill (design-tokens/SKILL.md) and follow its instructions.
**Produces**: Token file (CSS variables, Tailwind config, or theme file depending on stack).
**Transition**: "Tokens are set. Next I'll break the brief into a task list so we can build in order. Continue?"

### Phase 5: Brief to Tasks

Read the `brief-to-tasks` skill (brief-to-tasks/SKILL.md) and follow its instructions.
**Produces**: `.design/<feature-slug>/TASKS.md`.
**Transition**: "Tasks are ready. Now we build. I'll start with the first task on the list. Continue?"

### Phase 6: Frontend Design

Read the `frontend-design` skill (frontend-design/SKILL.md) and follow its instructions.
Work through the tasks from `TASKS.md` in order. After completing each task, check it off and confirm with the designer before moving to the next task.
**Produces**: Built components and pages.
**Transition**: "The flow is complete. Your brief, IA, tokens, and tasks are all saved in the project. When you're ready for a design review, run `/design-review` and I'll critique the build against the brief."

**The flow ends here.** Phase 7 is not automatic.

### Phase 7: Design Review (on request only)

This phase does NOT run automatically. It only runs if:

- The designer explicitly asks for a review during the flow
- The designer runs `/design-review` separately after building

The review requires built code to examine. If no components or pages have been built yet, do not run this phase. Instead, remind the designer: "Run `/design-review` once you have something built. It will check the output against the brief."

When triggered, read the `design-review` skill (design-review/SKILL.md) and follow its instructions. The review will capture screenshots of the running application using Playwright MCP (preferred), the Cursor IDE Browser (fallback), or by asking the user to provide them manually if no browser tool is available.

**Produces**: `.design/<feature-slug>/DESIGN_REVIEW.md` + screenshots saved in `.design/<feature-slug>/screenshots/`.
**Transition**: "Review is done. Screenshots are saved in `.design/<feature-slug>/screenshots/`. If there are must-fix items, I can address them now."

## Project Files Structure

All design flow artifacts are saved under `.design/<feature-slug>/` where `<feature-slug>` is a short, lowercase, hyphenated name derived from the feature being designed. This ensures multiple features can be designed independently without overwriting each other.

```
.design/
└── <feature-slug>/
    ├── DESIGN_BRIEF.md              ← Phase 2: Project intent, goals, aesthetic direction
    ├── INFORMATION_ARCHITECTURE.md  ← Phase 3: Navigation, page structure, user flows
    ├── DESIGN_TOKENS.*              ← Phase 4: Colors, spacing, typography, shadows (CSS/Tailwind/theme)
    ├── TASKS.md                     ← Phase 5: Ordered build checklist from the brief
    ├── DESIGN_REVIEW.md             ← Phase 7: Prioritized critique against the brief
    └── screenshots/                 ← Phase 7: Visual evidence from the running app
        ├── review-[page]-desktop-1280.png
        ├── review-[page]-tablet-768.png
        ├── review-[page]-mobile-375.png
        ├── review-[page]-dark-mode-*.png
        └── review-[component]-[state].png
```

The `screenshots/` subfolder is created during the design review phase. All visual evidence of the review (responsive breakpoints, interactive states, dark mode) is saved here with descriptive filenames so findings in `DESIGN_REVIEW.md` are traceable.

## If the Designer Returns Mid-Flow

Check the `.design/` folder for existing feature subfolders. If files from earlier phases exist (DESIGN_BRIEF.md, INFORMATION_ARCHITECTURE.md, TASKS.md) inside a feature folder, read them to understand where the designer left off. Ask which feature to resume if multiple folders exist. Resume from the next incomplete phase.
