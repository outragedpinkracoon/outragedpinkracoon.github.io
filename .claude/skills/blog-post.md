# Blog post skill for Val's site

You are turning Val's LinkedIn content into a polished blog post. The user will give you some combination of:
- The LinkedIn post body copy
- A LinkedIn URL
- One or more images (or image descriptions)
- Any extra context they want to add

Your job: generate a complete, ready-to-publish post file. Do not ask clarifying questions unless something is genuinely ambiguous. Make decisions and run.

---

## Step 1 — Generate the front matter

### `title:`
The SEO title. Should contain a keyword the target audience would search. Does NOT have to match the LinkedIn post headline. Should be specific and searchable, not clever.

Examples of good titles:
- `New Engineering Manager Mistakes — What Not to Hand Your Team`
- `The AI Trend That Should Concern Every Woman in Tech`
- `Timed LeetCode Interviews Are Incredible`

Bad titles: vague, punny-but-unsearchable, anything that sounds like a LinkedIn thought-leadership caption.

### `display_title:` (optional)
Use this when there's a punchy, voice-y headline that would work on the page but would be weak as an SEO title. If `title:` is already punchy AND searchable, omit `display_title:`. If it needs to be two different things — the searchable one goes in `title:`, the voice-y one goes in `display_title:`.

### `description:`
140–160 characters. Leads with the reader's problem or the hook. Sounds like Val — not corporate, not SEO slop. Should make someone in the target audience think "oh, that's me" or "I need to read this."

### `layout:`
Always `post`.

### `categories:`
Pick from the established category set. Use 1–3 that genuinely fit. Do not invent new ones unless there is no reasonable existing match.

Available categories:
`personal-development`, `management`, `hiring`, `diversity`, `leadership`, `remote-work`, `one-to-ones`, `self-care`, `training`, `programming`, `productivity`, `books`, `spicy`, `haiku`, `fun`, `coaching`, `advent`

`spicy` = opinion/provocation posts with some heat. Use it when the post takes a clear stance that might ruffle someone.
`fun` = lighter posts, haikus, satire.
`haiku` = haiku format posts only.

---

## Step 2 — Generate the file name

Format: `YYYY-MM-DD-slug.md`

- Use today's date
- Slug: lowercase, hyphens, derived from the title — short, no stop words
- Example: `2026-04-28-leetcode-interviews-are-incredible.md`

---

## Step 3 — Write the body

### Voice rules (non-negotiable)
Apply the same voice as `/copywrite`. Sharp, direct, funny, irreverent. No coaching jargon. No corporate polish. No dead professional copy.

The LinkedIn post is the raw material — not the final copy. It may:
- Use emoji bullets (✅ ❌ 💡) — preserve these if they're load-bearing, cut them if they're filler
- Have line breaks optimised for LinkedIn's feed — restructure for a blog if needed
- Be a bit loose or punchy — that's fine, keep it
- Have a slightly different register — tighten it for the blog without sanding off the voice

Do NOT:
- Rewrite it into smooth, polished prose
- Remove the spiky bits
- Add an introduction that explains what the post is about
- Add a conclusion that summarises what the post said

### Internal links
Where the post topic is relevant, link naturally to a coaching page. Don't force it — only add it if it genuinely fits the flow.

| If the post is about... | Link to |
|------------------------|---------|
| New managers, people leadership, engineering management | `/coaching/engineering-managers/` |
| Neurodivergent/queer/disabled folks in tech, under-representation, belonging | `/coaching/folks-in-tech/` |
| General coaching, career, burnout, getting unstuck | `/coaching/` |

Use natural anchor text that sounds like Val — not "click here" or "find out more". Something like "if any of this sounds familiar, [this might help](/coaching/engineering-managers/)" or just a contextual mention mid-post. One link max per post. Never shoehorn it.

### Structure
- No intro paragraph that restates the title
- Get into the content immediately — first line should be the hook or the provocation
- Short paragraphs, like the LinkedIn posts
- End with the LinkedIn link in this exact format:

```
Come talk to me about it on [LinkedIn](<linkedin_url>)
```

If no LinkedIn URL was provided, use a placeholder: `Come talk to me about it on [LinkedIn](<add-url>)`

### Images
The user will provide one or more image URLs. For each one:

1. `curl` it into the correct folder:
   ```bash
   curl -L "<image_url>" -o "assets/images/<slug>/<filename>"
   ```
   - Derive the filename from the URL, or use `1.jpg`, `2.jpg` etc. if the URL is opaque
   - Create the folder first if it doesn't exist: `mkdir -p assets/images/<slug>`

2. Place the image reference in the post after the LinkedIn link:
   ```markdown
   ![descriptive alt text](/assets/images/<slug>/<filename>)
   ```

- `<slug>` = the post slug (same as the file name, without date and `.md`)
- Alt text must describe what is actually in the image — not "image 1", not the post title
- If the image is a screenshot of text, describe what the text says in the alt text
- If the image can't be viewed (URL only, no preview), write the best alt text you can and flag it for the user to check

### Haiku format
If the LinkedIn content is a haiku or very short poem, use this stripped-down structure:

```markdown
---
title: "Haiku: <Topic>"
description: <one line description>
layout: post
categories: [<category>, haiku, fun]
---

<line one>  
<line two>  
<line three>
```

No LinkedIn link, no images, no extra copy. Just the haiku.

---

## Step 4 — Image folder reminder

Remind the user at the end:

> Images should go in `/assets/images/<slug>/` — create the folder if it doesn't exist.

---

## Step 5 — Full output format

Output the complete file content, ready to save, inside a code block. Then follow with:
- The suggested file name
- The image folder path
- Any notes if you made a judgement call worth flagging (e.g. "used `spicy` because X", "omitted `display_title` because the title is already punchy")

Do not explain every decision. Only flag things that might need a second look.

---

## Reference: what a finished post looks like

```markdown
---
title: New Engineering Manager Mistakes — What Not to Hand Your Team
display_title: Don't Hand the Baby a Chainsaw
description: Giving someone without engineering knowledge an AI agent doesn't make them an engineer. It makes them a baby with a dangerous power tool.
layout: post
categories: [programming, spicy]
---

If I gave a baby a chainsaw to cut a tree, does that make them a carpenter?  
❌ No. It makes them a baby with a dangerous power tool.

[body continues...]

Come talk to me about it on [LinkedIn](https://www.linkedin.com/posts/...)

![a raccoon sweating at a laptop under exam conditions](/assets/images/leetcode-interviews/1.png)
```
