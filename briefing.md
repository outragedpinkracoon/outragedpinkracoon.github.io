# Design Briefing — Outraged Racoon Coaching

**Brief:** Bold, distinctive Riso-like colours with the chaotic energy of Mork Borg / Johan Nohr. Bright and fun.  
**Constraint:** Must work on 4K monitors, smartphones, and everything between.

---

## Current Stack

- **Palette:** `$cream` bg, `$ink`, `$magenta`, `$teal`, `$yellow`, `$orange`, `$lavender`
- **Fonts:** Fraunces (display/h1), Bricolage Grotesque (h2–h6, nav), Space Grotesk (body)
- **Source:** `_sass/main.scss`, `_sass/variables.scss`, `_sass/post.scss`, `_sass/posts.scss`, `_sass/categories.scss`

---

## What's Working

- Riso palette is correct and well-named
- Hard box-shadows on cards, blockquotes, callouts — right direction
- Off-register text-shadow on site header
- Diagonal hatch on h2 — good concept
- Fraunces + Bricolage Grotesque is a strong pairing
- Cards with solid colour backgrounds + contrasting shadows

---

## What's Not Working

### 1. Rotations are timid
Mork Borg / Johan Nohr rotates elements **1.5–4 degrees** — enough to feel intentionally unhinged. Current values (`-0.4deg`, `0.5deg`) are imperceptible and read as rendering artefacts rather than design choices.

### 2. Noise is almost invisible
`opacity: 0.042` contributes almost nothing. Riso paper grain should be *felt* — like uncoated stock, not a clean hex background.

### 3. Yellow is wasted
`$yellow` only appears on blockquotes and as a faint h2 shadow layer. In Nohr's work, yellow is blinding and radioactive. It needs to hit as a full background on at least one major component.

### 4. Typography hierarchy is too polished
Conventional descending scale (h1: 3rem, h2: 1.9rem, h3: 1.4rem). Nohr uses violent contrast — massive display type next to tiny labels. The h1 should feel slightly *too* big.

### 5. Header is too calm and symmetrical
Clean centred masthead with a tidy magenta rule above and teal below. That's editorial magazine energy. Nohr misaligns things and uses thick rules that feel stamped.

### 6. Nav is near-invisible
`rgba($ink, 0.5)` at `0.82rem` — disappears on most screens. Navigation in this aesthetic should be bold and legible.

### 7. Card shadows are undersized
`6px 6px` is correct in concept but underpowered. The hover jump (6→9px) is barely noticeable. Both need to be bigger and more dramatic.

### 8. h2 diagonal hatch is invisible
`rgba($cream, 0.08)` on magenta is theoretically great but practically invisible. The texture needs to be seen.

### 9. Page subtitle is stuck in the middle
`rgba($ink, 0.4)` at `0.78rem` — neither deliberately suppressed nor a visual element. In Nohr's layouts a subtitle either whispers (tiny, near-invisible) or shouts. This one does neither.

---

## Change List

All changes must be tested at mobile (320px+), tablet (768px), desktop (1280px), and 4K (2560px+).

| # | Change | File | Lines |
|---|--------|------|-------|
| 1 | ~~Noise overlay~~ — skipped; blend mode limitations on light backgrounds make this not worth pursuing | — | — |
| 2 | Blockquote rotation `-0.4deg` → `-2deg`; callout `0.5deg` → `1.8deg` | `_sass/main.scss` | ~719, ~761 |
| 3 | ~~h2 diagonal hatch~~ — removed entirely, too busy | — | — |
| 4 | Card box-shadows `6px` → `8px`; hover `9px` → `12px` | `_sass/main.scss` | ~476 |
| 5 | h1 font-size `3rem` → `4rem` mobile, `5rem` at medium breakpoint | `_sass/main.scss` | ~56 |
| 6 | Nav links: full `$ink` opacity, bolder active/hover state | `_sass/main.scss` | ~216 |
| 7 | Profile image: `rotate(2deg)` + heavier misaligned shadow | `_sass/main.scss` | ~697 |

---

## Responsive Notes

- **Rotations:** Large rotations (2deg+) on small screens can cause horizontal overflow. Use `overflow-x: hidden` on body (already set) and test that rotated blockquotes/callouts using negative margins don't escape the viewport on 320px screens.
- **h1 size:** 4rem mobile is bold but watch for line wrapping on very long page titles. `line-height: 1.0` may need adjusting at smaller sizes.
- **Card shadows:** At 4K the 8px hard shadow may look small relative to the card size. Consider scaling shadows up at large breakpoints.
- **Noise overlay:** SVG noise is `150px` tiled — at 4K the tile is the same physical size so grain will look finer. This is acceptable (more like fine paper grain at scale).
- **Nav:** Currently wraps on mobile — bold full-opacity links will be more legible but ensure the dot separators still work when wrapping.
- **Profile image rotation:** Float-right layout kicks in at `medium` breakpoint. Rotation looks best when floated; on mobile (centred, full-width) a slight rotation is fine but ensure it doesn't cause overflow.
