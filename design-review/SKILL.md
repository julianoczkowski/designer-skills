---
name: design-review
description: Run a structured design critique against the brief and codebase. Checks visual hierarchy, consistency, responsiveness, accessibility, and aesthetic fidelity. Use when user wants a design review, critique, QA pass, polish pass, or mentions "review" after building.
---

This skill runs a structured design review of what has been built, measured against the design brief and the chosen aesthetic philosophy.

> **CRITICAL — Visual Screenshot Capture**
>
> You MUST capture screenshots of the running application as part of every design review. Code review alone is insufficient — you need to see what the user sees. Follow the screenshot capture protocol in Step 3 below. This is not optional.

## Example prompts

- "Review what I just built"
- "Run a design critique on the landing page"
- "Check this against the brief"
- "Here's a screenshot. How does it look?" [paste screenshot]
- "QA pass before I ship this"

## Process

1. **Read the brief.** Look for the active feature's brief at `.design/<feature-slug>/DESIGN_BRIEF.md`. If multiple feature folders exist under `.design/`, ask the user which feature to review. If no `.design/` folder exists, fall back to `DESIGN_BRIEF.md` in the project root. If neither exists, ask the user what the intended design direction was.

2. **Explore the built code.** Examine every component, page, and style file that was created or modified. Scan specifically for:
   - All new or modified components and their relationship to pre-existing components
   - Token/variable usage: are components using shared tokens or hardcoding values?
   - Duplicate components that should be consolidated
   - File naming and organization: do new files follow the project's conventions?
   - Understand what was actually built, not what was planned.

