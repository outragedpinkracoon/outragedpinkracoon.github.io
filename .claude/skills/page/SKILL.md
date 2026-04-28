# Page skill for Val's site

You are writing, editing, or reviewing a page on Val Dryden's coaching site. Copy and design are the same decision here — you handle both together. Apply all rules below without being asked.

---

## Voice and brand (non-negotiable)

**Her voice:** Sharp, irreverent, funny, direct, emotionally intelligent. Warm but not soft. High-agency. Mildly feral. Swear where it lands hardest, not everywhere. Zero coaching jargon (`power hour`, `intensive`, `transformational journey`, etc). Zero corporate polish. Zero dead professional copy.

**Her promise:** Fast clarity. Getting to the heart of the problem fast. One session can shift a lot.

**Her brand:** No-bullshit coaching. Lived experience is supporting proof, not the headline.

**Lines that nail her voice:**
- `I've seen this exact mess before`
- `we are not wasting time here`
- `whatever carnage is unfolding`
- `There's no undo button for people`
- `Bring your mess`
- `dangerous amount of clarity in human form`
- `done settling for this`
- `I want more than this`

**Phrases to use sparingly:** `chaos untangler`, `fast clarity`

**Avoid:** Too much doom upfront. Overexplaining. SEO sludge. Polished consultant/therapist/LinkedIn voice. Weird metaphors. Try-hard or accidentally poetic. Overusing `fast clarity`.

## Audience

- Engineering managers new to people leadership (overwhelmed, underbriefed, suddenly responsible for actual humans)
- Neurodivergent, queer, disabled, under-represented folks in tech
- Burnt out women who mask
- Softer men who are overlooked
- People doing the job without title, credit, or promotion
- Ambitious and blocked, or quietly wanting more

**Important:** Don't write as if only people in collapse deserve coaching. Keep the door wide for aspirational buyers too. `I work in tech and I want more than this` is a better front door than `I'm done`.

## Reference: what good copy looks like

These lines represent her voice at its best — use them to calibrate:

**Index:**
> "You do not need six weeks of 'how does that feel?' while Slack ruins your blood pressure."
> "hear three minutes of whatever carnage is unfolding, spot the actual problem"
> "If you want autistic directness, kindness, hard-won judgement, and someone who can do more in one session than most coaches manage in ten, welcome."

**Coaching router:**
> "You bring the mess. I help you get fast clarity on what is actually going on, what matters, and what the hell to do next."
> "You're a manager now. Sorry."
> "You are capable, ambitious, and tired of being treated like a maybe."

**Engineering managers page:**
> "You've been promoted. Congratulations. Also: holy shit."
> "suddenly you cannot hide in your IDE anymore"
> "Without the HR varnish, the corporate euphemisms, or weeks of polite pissing about."

**Folks in tech page:**
> "You're good at this. That's not the problem."
> "exhausted from making yourself easier to digest"
> "talented in rooms that keep asking them to prove the obvious"
> "I cannot work out whether I need confidence, boundaries, accommodations, a new job, or a nap that lasts six months."

**Who is Val:**
> "I coach the people I used to be"
> "This is not 'how do I feel about that?' coaching. This is 'what's actually going on, what matters, and what are you going to do about it?' coaching."
> "Weird, tired, furious, ambitious, confused and brilliant can all come in."

## Conversion rules

- Lead with problem, get to fix fast
- Router/overview pages: open the door, don't diagnose hard
- Deeper sales pages: more bite
- No padding, no reassuring lines that add nothing
- Vivid and specific over abstract
- Every section should make the reader think: "Oh fuck, that's me" / "She gets it" / "Take my money"
- Single session is the hero offer; bundle is for when more room is needed
- No fit checks. No defensive pricing. Frame: valuable because it works, fast.

---

## Aesthetic — what this site is

**Risograph print aesthetic with MÖRK BORG-influenced chaos.** That means:

- Bold, flat, saturated colour — no gradients, no gentle pastels, no corporate clean
- Hard offset box-shadows (e.g. `8px 8px 0 $ink`) instead of soft drop shadows
- Deliberate misalignment, tilt, and visual tension — things are supposed to look slightly unhinged, not broken
- Paper grain texture (a fixed SVG noise overlay at `body::before`) — don't remove it
- High contrast, expressive typography — `Fraunces` (inky editorial serif) for display, `Bricolage Grotesque` for headings/nav, `Space Grotesk` for body
- Colour rotation across repeated elements (cards, lists, badges) — adjacent items should clash interestingly, not harmonise safely

This is not a site that should ever look minimal, airy, or neutral. If a design proposal looks like it belongs on a SaaS landing page, it's wrong.

## Brand palette

All colours are SCSS variables in `_sass/variables.scss`. Always use the variables — never hardcode hex values.

| Variable | Hex | Role |
|----------|-----|------|
| `$magenta` | `#d91a5e` | Primary brand colour — non-negotiable |
| `$cream` | `#f7f2e8` | Background — uncoated risograph paper |
| `$ink` | `#1c1714` | Text / shadows — warm near-black |
| `$teal` | `#008c84` | Secondary accent |
| `$yellow` | `#f0c000` | Accent — use sparingly, high visual weight |
| `$lavender` | `#6f4f94` | Accent |
| `$orange` | `#c8421a` | Accent |

Semantic aliases: `$bg-color` → `$cream`, `$primary-color` → `$magenta`, `$text-color` → `$ink`

Card accent rotation: `$card-accents: $magenta, $teal, $orange, $lavender`

**Contrast rule:** All text on coloured backgrounds must pass WCAG AA. `$yellow` and `$cream` are not safe for small text — use `$ink` on top of both.

## Non-negotiable constraints

**Responsive — hard requirement:** Every change must work at 320px → 4K. No exceptions. Test your mental model at both extremes before proposing anything.

**Accessibility modes — must not be broken.** All in `_sass/reading-mode.scss`:

| Mode | Body class | What it does |
|------|-----------|--------------|
| Reading mode | `body.reading-mode` | Atkinson Hyperlegible, softer palette, looser spacing |
| Reduce motion | `body.reduce-motion` | Kills transitions/animations |
| Red-green colourblind | `body.cb-red-green` | Okabe-Ito safe palette |
| Blue-yellow colourblind | `body.cb-blue-yellow` | Tritanopia-safe palette |
| Greyscale | `body.cb-greyscale` | Full grey palette, border-style variants for distinction |

When adding a new component: check whether its colours rely on any swapped palette. If yes, add overrides in `_sass/reading-mode.scss`.

## SCSS structure

| File | Purpose |
|------|---------|
| `_sass/variables.scss` | Palette, spacing, font vars |
| `_sass/main.scss` | Base styles |
| `_sass/breakpoints.scss` | Breakpoint mixins/vars — use these, not magic numbers |
| `_sass/reading-mode.scss` | All accessibility mode overrides |
| `_sass/post.scss` | Single post styles |
| `_sass/posts.scss` | Post list styles |
| `assets/css/styles.scss` | Entry point — imports everything |

---

## What to check on every page change

**Copy:**
- Does every line sound like Val, not a LinkedIn coach?
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
