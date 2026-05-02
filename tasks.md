## Current Priorities

These tasks reflect the post-overhaul conversion review. Older positioning context now lives in `context/bio.md` and evidence/credentials live in `context/cv.tex`.

- [ ] **Coaching page** — add a clear "What it's like to work with me" section.
  - Cover how people start, likely via intro call or email.
  - Explain session format: single session, bundles, ongoing work, and whether anything async happens between sessions.
  - Show what Val actually does with clients: real situations, live decisions, people mess, strategy, career moves. Not theory.
  - Spell out what changes for the client after working together.

- [ ] **Fractional CTO page** — rewrite service framing so it is outcome-led, not service-led.
  - "Delivery transformation" should become "your team starts shipping predictably."
  - "Tech due diligence" should become "you stop making expensive bets blind."
  - "AI adoption" should become "you avoid wasting money chasing hype and make useful adoption stick."
  - "Culture and team assessments" should become "you find out whether the problem is people, process, tech, leadership, or incentives."

- [ ] **Fractional CTO page** — add proof-led case studies using `context/cv.tex`.
  - Doccla: Acting CTO, 60% cycle time reduction, 80% AI adoption, 50% ops cost reduction via ElevenLabs, ISO 27001/13485, zero-downtime cloud migration, £1m+ revenue unlocked, eNPS -50 to +64, defects down 40%, incidents down 50%.
  - Thirdfort: £1m+ annual saving, cycle time 24 days to 2 days, release lead time down 75%, 70% AI adoption, eNPS up 40%, ops costs down 25%.
  - Snyk: 55% cycle time reduction, FedRAMP readiness, $20m+ enterprise deals, incident resolution down 34%, eNPS 78, diversity up 55%, time-to-hire down 62%.
  - Zego: $30m+ microservices rebuild, cycle time down 60%, cloud spend down 23%, diversity up 60%, onboarding 14 days to 3 days.
  - Format: short "what I walked into / what was broken / what changed" blocks, not corporate case studies.

- [ ] **Who Is Val page** — add 2-3 mini war stories.
  - Keep them punchy and human.
  - Show the chaos Val has walked into rather than only saying she has seen it.
  - Use concrete examples from the CV where possible.

- [ ] **Core pages** — add 1-2 concrete client/coaching outcomes near testimonials or pricing.
  - Examples could include promotion, clearer roadmap, stabilised team, hard conversation handled, role transition navigated.
  - Use existing testimonials where possible, especially "promoted to Director of Engineering by September."
  - Avoid fluffy "clients feel empowered" language.

- [x] **Core pages** — standardise email CTAs.
  - Use one strong, plain CTA for email actions across the site: "Get in touch".
  - Keep navigation CTAs descriptive where they link to another page.
  - Keep the next step unmistakable without over-specific microcopy.

- [ ] **Pricing and engagement signal** — add light expectation-setting where uncertainty may block buyers.
  - Coaching already starts at £400, but make the path from first contact to booked session clearer.
  - Retainer should signal likely shape, cadence, and seriousness. Avoid leaving it as a vague "pricing on application" dead end.
  - Fractional CTO already says £1,600/day; add what a first conversation/scoping step looks like.

- [ ] **Blog** — connect high-performing posts to coaching/CTO enquiries with relevant CTAs.
  - Route new manager posts to `/coaching/engineering-managers/`.
  - Route burnout/career/power posts to `/coaching/folks-in-tech/`.
  - Route founder, AI, delivery, hiring, and org-chaos posts to `/fractional-cto/` or `/coaching/founders/`.
  - Add a stronger blog index CTA so readers know where to go next.

- [ ] **HTML cleanup** — replace smart quotes in HTML attributes on testimonial sections.
  - Fix `class=”testimonial-card”` / `class=”testimonial-grid”` in `pages/coaching-managers.md`.
  - Fix `class=”testimonial-card”` / `class=”testimonial-grid”` in `pages/coaching-folks-in-tech.md`.
  - Check rendered styling after the fix.

## Recently Completed

- [x] **Who Is Val** — full rewrite to lead with authority before identity.
- [x] **Coaching landing page** — refreshed intro copy to match messy, human, hard-parts positioning.
- [x] **Founders/CTOs page** — added ongoing retainer option.
- [x] **All coaching pages** — updated header strip to reflect dual Fractional CTO + Coach positioning.
- [x] **All coaching pages** — moved credentials earlier so trust lands before empathy.
