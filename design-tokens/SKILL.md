---
name: design-tokens
description: Generate a design tokens file (CSS variables or Tailwind config) based on a chosen aesthetic philosophy, with light and dark mode palettes, spacing scale, type ramp, and component-level tokens. Use when starting a new project, establishing a visual system, setting up tokens, or mentions "tokens" or "design system".
---

This skill generates the foundational design tokens for a project. Run this after the design brief and before building any components. Every component built after this references these tokens instead of hardcoding values.

## Example prompts

- "Set up design tokens for this project"
- "Generate a token system based on Dieter Rams"
- "I need a spacing scale and color palette before I start building"
- "Create tokens that match our brief"

## Process

1. **Check what already exists.** Before generating anything, scan the codebase for:
   - CSS variable definitions (`:root`, `[data-theme]`, custom property files)
   - Tailwind config (`tailwind.config.js`, `tailwind.config.ts`) and any theme extensions
   - Theme provider files (Material UI `createTheme`, Chakra `extendTheme`, shadcn `globals.css`)
   - Design token JSON files (Style Dictionary format, Figma token exports)
   - Any `tokens.css`, `variables.css`, `theme.css`, or similarly named files
   - `package.json` for UI framework dependencies (tailwindcss, @mui/material, @chakra-ui/react, etc.)

   If tokens already exist, **extend them** rather than replacing. Identify gaps (missing dark mode, incomplete spacing scale, no motion tokens) and fill those.

2. **Read the brief.** Look for a design brief at `.design/*/DESIGN_BRIEF.md`. If multiple subfolders exist, use the most recently modified one, or ask the user which feature they are working on. If a philosophy is named, use the parameters from `/frontend-design` to derive token values. If no brief exists, ask the user what direction they want.

3. **Generate tokens** in the format that matches the project's tech stack:
   - Tailwind project → extend `tailwind.config.js` and write to `globals.css`
   - CSS/HTML project → write to a `tokens.css` file
   - CSS-in-JS project → write to a `theme.ts` or `theme.js` file
   - If unclear, default to CSS custom properties (most portable)

4. **Always generate both light and dark mode palettes.** Use `[data-theme="dark"]` or `prefers-color-scheme` media query. Both palettes should feel intentional for the chosen philosophy, not just inverted values.

## Token Categories

### Color

```css
/* Semantic color tokens, not raw values */
--color-bg-primary:          /* Main background */
--color-bg-secondary:        /* Secondary/card background */
--color-bg-tertiary:         /* Subtle background (inputs, wells) */
--color-bg-inverse:          /* Inverted background */

--color-text-primary:        /* Main text */
--color-text-secondary:      /* Subdued text */
--color-text-tertiary:       /* Placeholder, disabled text */
--color-text-inverse:        /* Text on inverse backgrounds */
--color-text-link:           /* Link color */

--color-border-primary:      /* Default borders */
--color-border-secondary:    /* Subtle borders */
--color-border-focus:        /* Focus ring color */

--color-accent-primary:      /* Primary action color */
--color-accent-primary-hover:
--color-accent-primary-active:
--color-accent-secondary:    /* Secondary action color */

--color-status-success:
--color-status-warning:
--color-status-error:
--color-status-info:

--color-surface-overlay:     /* Modal/dropdown backdrop */
```

### Spacing

Generate a consistent scale. The base unit should match the philosophy:
- Tight philosophies (Brutalist, Swiss): 4px base
- Balanced philosophies (Rams, Scandinavian): 4px or 8px base
- Spacious philosophies (Japanese Minimalism, Editorial): 8px base with larger multipliers

```css
--space-0:   0;
--space-1:   /* base * 0.25 */
--space-2:   /* base * 0.5 */
--space-3:   /* base * 0.75 */
--space-4:   /* base * 1 */
--space-5:   /* base * 1.5 */
--space-6:   /* base * 2 */
--space-7:   /* base * 3 */
--space-8:   /* base * 4 */
--space-9:   /* base * 6 */
--space-10:  /* base * 8 */
--space-11:  /* base * 12 */
--space-12:  /* base * 16 */
```

### Typography

```css
--font-family-display:       /* Headline/display font */
--font-family-body:          /* Body text font */
--font-family-mono:          /* Code/monospace font */

--font-size-xs:
--font-size-sm:
--font-size-base:
--font-size-md:
--font-size-lg:
--font-size-xl:
--font-size-2xl:
--font-size-3xl:
--font-size-4xl:             /* Hero/display size */

--font-weight-normal:
--font-weight-medium:
--font-weight-semibold:
--font-weight-bold:

--line-height-tight:         /* Headings: 1.1-1.3 */
--line-height-normal:        /* Body: 1.4-1.6 */
--line-height-relaxed:       /* Spacious body: 1.6-1.8 */

--letter-spacing-tight:      /* Display type */
--letter-spacing-normal:
--letter-spacing-wide:       /* All-caps, labels */
```

### Layout

```css
--max-width-content:         /* Max reading width (65-75ch equivalent) */
--max-width-wide:            /* Wide content area */
--max-width-page:            /* Full page max width */

--border-radius-sm:
--border-radius-md:
--border-radius-lg:
--border-radius-full:        /* Pill/circle */

--shadow-sm:
--shadow-md:
--shadow-lg:
--shadow-focus:              /* Focus ring shadow */
```

### Motion

```css
--duration-instant:   50ms;
--duration-fast:      150ms;
--duration-normal:    250ms;
--duration-slow:      400ms;
--duration-slower:    600ms;

--easing-default:     cubic-bezier(0.4, 0, 0.2, 1);
--easing-in:          cubic-bezier(0.4, 0, 1, 1);
--easing-out:         cubic-bezier(0, 0, 0.2, 1);
--easing-bounce:      cubic-bezier(0.34, 1.56, 0.64, 1);
```

### Responsive Breakpoints

```css
--breakpoint-sm:   375px;    /* Mobile */
--breakpoint-md:   768px;    /* Tablet */
--breakpoint-lg:   1024px;   /* Small desktop */
--breakpoint-xl:   1280px;   /* Desktop */
--breakpoint-2xl:  1536px;   /* Wide desktop */
```

## Dark Mode

Always generate dark mode tokens alongside light mode. Rules:

- Do not simply invert colors. Dark backgrounds should be warm or cool depending on the philosophy.
- Reduce contrast slightly in dark mode (pure white text on pure black is harsh).
- Shadows should use darker, more transparent values in dark mode, not the same shadows as light.
- Accent colors may need lightness adjustments to maintain contrast ratios.
- Include a `prefers-color-scheme` media query AND a `[data-theme="dark"]` attribute selector so the user can support both system preference and manual toggle.

```css
:root {
  /* Light mode tokens */
}

[data-theme="dark"] {
  /* Dark mode overrides */
}

@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    /* System-preference dark mode, unless user explicitly chose light */
  }
}
```

## Output

Save the tokens file in the appropriate location for the project's tech stack. State which philosophy the tokens are derived from and note any deviations or choices made.
