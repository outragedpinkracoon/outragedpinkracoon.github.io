# SEO review skill for Val's site

You are reviewing or improving SEO on Val's Jekyll coaching site. Apply everything below without being asked.

## Who this site is trying to reach

These are the target audiences, in rough priority order:

1. **New engineering managers** — promoted into people leadership, overwhelmed, no playbook, suddenly responsible for real humans
2. **Neurodivergent, queer, disabled, and under-represented folks in tech** — good at the job, treated like a maybe, masking, exhausted
3. **Burnt-out women in tech** — done shrinking, considering a move or just wanting more
4. **Softer men who are overlooked** — capable, blocked, not the loud one in the room
5. **Ambitious people who want more** — not necessarily in crisis, just done settling

The site is NOT targeting:
- HR departments or L&D buyers
- Corporate training budgets
- People who want therapy or long-form coaching programmes
- Generic "life coaching" searches

## Search intent to capture

| Intent | What they search | What to serve |
|--------|-----------------|---------------|
| New manager panic | "new engineering manager help", "just been promoted to manager scared", "engineering manager coaching" | `/coaching/engineering-managers/` |
| Identity/belonging in tech | "coaching for neurodivergent people tech", "queer tech coach", "coaching for disabled engineers" | `/coaching/folks-in-tech/` |
| General coaching browse | "ILM certified coach Scotland", "tech leadership coach remote", "executive coach for engineers" | `/coaching/` and `/` |
| Trust / who is this person | "Val Dryden coach", "Outraged Racoon Coaching" | `/who-is-val/` |
| Content discovery | Blog posts matching specific problems (imposter syndrome, 1:1s, giving feedback, burnout) | Individual posts |

## Technical setup

- Jekyll with `jekyll-seo-tag` — the `{% seo %}` tag in `_layouts/default.html` generates `<title>`, `<meta name="description">`, Open Graph, and Twitter Card tags automatically
- Page-level SEO is set via front matter: `title:`, `description:`, `image:`
- Structured data (JSON-LD) is handwritten in `_layouts/default.html` — Service + FAQPage schemas appear on coaching pages; Person + WebSite on all pages
- `jekyll-sitemap` auto-generates `/sitemap.xml`
- Analytics: Simple Analytics (privacy-first, no cookies)

## What to check on every page review

### Front matter
- `title:` — does it contain a target keyword AND sound like Val? Not "Coaching Services". More like "Engineering Manager Coaching — Outraged Racoon"
- `description:` — 140–160 chars, leads with the reader's problem, sounds human not corporate, contains at least one search term
- `image:` — is there a meaningful OG image set? Defaults to `/assets/images/site/racoon.jpg` if not overridden

### Headings
- Is there exactly one `<h1>` per page?
- Does the `<h1>` contain a keyword that matches what the audience would type?
- Do `<h2>` headings reinforce the topic, not just act as visual dividers?

### Body copy
- Does the page use the language the audience uses? ("new manager", "neurodivergent", "engineering", "tech", "feedback", "1:1s", "promotion") — not vague coaching language
- Is the primary audience problem named explicitly within the first 100 words?
- Are there internal links to related pages (e.g. coaching page → engineering managers page)?

### Structured data (JSON-LD)
- Coaching pages: does the Service schema have a specific, descriptive `description`? Is pricing up to date? (`priceValidUntil` is currently set to 2026-12-31 — flag if expired)
- FAQ schema: are the questions ones the audience would actually search? Flag generic filler questions
- All pages: Person schema has `jobTitle: "ILM Certified Coach"` — check this reflects current credentials

### Links and crawlability
- Internal links: are key pages (especially `/coaching/engineering-managers/` and `/coaching/folks-in-tech/`) linked from multiple places?
- Blog posts: do they link back to the relevant coaching page where appropriate?
- Are there any orphan pages (no inbound links from the site)?

### Blog post SEO
- Does the `title:` front matter read as something a person would search, not just a clever headline?
- Is the post `description:` specific enough to stand out in a results page?
- Does the post target one specific problem or question, not a broad topic?
- Is there a relevant internal link to a coaching page?

## What good looks like

**Strong description example:**
> "You've just been promoted to engineering manager. Nobody told you what that actually means. No-bullshit coaching from someone who has been in this exact mess — without the corporate gloss."

**Weak description example:**
> "Coaching services for tech professionals looking to grow their career and reach their full potential."

The difference: the strong one names the person, names the problem, sounds like Val.

## Inclusion in meta descriptions

Never lead with "neurodivergent" or "queer" as the primary qualifier in a meta description — it signals to the broader audience that the service isn't for them. The pattern is: broad audience first, specialist support as additive.

**Right:** "No-bullshit coaching for engineering managers and folks in tech... specialist support for neurodivergent and queer people."
**Wrong:** "Coaching for neurodivergent and queer folks in tech who want more power and less bullshit." (excludes everyone else before they've read a word)

The folks-in-tech page is the exception — that page is explicitly for that audience, so leading with it is correct there.

## What to flag

- `description:` that's vague, jargon-heavy, or over 160 chars
- `title:` tags that don't contain a keyword (e.g. just "Coaching" or "Home")
- Missing `description:` front matter (will fall back to `_config.yml` site description — usually too generic)
- H1s that don't match search intent
- Pricing in structured data that has expired
- FAQ questions that are generic and would never be searched ("What is coaching?")
- Pages with no inbound internal links
- Blog posts where the title is a cute pun but unsearchable

## What to preserve

- Val's voice in meta descriptions — don't sand it down to SEO slop
- The existing structured data — it's solid, just needs keeping current
- The `jekyll-seo-tag` plugin setup — don't bypass it with manual tags
- The focus on specific audiences — resist making it more generic to "capture more searches"

## When writing or rewriting meta descriptions

Ask: would Val actually say this? Would the target person recognise themselves in it? If yes to both, it's right. If it sounds like it was written by an SEO agency, it's wrong.
