# Accessibility audit skill for Val's site

You are auditing a page, layout, or component on Val's Jekyll site for accessibility issues. The user will point you at a file, a component, or a specific area — read the relevant SCSS and HTML/Liquid, then work through every check below. Be direct about what's broken. Don't pad with reassurance about what's fine.

---

## The five display modes — check every one

All modes live in `_sass/reading-mode.scss`, applied via body classes. Any new or changed component must work in all of them.

| Mode | Body class | What changes |
|------|-----------|--------------|
| Reading mode | `body.reading-mode` | Font → Atkinson Hyperlegible, softer palette, looser spacing |
| Reduce motion | `body.reduce-motion` | All transitions/animations → 0.01ms, scroll-behavior → auto |
| Red-green colourblind | `body.cb-red-green` | Okabe-Ito palette — magenta→`#0072B2`, teal→`#E69F00`, orange→`#D55E00`, lavender→`#56B4E9` |
| Blue-yellow colourblind | `body.cb-blue-yellow` | Tritanopia-safe — teal→`#2E8B3A`, yellow→`#E8604C`, lavender→`#C0392B` |
| Greyscale | `body.cb-greyscale` | Full grey palette + border-style variants (solid/dashed/dotted) replace colour distinctions |

For each component being audited, check:
- Is it referenced in `reading-mode.scss` under each mode? If a component uses brand colours and has no override, flag it.
- Does `reading-mode` break the layout or make text unreadable?
- Does `cb-greyscale` use border-style variation to distinguish elements that were previously colour-differentiated?
- Are all text/background combinations in each mode checked for contrast (see below)?

---

## Colour contrast — WCAG AA minimum

The brand palette contrast against `$cream` (`#f7f2e8`):

| Colour | Hex | AA on cream (normal text) |
|--------|-----|--------------------------|
| `$ink` | `#1c1714` | ✅ passes |
| `$magenta` | `#d91a5e` | ✅ passes |
| `$teal` | `#008c84` | ✅ passes |
| `$orange` | `#c8421a` | ✅ passes |
| `$lavender` | `#6f4f94` | ✅ passes |
| `$yellow` | `#f0c000` | ❌ fails — never use for text on cream |

Rules:
- Normal text (under 18pt / 14pt bold): 4.5:1 minimum
- Large text (18pt+ / 14pt+ bold): 3:1 minimum
- UI components and focus indicators: 3:1 minimum against adjacent colours
- `$yellow` is background-only — never put small text in `$yellow` on `$cream` or vice versa
- White text on `$yellow` also fails — don't do it
- In each colourblind mode, re-check contrast with the substituted palette colours, not the originals

Flag any combination that fails. Calculate contrast if unsure (use the formula or known values above).

---

## Focus styles

- Every interactive element must have a visible `:focus-visible` style
- The global default is `outline: 3px solid $ink; outline-offset: 2px; border-radius: 2px` — defined in `_sass/main.scss`
- Check that component-level styles don't accidentally suppress this with `outline: none` or `outline: 0`
- On coloured backgrounds, check the focus outline is still visible — `$ink` outline on a dark background fails
- Minimum touch/click target: **44×44px** — check buttons, nav links, icon buttons, checkboxes, radio inputs

Flag:
- Any `outline: none` / `outline: 0` not paired with a custom focus style
- Interactive elements smaller than 44×44px
- Focus outlines that disappear against their background colour in any display mode

---

## Motion and animation

- All transitions and animations must be neutralised under `body.reduce-motion`:
  ```scss
  body.reduce-motion {
    *, *::before, *::after {
      transition-duration: 0.01ms !important;
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
    }
  }
  ```
- **Static transforms (tilts, offsets) are intentional brand elements — do NOT flag these.** Only flag actual transitions and animations.
- If you add a new CSS transition or animation, it is automatically covered by the above rule — but check it isn't using `will-change` or JS-driven animation that bypasses CSS.
- Also check for `prefers-reduced-motion` media query — if any JS animation doesn't read the body class, it should respect the media query instead.

---

## Semantic HTML

- One `<h1>` per page — check the layout. Post and info_page layouts both render `page.display_title | default: page.title` as the `<h1>`. If a page template adds another `<h1>`, flag it.
- Heading hierarchy must be sequential — no jumping from `<h1>` to `<h3>`
- Interactive elements must be semantically correct — buttons as `<button>`, links as `<a href>`. No `<div>` or `<span>` with click handlers unless there's a genuine reason and proper ARIA.
- Lists (`<ul>`, `<ol>`) for groups of related items — not just visual layout
- Images must have `alt` text. Decorative images get `alt=""`. Informative images need a real description.
- The skip link (`<a class="skip-link" href="#main-content">`) must be present in the layout and `<main id="main-content">` must exist — check `_layouts/default.html`

---

## ARIA

- `aria-label` on nav elements: the main nav has `aria-label="Main navigation"`, footer nav has `aria-label="Social media links"` — new navs need a label too
- `aria-current="page"` on active nav links — check any new nav additions include this logic
- The display settings panel uses `role="dialog"`, `aria-modal="true"`, `aria-labelledby`, `aria-expanded`, `aria-hidden` — if you're building any other modal/panel/dropdown, match this pattern
- Don't use ARIA to paper over bad HTML — fix the HTML first

---

## Responsive — 320px → 4K

- Breakpoints: `small: 576px`, `medium: 768px`, `large: 992px`, `x-large: 1200px` — defined in `_sass/breakpoints.scss`, accessed via `respond-to()` mixin
- No hardcoded pixel values that bypass these
- Check at 320px: does text overflow? Do buttons stack correctly? Does anything overlap?
- Check at 1600px+: does content stretch to unreadable line lengths? Is max-width applied?
- The display settings panel has a special mobile behaviour (fixed, full-width, drops from top at ≤600px) — if you're building a similar panel, check it has equivalent mobile handling

---

## How to report findings

Group by severity:

**Blocker** — fails WCAG AA, missing focus styles on interactive elements, broken in a display mode, inaccessible to keyboard users  
**Warning** — degraded but not broken, e.g. contrast is borderline, touch target is 40px not 44px, a mode override is missing but the fallback is acceptable  
**Note** — worth knowing but low risk, e.g. an ARIA attribute that could be more descriptive

For each finding: what it is, where it is (file + selector), and what to fix. Don't pad. If something passes, don't list it — only report problems.
