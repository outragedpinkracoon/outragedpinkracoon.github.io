# Outraged Pink Racoon — Website Design Brief v2

## The site
outragedpinkracoon.com — personal brand site for Valerie Dryden. Jekyll static site.

## Who this is for
Marginalised folks in tech — women, non-binary, queer, disabled, neurodivergent people — who are struggling, growing, or figuring out how to navigate a world that wasn't built for them. The site needs to feel like it was made for them, not for a generic tech audience.

## The brand
**Outraged Pink Racoon (OPR)** is the personal brand. The racoon is not a metaphor. She is just Val.

The tone is: warm but spiky. Funny but not fluffy. Colourful and alive. Feral in the best way. Absolutely not corporate.

---

## Visual Identity Direction

### The aesthetic
**Risograph print × Val's illustration style**

The entire visual direction is inspired by risograph printing — that distinctive textured, slightly-off-register, ink-on-paper quality with bold flat colours and visible grain. This matches Val's own illustration style directly: her artwork already lives in this world.

Think:
- Risograph zines and printed matter — flat bold colour, paper texture, slight ink bleed
- Screen printing aesthetic — limited colour palette, deliberate layering
- Independent illustration and editorial design — handmade, characterful, not slick
- The specific colours of risograph inks: fluorescent pink, teal, yellow, orange, purple, coral
- Val's own artwork: lavender racoon, magenta bat, orange frog, purple bunny, burgundy skeleton, dark lighthouse

The result should feel like: a beautifully printed zine made by a very talented feral racoon.

### What this is NOT
- Dark, gothic, moody (that was v1 — this is the opposite)
- Clean minimal tech site
- Corporate anything
- Flat design without texture
- AI-generated aesthetic
- Pastel and soft (it should be POPPY and saturated, not washed out)

### Colour palette
Complete rethink from the dark navy. Risograph-inspired, light, colourful, poppy.

| Role | Direction |
|------|-----------|
| Background | Warm cream / off-white — like uncoated risograph paper |
| Primary accent | Fluorescent pink / magenta — hero ink colour, non-negotiable, it's in the name |
| Secondary accent | Teal / sea green — classic risograph pairing with pink |
| Tertiary accent | Warm yellow or orange |
| Additional accent | Soft purple / lavender |
| Text | Near-black or very dark navy — never pure black, slightly warm or cool |

Colours should feel saturated and deliberate — like a limited ink palette. Not pastel, not neon-digital. Think: the specific slightly-muted-but-punchy quality of actual risograph inks.

Texture is essential — a subtle paper grain overlay should sit over everything. Backgrounds should feel like paper, not screens.

### Typography
- Display / headings: bold, characterful, with personality. Could lean condensed, could lean illustrated/hand-drawn, should feel like it belongs on a zine cover. NOT generic sans.
- Body: warm, readable, generous line height. Slightly editorial.
- Consider: a display font with illustration-adjacent energy paired with a clean readable body font.

### Texture and pattern
- **Paper grain** — subtle texture overlay on all backgrounds. Makes everything feel printed not digital.
- **Ink texture** — elements, borders, and shapes should feel like ink on paper, not perfect vector fills.
- **Off-register effects** — subtle misalignment or shadow in a second colour on display text or key elements. Classic risograph look.
- **Botanical/creature elements** — Val's illustrations used as decorative elements, section breaks, card images, hero characters. Should feel naturally placed, like they belong in the layout.
- **Pattern possibility** — a risograph-style repeat pattern using the racoon and supporting creatures could work as section backgrounds or decorative elements.

---

## Val's Artwork (available in `/assets/images/brand-images/`)

These illustrations exist and should be incorporated into the design. They already have risograph-compatible colour palettes — the site should feel like an extension of them.

### Full image inventory

