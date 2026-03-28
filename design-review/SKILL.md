---
name: design-review
description: Run a structured design critique against the brief and codebase. Checks visual hierarchy, consistency, responsiveness, accessibility, and aesthetic fidelity. Use when user wants a design review, critique, QA pass, polish pass, or mentions "review" after building.
---

This skill runs a structured design review of what has been built, measured against the design brief and the chosen aesthetic philosophy.

## Example prompts

- "Review what I just built"
- "Run a design critique on the landing page"
- "Check this against the brief"
- "Here's a screenshot. How does it look?" [paste screenshot]
- "QA pass before I ship this"

## Process

1. **Read the brief.** Look for `DESIGN_BRIEF.md` in the project root. If it does not exist, ask the user what the intended design direction was.

2. **Explore the built code.** Examine every component, page, and style file that was created or modified. Scan specifically for:
   - All new or modified components and their relationship to pre-existing components
   - Token/variable usage: are components using shared tokens or hardcoding values?
   - Duplicate components that should be consolidated
   - File naming and organization: do new files follow the project's conventions?
   - Understand what was actually built, not what was planned.

3. **Screenshot review (if provided).** If the user provides a screenshot or image of the rendered output:
   - Compare the visual output against the design brief's aesthetic direction
   - Check visual hierarchy: is the most important element the most prominent?
   - Check spacing consistency: do margins and padding look even and intentional?
   - Check color: does the palette match the brief's direction?
   - Check typography: are font sizes, weights, and spacing visually correct?
   - Check responsive appearance if multiple screenshots are provided
   - Note any rendering issues visible in the screenshot that code review alone would miss (font loading failures, broken images, layout overflow, z-index problems)

4. **Run the review checklist below.** For each category, note what passes and what needs refinement. Be specific. Reference exact components, files, and line numbers.

5. **Produce a prioritized refinement list.** Group issues by severity:
   - **Must fix**: Broken functionality, accessibility failures, major deviations from the brief.
   - **Should fix**: Inconsistencies, missing states, responsive issues.
   - **Could improve**: Polish, animation refinement, typography fine-tuning.

6. Save the review as `DESIGN_REVIEW.md` in the project root, or present it directly if the user prefers.

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

## Summary
[2-3 sentences on overall quality and the biggest finding.]

## Must Fix
1. **[Issue]**: [Specific description with file/component reference]. _Fix: [concrete suggestion]._

## Should Fix
1. **[Issue]**: [Description]. _Fix: [suggestion]._

## Could Improve
1. **[Issue]**: [Description]. _Suggestion: [idea]._

## What Works Well
[Note the strongest aspects of the implementation. This is not padding. Designers need to know what to keep doing.]
```
