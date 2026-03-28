---
name: frontend-design
description: Build distinctive, production-grade frontend interfaces with high design quality, guided by named aesthetic philosophies. Use when building components, pages, or applications. Generates working code with exceptional attention to aesthetic details and creative choices that avoid generic AI output.
---

This skill guides creation of distinctive, production-grade frontend interfaces. Implement real working code with exceptional attention to aesthetic detail.

## Example prompts

- "Build the hero section from the brief"
- "Create a card component in a Scandinavian style"
- "I want this to feel like a Japanese magazine. Build the layout."
- "Build the settings page. Use whatever style fits."

## Before You Write Any Code

1. **Explore the existing codebase first.** Scan specifically for:
   - **Component directories**: `components/`, `ui/`, `shared/` and list every component by name and its props/API
   - **CSS variables / tokens**: files named `tokens.css`, `variables.css`, `theme.css`, or `:root` declarations with custom properties
   - **Tailwind config**: `tailwind.config.js` or `tailwind.config.ts`, check `theme.extend` for custom values
   - **UI framework themes**: Material UI `createTheme`, Chakra `extendTheme`, shadcn `globals.css` and `components.json`
   - **Storybook**: `.storybook/` directory or `*.stories.*` files indicating documented components
   - **Font loading**: Google Fonts links, `@font-face` declarations, font imports
   - **Layout patterns**: how existing pages handle grid, containers, breakpoints, and spacing
   - **Package.json UI dependencies**: tailwindcss, @mui/material, @chakra-ui/react, @radix-ui, lucide-react, framer-motion, etc.
   - If components exist that match or partially match what you need to build, extend or compose them. Do not create duplicates.

2. **Understand the context:**
   - What problem does this interface solve? Who uses it?
   - What is the intended emotional tone?
   - What are the hard constraints (framework, devices, performance, accessibility)?

3. **Commit to an aesthetic direction.** Either the user names one (see philosophies below) or you choose one that fits the context. State your choice and why before writing code.

## Aesthetic Philosophies

When the user names a philosophy or describes a vibe, use these as concrete implementation guides. Each philosophy defines typography, color, layout, spacing, motion, and detail treatment.

### Dieter Rams (Functionalist)
Less but better. Every element earns its place. Nothing decorative without function.
- **Typography**: Clean sans-serif (Helvetica Neue, Suisse Intl, Akkurat). Tight letterspacing on headings. Generous line height on body. One size scale, used strictly.
- **Color**: Restrained. Monochromatic with a single functional accent. White or light grey backgrounds. Color is information, not decoration.
- **Layout**: Strict grid. Clear functional hierarchy. Components aligned to a spatial system. No asymmetry for its own sake.
- **Spacing**: Consistent, mathematical scale (4px/8px base). Generous padding. Breathing room between elements.
- **Motion**: Minimal. Purposeful transitions only (state changes, reveals). No decorative animation.
- **Details**: Subtle borders and dividers over shadows. Precise alignment. Rounded corners used sparingly and consistently.

### Swiss / International Typographic
Objectivity through structure. The grid is sacred. Content is king.
- **Typography**: Strong sans-serifs (Neue Haas Grotesk, Univers, Aktiv Grotesk). Dramatic scale contrast between headings and body. All-caps subheadings with generous letterspacing.
- **Color**: High contrast. Black, white, and one primary color. Bold color blocks as compositional elements.
- **Layout**: Rigid multi-column grid. Asymmetric balance. Text and image in dialogue. Alignment across elements is non-negotiable.
- **Spacing**: Defined by the grid module. Gutters are part of the design, not afterthought.
- **Motion**: Page transitions and scroll-triggered reveals that respect the grid. No playful bounce.
- **Details**: Rules (horizontal lines) as structural elements. No gradients. No shadows. Flatness is the point.

### Japanese Minimalism (Ma)
Negative space is content. Restraint communicates sophistication. Quiet over loud.
- **Typography**: Thin-weight sans-serifs or elegant serifs (Noto Sans, Cormorant). Generous line height (1.8-2.0). Small body size with large whitespace margins.
- **Color**: Muted naturals (warm greys, stone, sage, washi). Subtle tonal shifts over hard contrasts. Near-monochrome.
- **Layout**: Asymmetric but balanced. Off-center content. Large empty areas are intentional. Content floats in space.
- **Spacing**: Extreme whitespace. Padding and margins 2-3x what feels "normal." Elements breathe.
- **Motion**: Slow, gentle fades (400-600ms). No bounce, no overshoot. Opacity transitions over position shifts.
- **Details**: Hairline borders. Subtle texture (paper grain, linen). No sharp shadows. Soft, diffused effects.

### Brutalist / Raw
Structure is visible. No polish. Anti-aesthetic is the aesthetic.
- **Typography**: System fonts, monospace (JetBrains Mono, IBM Plex Mono, Courier), or aggressive display faces. Mixed sizes. Text as texture.
- **Color**: Black and white primary. If color, it is raw and clashing (construction yellow, hazard orange, terminal green). No gradients.
- **Layout**: Visible borders. Box model exposed. Stacked blocks. Deliberate roughness. Content first, beauty never.
- **Spacing**: Tight or intentionally uneven. Padding that feels compressed.
- **Motion**: None, or jarring (instant state changes, hard cuts). No easing.
- **Details**: Visible outlines. Default browser form elements can be intentional. Text-only interfaces. No icons unless functional.

