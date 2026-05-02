# Shared Agent Instructions

This repository uses `.claude` as the source of truth for project-specific agent guidance.

Codex should read and apply these files as shared project instructions:

- `.claude/claude.md` for collaboration style and task tracking
- `.claude/skills/site-pages.md` for the page and include index
- The relevant `.claude/skills/*/SKILL.md` file before doing matching work

## Skill Triggers

Use these Claude skills as Codex project skills:

- Copywriting, page copy, editing, voice, conversion copy: `.claude/skills/copywrite/SKILL.md`
- Page creation, page review, coaching page work: `.claude/skills/page/SKILL.md`
- Design, layout, visual polish, SCSS changes: `.claude/skills/design/SKILL.md`
- Blog posts from LinkedIn content: `.claude/skills/blog-post/SKILL.md`
- SEO review, meta descriptions, search intent, structured data: `.claude/skills/seo-review/SKILL.md`
- Accessibility audit, display modes, contrast, focus, semantic HTML: `.claude/skills/accessibility-audit/SKILL.md`
- Business strategy, offer architecture, positioning, pricing: `.claude/skills/strategy/SKILL.md`

If a task spans multiple areas, read the narrowest set of skill files needed. For page work, read the page skill first, then its referenced copywriting, design, and site-pages files.

## Shared Rules

- Keep `.claude/skills` as the canonical home for Val's site skills.
- Do not duplicate those files into a second skill tree unless the user explicitly asks.
- If a Claude skill mentions a Claude-only command such as `/copywrite`, interpret it as "read and apply the matching skill file."
- Treat `SKILL.md` casing as canonical when linking between skill files.
- Remember that Val has worked hard on this website and is making a big leap doing her own thing. Give useful, candid feedback, but be kind: critique the work, not Val; do not be cruel, dismissive, or needlessly harsh.
- After completing a task or sensible chunk of work, ask Val whether to commit it. If she says yes, make a clean commit for that chunk rather than letting unrelated changes pile up.