3. **Capture screenshots of the running application.**

   This step is **mandatory**. Do not skip it. Do not rely only on user-provided screenshots.

   ### Screenshot Tool Priority

   Try each option in order. Use the first one that is available:
   1. **Playwright MCP (preferred).** Check if the `plugin-playwright-playwright` MCP server is available. If it is, use it — it gives you precise control over viewport sizing, full-page captures, and file naming.
   2. **Cursor IDE Browser (second choice).** If Playwright MCP is not available, use the `cursor-ide-browser` MCP server's `browser_take_screenshot` tool instead. It has the same core capabilities.
   3. **Ask the user (last resort).** If neither MCP server nor in-app browser is available, you MUST ask the user to provide screenshots manually. Be specific about what you need:
      - "I don't have access to a browser tool. To complete the visual review I need screenshots of the running application. Please provide:"
      - A full-page screenshot at **desktop** width (1280px)
      - A full-page screenshot at **tablet** width (768px)
      - A full-page screenshot at **mobile** width (375px)
      - Dark mode variants (if applicable)
      - Any specific component or interactive state you want reviewed
      - Ask the user to paste/attach the images directly in chat, or to save them into the `screenshots/` folder themselves.
      - **Do not skip the visual review.** Wait for the user to provide screenshots before proceeding with the checklist.

   ### Screenshot Save Location

   All screenshots MUST be saved to a `screenshots/` subfolder inside the feature's `.design/` directory — the same folder where `DESIGN_BRIEF.md` and other design flow files live.

   Path pattern: `.design/<feature-slug>/screenshots/`

   If the brief lives at `.design/onboarding-flow/DESIGN_BRIEF.md`, screenshots go to `.design/onboarding-flow/screenshots/`. Create the folder if it does not exist.

   If no `.design/` folder exists (legacy project or standalone review), fall back to a `screenshots/` folder in the project root.

   Use descriptive filenames that encode what was captured:

   ```
   .design/
   └── onboarding-flow/
       ├── DESIGN_BRIEF.md
       ├── DESIGN_REVIEW.md
       └── screenshots/
           ├── review-homepage-desktop-1280.png
           ├── review-homepage-tablet-768.png
           ├── review-homepage-mobile-375.png
           ├── review-homepage-dark-mode-desktop-1280.png
           └── review-card-component-hover.png
   ```

   ### Screenshot Capture Protocol

   **a. Navigate to the application.** Ask the user for the URL if not obvious from the project (e.g., `http://localhost:3000`). Use `browser_navigate` to open it.

   **b. Capture responsive breakpoints.** At minimum, capture these three viewports for every key page/view:

   | Breakpoint | Width × Height | Filename suffix |
   | ---------- | -------------- | --------------- |
   | Mobile     | 375 × 812      | `-mobile-375`   |
   | Tablet     | 768 × 1024     | `-tablet-768`   |
   | Desktop    | 1280 × 800     | `-desktop-1280` |

   Use `browser_resize` to set the viewport before each screenshot. Use `browser_take_screenshot` with `fullPage: true` to capture the entire scrollable page, and save with the `filename` parameter pointing to the `screenshots/` folder.

   **Playwright MCP example sequence** (assuming feature slug is `onboarding-flow`):

   ```
   1. browser_navigate → { url: "http://localhost:3000" }
   2. browser_resize   → { width: 1280, height: 800 }
   3. browser_take_screenshot → { type: "png", filename: ".design/onboarding-flow/screenshots/review-homepage-desktop-1280.png", fullPage: true }
   4. browser_resize   → { width: 768, height: 1024 }
   5. browser_take_screenshot → { type: "png", filename: ".design/onboarding-flow/screenshots/review-homepage-tablet-768.png", fullPage: true }
   6. browser_resize   → { width: 375, height: 812 }
   7. browser_take_screenshot → { type: "png", filename: ".design/onboarding-flow/screenshots/review-homepage-mobile-375.png", fullPage: true }
   ```

   **c. Capture interactive states (when relevant).**
   - Hover states on buttons, cards, links
   - Focus states on form fields
   - Open states on dropdowns, modals, menus
   - Error/success states on forms
   - Loading and empty states

   **d. Capture dark mode (if the project supports it).** Toggle dark mode and repeat the responsive breakpoint captures with `-dark-mode` in the filename.

   **e. Capture specific components.** If the review focuses on a particular component, use the `element` and `ref` parameters to screenshot just that element.

   ### Analyze Every Screenshot

   After capturing, visually analyze each screenshot against the design brief. For each screenshot:
   - Compare against the brief's aesthetic direction
   - Check visual hierarchy: is the most important element the most prominent?
   - Check spacing consistency: do margins and padding look even and intentional?
   - Check color: does the palette match the brief's direction?
   - Check typography: are font sizes, weights, and spacing visually correct?
   - Check responsive adaptation: does the layout properly reorganize (not just shrink)?
   - Note rendering issues that code review alone would miss (font loading failures, broken images, layout overflow, z-index problems, incorrect border-radius, color mismatches)

   Reference specific screenshots by filename in the review output so findings are traceable.

4. **Run the review checklist below.** For each category, note what passes and what needs refinement. Be specific. Reference exact components, files, line numbers, and screenshot filenames.

5. **Produce a prioritized refinement list.** Group issues by severity:
   - **Must fix**: Broken functionality, accessibility failures, major deviations from the brief.
   - **Should fix**: Inconsistencies, missing states, responsive issues.
   - **Could improve**: Polish, animation refinement, typography fine-tuning.

6. Save the review as `DESIGN_REVIEW.md` inside the feature's `.design/<feature-slug>/` folder (next to `DESIGN_BRIEF.md`). If no `.design/` folder exists, save to the project root. Include a "Screenshots Captured" section listing all screenshots taken with their paths. Present the review directly as well if the user prefers.

## Review Checklist

### Visual Hierarchy

- Is the most important content the most visually prominent on each page/view?
- Does the type scale create clear levels of importance (heading, subheading, body, caption)?
- Do interactive elements (buttons, links, inputs) have enough visual weight to be found without hunting?
- Is there a clear reading order? Can you trace where the eye goes first, second, third?

### Consistency

- Are spacing values consistent? Check padding and margins against the established scale (4px/8px base or whatever the project uses).
- Are colors used consistently? Check that the same semantic meaning always maps to the same color (primary actions, errors, success states, disabled states).
- Are border radii, shadow values, and font sizes reused from a shared set, or are there one-off values?
- Do similar components look and behave similarly? (e.g., all cards, all form fields, all buttons within a category.)

### Aesthetic Fidelity