### Scandinavian
Warmth plus restraint. Functional beauty. Accessible by default.
- **Typography**: Rounded, friendly sans-serifs (Nunito, Poppins, Circular, Cera Pro). Medium weights. Comfortable reading sizes.
- **Color**: Natural palette. Warm whites, soft blues, muted greens, clay. Pastel accents. No pure black (use charcoal).
- **Layout**: Clean and open. Card-based. Rounded corners (8-12px). Comfortable, generous layouts.
- **Spacing**: Generous but not extreme. Everything feels approachable and uncluttered.
- **Motion**: Gentle, natural easing. Subtle hover lifts. Content that settles into place.
- **Details**: Soft shadows (large blur, low opacity). Rounded elements. Warm undertones in greys. Illustration-friendly.

### Art Deco / Geometric
Bold symmetry. Decorative precision. Statement and luxury.
- **Typography**: Geometric display faces (Futura, Poiret One, Josefin Sans). All-caps headlines with extreme letterspacing. Serif body text for contrast.
- **Color**: Rich and deep. Gold/champagne, emerald, navy, burgundy, black. Metallic accents (gold gradients, shimmer effects).
- **Layout**: Symmetrical and centered. Strong vertical axis. Decorative frames and borders. Layered depth.
- **Spacing**: Structured and formal. Padding is architectural.
- **Motion**: Elegant reveals. Staggered entrance animations. Parallax depth.
- **Details**: Geometric patterns (chevrons, sunbursts, fan shapes). Ornamental borders. Texture (marble, brushed metal). Statement typography at hero scale.

### Neo-Memphis
Playful chaos. Anti-corporate. Shapes as characters.
- **Typography**: Mix of weights and styles. Clashing fonts is intentional. Oversized headlines. Text at angles.
- **Color**: Bold primaries and neons. Clashing combinations (pink and yellow, blue and orange). No muted tones. Flat color, no gradients.
- **Layout**: Broken grid. Overlapping elements. Shapes (circles, triangles, squiggles) as compositional elements. Asymmetric on purpose.
- **Spacing**: Dense in some areas, empty in others. Rhythm is irregular.
- **Motion**: Bouncy, playful. Exaggerated hover effects. Elements that wiggle, rotate, or pop.
- **Details**: Thick borders. Geometric shapes as decoration. Patterns (dots, dashes, zigzags). Drop shadows with hard edges and bright colors.

### Editorial / Magazine
Content-led design. Typography does the heavy lifting. Every page is a spread.
- **Typography**: Display serif for headlines (Playfair Display, Fraunces, Instrument Serif). Clean sans for body (DM Sans, Source Sans). Dramatic scale (hero headlines at 72-120px). Pull quotes. Drop caps.
- **Color**: Minimal. Black and white with one accent. Color used editorially (to highlight, not decorate).
- **Layout**: Strong column grid (3-5 columns). Full-bleed images. Text wrapping. Mixed column widths. Vertical rhythm.
- **Spacing**: Generous margins. Tight leading on headlines, open on body. Whitespace as a compositional tool.
- **Motion**: Scroll-triggered reveals. Parallax on images. Smooth page transitions.
- **Details**: Thin rules as dividers. Caption typography. Issue/date metadata. Print-inspired details (folio numbers, running headers).

## Implementation Guidelines

- **Typography**: Choose distinctive fonts loaded via Google Fonts or CDN. Avoid generic defaults (Inter, Roboto, Arial, system fonts). Pair a display font with a body font.
- **Color**: Use CSS variables for consistency. Dominant color with sharp accents outperforms safe, evenly-distributed palettes.
- **Motion**: CSS transitions for HTML. Framer Motion / Motion library for React. Focus on high-impact moments (page load reveals, state changes) over scattered micro-interactions.
- **Spatial composition**: Unexpected layouts earn attention. Asymmetry, overlap, diagonal flow, grid-breaking elements. Or, if the philosophy demands it, strict grids executed with precision.
- **Backgrounds and depth**: Create atmosphere. Gradient meshes, noise textures, geometric patterns, layered transparencies, grain overlays. Match the chosen philosophy.

NEVER produce generic AI aesthetics: purple gradients on white, Inter font, predictable card grids, cookie-cutter component layouts. Every output should feel designed for its specific context.

Match implementation complexity to the aesthetic vision. A Dieter Rams interface is 50 lines of precise CSS. A Neo-Memphis interface is 300 lines of creative chaos. Both are correct.

## Mobile-First

Build mobile layout first, then scale up. This is non-negotiable.

- Start with a single-column layout at 375px width.
- Add complexity at each breakpoint (`min-width` media queries, not `max-width`).
- Touch targets must be at least 44x44px on mobile.
- Body text must be at least 16px on mobile (prevents iOS zoom on input focus).
- Navigation must have a mobile-specific pattern (hamburger, bottom tabs, or drawer). Do not rely on horizontal nav bars that overflow.
- Test that line lengths stay comfortable (45-75 characters) at every breakpoint.

## Dark Mode

If a design tokens file exists (from `/design-tokens`), use its dark mode palette. If not, generate dark mode support alongside the light theme.

- Use CSS custom properties so switching themes means changing variable values, not rewriting components.
- Support both `prefers-color-scheme` media query (system preference) and a `[data-theme="dark"]` attribute (manual toggle).
- Do not simply invert colors. Dark backgrounds should be warm or cool to match the philosophy (warm charcoal for Scandinavian, cool slate for Swiss, near-black for Brutalist).
- Reduce pure white text to off-white (e.g., `#E5E5E5` or `rgba(255,255,255,0.87)`) to reduce eye strain.
- Shadows in dark mode should be darker and more transparent, not the same values as light mode.
- Accent colors may need lightness adjustments to maintain WCAG contrast ratios against dark backgrounds.
- Include a `prefers-reduced-motion` media query for users who need it. Disable or simplify all animations and transitions within that query.