| Filename | Description | Background |
|----------|-------------|------------|
| `raccoon-beret-baguette.jpeg` | Raccoon in striped top, red beret, holding baguette | Lavender |
| `raccoon-red-balloon.jpeg` | Same raccoon holding a red balloon | Lavender |
| `Me.png` | Photo of Val — profile picture | — |
| `bat-eating-grapefruit-pink-bg.jpeg` | Demon bat attacking a grapefruit | Hot magenta |
| `bear-bowtie-bakery.jpeg` | Dapper bear in bowler hat outside a bakery | White |
| `black-cat-halloween-pumpkin.jpeg` | Chaotic spiked black cat on a pumpkin | Teal |
| `carrot-potato-characters-orange-bg.jpeg` | Silly animated carrot and potato | Orange |
| `cat-milk-carton-orange-bg.jpeg` | Cat-shaped milk carton character | Orange |
| `claw-talon-red-purple-bg.jpeg` | Dramatic red claw/talon | Burgundy |
| `dark-bird-witch-hat-streetlamp.jpeg` | Moody bird in witch hat by a streetlamp | Black |
| `fluffy-monster-dragonfly-dark-bg.jpeg` | Gentle fluffy monster watching a dragonfly | Dark navy |
| `hedgehog-pinecone-creature.jpeg` | Hedgehog emerging from a pinecone | White |
| `lighthouse-butterflies-night.jpeg` | Lighthouse at night with butterflies in the beam | Dark navy |
| `monster-arms-outstretched-black-bg.jpeg` | Dramatic monster with arms outstretched | Black |
| `pig-face-allowed-to-be-a-lot.jpeg` | Pig face with text "I am allowed to be a lot" | Burgundy |
| `rabbit-ears-cracked-flower-pot.jpeg` | Tiny anxious bunny ears poking from cracked pot | Purple |
| `rose-pink-outline-dark-bg.jpeg` | White rose with hot pink outline | Dark navy |
| `skeleton-tuxedo-bouquet.jpeg` | Dapper skeleton in top hat holding roses | Burgundy |
| `teal-goat-creature-purple-bg.jpeg` | Teal goat-like creature with yellow flowers | Purple |
| `toad-jeans-smoking-pipe.jpeg` | Very chill orange toad in jeans with a pipe | Bright green |
| `vampire-woman-wild-hair.jpeg` | Haunting vampire woman, chalky linework | Dark navy |
| `wild-bird-scientist-glasses.jpeg` | Chaotic bird scientist reading intensely | White with teal/peach brush |

The raccoon is the primary character and should appear most prominently. All others can be used to add character and variety throughout the site.


## Layout and Structure

### Pages
1. **Homepage** (`/`) — hero with intro paragraph, four feature cards (Meet Val, Coaching, Holy Sh*t I'm A Manager, Stakeholders), recent blog posts
2. **Meet Val** (`/about-me/`) — full personal page with story, values, credentials, art gallery
3. **Coaching** (`/coaching/`) — coaching offering, who it's for, how it works, pricing, testimonials
4. **Blog** — archive of posts, category filtering
5. Future: HSIAM course page, Stakeholders landing page

### Navigation
`Home | Blog | Meet Val | Coaching | LinkedIn`
LinkedIn opens in a new tab (`target="_blank" rel="noopener noreferrer"`).

### Key components needed
- **Hero section**: large display type, tagline, CTA button
- **Feature cards**: four cards on homepage — should feel like zine panels or printed cards
- **Pricing cards**: two cards (single session £200, bundle of 3 £450), one featured
- **Testimonial blocks**: blockquote style, warm and characterful
- **Image gallery**: CSS grid, artwork images, no captions
- **Image pair**: side-by-side two images (racoon + photo of Val)
- **CTA button**: email mailto link, styled as proper button, hot pink/magenta
- **Book a coaching session**: primary CTA throughout

### Responsive
Must work on mobile. Display type should scale gracefully. Cards should stack on small screens.

---

## Custom CSS classes already in use

```
.image-gallery
.image-pair
.pricing-card
.pricing-card--featured
.pricing-badge
.pricing-amount
.pricing-title
.pricing-detail
.pricing-cta
.quote-author
.button
.card-grid
.card
```

Maintain these class names for compatibility with existing markdown content.

---

## Voice and tone (for any copy)

- Direct, warm, funny, a bit sweary (f*ck not fuck in public-facing)
- "Feral in the best way"
- Colourful and alive, not dark and brooding
- Tech-savvy but not corporate
- For the under-represented, by the under-represented
- Key phrases: "full-fat, no f*ck given self", "the ones who don't belong anywhere but thrive anyway", "highest performer and most overlooked", "someone actually in your corner"

---

## Reference and inspiration

- Risograph printing and zine culture — texture, flat colour, limited palette, paper feel
- Independent illustration and editorial design
- Val's own illustration style — the colour palettes in her artwork ARE the palette
- Screen printing aesthetic
- Colourful, poppy, handmade — think independent bookshop, art zine, illustrated poster

## The vibe in one sentence
A beautifully chaotic risograph zine, made by a feral racoon who also happens to be an excellent executive coach.