- Does the implementation match the named philosophy from the brief?
- Would someone looking at this immediately recognize the intended aesthetic direction?
- Are there elements that break the aesthetic (a generic component in an otherwise distinctive interface, a conflicting font, an out-of-place color)?
- Does the level of detail match the philosophy? (Minimalist designs should not have unnecessary decoration. Maximalist designs should not have empty, unfinished areas.)

### Component Quality

- Do existing components from the codebase appear correctly, or were they reimplemented?
- Are new components following the same API patterns (props, naming, file organization) as existing ones?
- Are there duplicate components that should be consolidated?

### States and Interactions

- Do interactive elements have all necessary states: default, hover, focus, active, disabled?
- Do form fields have states for: empty, filled, error, success, disabled?
- Are loading states handled? Empty states?
- Do transitions and animations match the philosophy's motion guidelines?
- Is there visual feedback for every user action?

### Responsive Behavior

- Does the layout work at mobile (375px), tablet (768px), and desktop (1280px+)?
- Do components adapt appropriately? (Not just shrink, but reorganize when needed.)
- Is touch target size adequate on mobile (minimum 44x44px)?
- Does text remain readable at all breakpoints? No text too small, no lines too wide (max 65-75 characters).

### Accessibility

- Color contrast: Do text/background combinations meet WCAG AA (4.5:1 for body text, 3:1 for large text)?
- Keyboard navigation: Can every interactive element be reached and activated with keyboard alone?
- Focus indicators: Are focus rings visible and styled consistently?
- Semantic HTML: Are headings in order? Are landmarks used (main, nav, header, footer)? Are form labels associated?
- Screen reader: Do images have alt text? Do icons have labels? Are decorative elements hidden from assistive technology?
- Motion: Is there a reduced-motion media query for users who need it?

### Typography

- Is the font actually loading? (Check for FOIT/FOUT flash.)
- Are line lengths comfortable for reading (45-75 characters on body text)?
- Is line height appropriate (1.4-1.6 for body, tighter for headings)?
- Is the type scale intentional, or are there arbitrary sizes?

### Dark Mode

- If the project has dark mode tokens, are they applied correctly?
- Are all color values using CSS variables (not hardcoded hex values that won't switch)?
- Does the dark palette feel intentional for the chosen philosophy, or is it a simple inversion?
- Are shadows adjusted for dark mode (darker, more transparent)?
- Do accent colors maintain sufficient contrast against dark backgrounds?
- Is there a working toggle mechanism or `prefers-color-scheme` support?

### Mobile-First

- Was the layout built mobile-first (using `min-width` media queries, not `max-width`)?
- Does the mobile layout work at 375px without horizontal scrolling?
- Is navigation adapted for mobile (not just a desktop nav that overflows)?
- Are touch targets at least 44x44px?
- Is body text at least 16px on mobile?

## Output Format

```markdown
# Design Review: [Feature/Page Name]

Reviewed against: DESIGN_BRIEF.md
Philosophy: [named philosophy]
Date: [date]

## Screenshots Captured

| Screenshot                                   | Breakpoint         | Description     |
| -------------------------------------------- | ------------------ | --------------- |
| `screenshots/review-[page]-desktop-1280.png` | Desktop (1280×800) | [what it shows] |
| `screenshots/review-[page]-tablet-768.png`   | Tablet (768×1024)  | [what it shows] |
| `screenshots/review-[page]-mobile-375.png`   | Mobile (375×812)   | [what it shows] |

> All screenshots are in `.design/<feature-slug>/screenshots/`.

## Summary

[2-3 sentences on overall quality and the biggest finding.]

## Must Fix

1. **[Issue]**: [Specific description with file/component reference]. See [`screenshots/[relevant-screenshot].png`]. _Fix: [concrete suggestion]._

## Should Fix

1. **[Issue]**: [Description]. See [`screenshots/[relevant-screenshot].png`]. _Fix: [suggestion]._

## Could Improve

1. **[Issue]**: [Description]. _Suggestion: [idea]._

## What Works Well

[Note the strongest aspects of the implementation. This is not padding. Designers need to know what to keep doing.]
```
