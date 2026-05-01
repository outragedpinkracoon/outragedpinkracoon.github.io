# Page skill for Val's site

You are writing, editing, or reviewing a page on Val Dryden's coaching site. Copy and design are the same decision here — you handle both together. Apply all rules below without being asked.

**Read all of these before doing anything:**
- `.claude/skills/copywrite/skill.md` — voice, audience, conversion rules, reference copy
- `.claude/skills/design/skill.md` — aesthetic, palette, constraints, SCSS structure
- `.claude/skills/site-pages.md` — index of all main pages and shared includes

Everything in those files applies here. The sections below are page-specific additions only.

**After reading the skills, ask the user what they need before doing any work.** Do not review, rewrite, or flag anything until you know what they're asking for.

---

## Page-specific conversion rules

- Single session is the hero offer; bundle is for when more room is needed
- Router/overview pages: open the door, don't diagnose hard
- Deeper sales pages: more bite
- No fit checks. No defensive pricing. Frame: valuable because it works, fast.

## Shared components — use Jekyll includes

Shared components live in `_includes/`. Always use these rather than duplicating HTML across pages:
- `{% include credibility-strip.html %}` — Val's credentials/stats bar
- `{% include pricing.html %}` — full pricing table, saving badges, teams card, pull-quote
- `{% include session-process.html %}` — "What happens in a remote 1:1 session" steps

If you're adding something that appears on more than one page, make it an include.

---

## What to check on every page change

**Copy:**
- Does every line sound like Val, not a LinkedIn coach?
- Are there any em dashes (—)? Replace with a period, comma, or colon. Val hates them as an AI tell.
- Is there doom without exit? Fix it.
- Is there padding that adds nothing? Cut it.
- Is jargon (`transformational`, `power hour`, `journey`) anywhere? Kill it.

**Design:**
- Does it hold at 320px and 1600px+?
- Does any new colour need overrides in `reading-mode.scss`?
- Does `reduce-motion` need an explicit override if you added transitions?
- Have you introduced colour-only meaning without a non-colour fallback?
- Are interactive elements keyboard accessible with visible focus styles? (min 44×44px touch targets)

## When reviewing existing pages

Flag copy that is:
- Too polished, too corporate, too gentle
- Abstract where it should be specific
- Too much doom with no exit
- Padding that adds nothing

Flag design that has:
- Hardcoded breakpoint values bypassing `_sass/breakpoints.scss`
- New colours not handled in `reading-mode.scss`
- Transitions not neutralised under `body.reduce-motion`
- Anything breaking below ~400px

Preserve:
- Lines that already sound like Val — specific, vivid, funny, with bite
- The bold, high-contrast, deliberately unhinged aesthetic
- Existing tilt/shadow/offset patterns
- Any component already tested and signed off across modes

When you flag something weak — copy or design — replace it, don't just point at it.
