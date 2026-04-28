# Design skill for Val's site

You are making design or layout changes to Val's Jekyll site. Apply all rules below without being asked.

## Aesthetic — what this site is

**Risograph print aesthetic with MÖRK BORG-influenced chaos.** That means:

- Bold, flat, saturated colour — no gradients, no gentle pastels, no corporate clean
- Hard offset box-shadows (e.g. `8px 8px 0 $ink`) instead of soft drop shadows
- Deliberate misalignment, tilt, and visual tension — things are supposed to look slightly unhinged, not broken
- Paper grain texture (a fixed SVG noise overlay at `body::before`) gives everything an uncoated print feel — don't remove it
- High contrast, expressive typography — `Fraunces` (inky editorial serif) for display, `Bricolage Grotesque` (hand-set irregular grotesque) for headings/nav, `Space Grotesk` for body
- Colour rotation across repeated elements (cards, lists, badges) — adjacent items should clash interestingly, not harmonise safely

This is not a site that should ever look minimal, airy, or neutral. If a design proposal looks like it belongs on a SaaS landing page, it's wrong.

## Brand palette

All colours are defined as SCSS variables in `_sass/variables.scss`. Always use the variables — never hardcode hex values in component SCSS.

| Variable | Hex | Role |
|----------|-----|------|
| `$magenta` | `#d91a5e` | **Primary brand colour — non-negotiable.** Fluorescent risograph pink. |
| `$cream` | `#f7f2e8` | Background — uncoated risograph paper |
| `$ink` | `#1c1714` | Text / shadows — warm near-black |
| `$teal` | `#008c84` | Secondary accent |
| `$yellow` | `#f0c000` | Accent — use sparingly, high visual weight |
| `$lavender` | `#6f4f94` | Accent — darkened for AA contrast on cream |
| `$orange` | `#c8421a` | Accent — darkened for AA contrast on cream |

Semantic aliases (use these in component code):
- `$bg-color` → `$cream`
- `$primary-color` → `$magenta`
- `$text-color` → `$ink`

Card accent rotation: `$card-accents: $magenta, $teal, $orange, $lavender` — use this list for `nth-child` colour cycling.

**Contrast rule:** All text on coloured backgrounds must pass WCAG AA. `$yellow` and `$cream` are not safe for small text — use `$ink` on top of both. `$magenta`, `$teal`, `$orange`, `$lavender` are all cleared for `$cream` body text at normal sizes (they've been adjusted for this).

**Callout variants and link safety:** `.callout--teal` uses `$cream` text — do not place `$magenta` links inside it (magenta-on-teal clashes badly; global link styles can bleed through). If a callout contains a link, use `.callout--yellow` instead, which has `$ink` text and the default `$magenta` link colour — safe and on-brand.

## Non-negotiable constraints

**Responsive — hard requirement:** Every change must work at 320px → 4K. No exceptions. Test your mental model at both extremes before proposing anything. If a layout breaks at 320px, it's broken.

**Accessibility stylesheets — must not be broken:** The site has multiple user-toggled display modes, all in `_sass/reading-mode.scss`. Any new CSS class, component, or colour change must be checked against all of these:

| Mode | Body class | What it does |
|------|-----------|--------------|
| Reading mode | `body.reading-mode` | Swaps to Atkinson Hyperlegible, softer palette, looser spacing |
| Reduce motion | `body.reduce-motion` | Kills transitions/animations, keeps static transforms |
| Red-green colourblind | `body.cb-red-green` | Okabe-Ito safe palette (replaces magenta/teal/orange/lavender) |
| Blue-yellow colourblind | `body.cb-blue-yellow` | Tritanopia-safe (replaces teal/yellow with green/coral/red) |
| Greyscale | `body.cb-greyscale` | Full grey palette, uses border-style variants (solid/dashed/dotted) to distinguish elements |

When you add a new component:
- Check whether its colours rely on any of the palettes being swapped out
- If yes, add overrides for the affected modes in `_sass/reading-mode.scss`
- When in doubt, add the override — it's better to be explicit

## Breakpoints

Breakpoints are defined in `_sass/breakpoints.scss`. Use those variables, not magic numbers.

## SCSS structure

| File | Purpose |
|------|---------|
| `_sass/variables.scss` | Palette, spacing, font vars |
| `_sass/main.scss` | Base styles |
| `_sass/breakpoints.scss` | Breakpoint mixins/vars |
| `_sass/reading-mode.scss` | All accessibility mode overrides |
| `_sass/post.scss` | Single post styles |
| `_sass/posts.scss` | Post list styles |
| `_sass/categories.scss` | Category page styles |
| `assets/css/styles.scss` | Entry point — imports everything |

Add new component SCSS into the most appropriate existing file, or create a new `_sass/<component>.scss` and import it from `assets/css/styles.scss`.

## What to check on every design change

1. Does it hold at 320px? Does it hold at 1600px+?
2. Does any new colour need overrides in `reading-mode.scss`?
3. Does `reduce-motion` mode need an explicit override if you added transitions or animations?
4. Have you introduced any colour-only meaning (e.g. red = error) without a non-colour fallback? If so, fix it.

## When reviewing design work

Flag:
- Hardcoded breakpoint values that bypass `_sass/breakpoints.scss`
- New colours added to component SCSS but not handled in any mode in `reading-mode.scss`
- Transitions/animations not neutralised under `body.reduce-motion`
- Anything that breaks below ~400px
- Missing `focus-visible` styles on interactive elements (min 44×44px touch targets)

Preserve:
- The bold, high-contrast, deliberate aesthetic — this is not a neutral site
- Existing tilt/shadow/offset patterns — they're intentional brand elements
- Any component already tested and signed off across modes
