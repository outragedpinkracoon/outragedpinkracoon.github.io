# Outraged Pink Racoon

A basic Jekyll site, using the same Jekyll and plugins as the coaching site.

## Run locally

Use Ruby 3.1.4 (selected by `.tool-versions` if you use asdf).

```sh
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4000
```

Open http://127.0.0.1:4000. Jekyll rebuilds when content changes;
refresh the browser to see them. Restart the server after changing `_config.yml`.

## Build

```sh
bundle exec jekyll build
```

The generated site goes into `_site/`.

Edit `index.md` for the homepage, `_layouts/default.html` for the shared
HTML layout and `assets/css/main.css` for styles. Add Markdown pages with
YAML front matter to publish more pages. Dated posts go in `_posts/`.

## Reusing the CSS on another site

The styles are plain CSS, with no Jekyll or build-tool dependency. Load in order:

1. `assets/css/base.css`: portable box sizing, body reset, typography tokens,
   colours, keyboard focus, skip link, SVG direction icon and reduced-motion support.
2. A theme stylesheet: this site's `assets/css/theme.css` sets its dark/pink
   palette. Another site should supply its own values instead.
3. That site's layouts and components. `main.css` contains Pink Racoon's poster
   composition and footer, not a general-purpose page template. Heading sizes
   are scoped to the poster and gallery; the base leaves headings alone.

For example, load `base.css`, then your own theme:

```css
:root {
  --color-scheme: light;
  --color-background: #faf7f0;
  --color-text: #202020;
  --color-accent: #9b174e;
  --font-body: Arial, Helvetica, sans-serif;
  --font-editorial: Georgia, 'Times New Roman', serif;
  --font-display: Impact, 'Arial Narrow', Arial, sans-serif;
  --font-mono: monospace;
}
```

Check text and focus contrast with the new palette. Font tokens do not download
fonts; supply your own `@font-face` rules if required. The `.skip-link` needs a
matching content target, as shown in `_layouts/default.html`.

Galleries are optional: load `photography.css` for the layout and viewer,
`gallery-accents.css` for the frames and stripes, and `art.css` for Cara links.
They use the same theme tokens. Their image order, breakpoints and decorations
are curated for this site; reuse them deliberately. The interactive viewer
also needs `assets/js/photography.js` and the gallery/dialog markup.

## Galleries

The art gallery is at `/art/`, with links to Cara for more work. Its order,
layout and alt text live in `_data/art.json`; web-sized JPEGs live in
`assets/art/`. Each entry names a full image (`file.jpg`) and thumbnail
(`file-small.jpg`), their dimensions and a `landscape`, `portrait` or `half`
layout. Original artwork in `my_work/art/` is kept out of the published site.

Photography uses `_data/photos.json` and `assets/photos/`. Both galleries share
the photography stylesheet and keyboard-accessible image viewer.

## Search and sharing

Each page's front matter supplies its search title, description and social
preview image. `jekyll-seo-tag` renders these along with canonical URLs and
structured data; keep `url` in `_config.yml` set to the public HTTPS domain.

`jekyll-sitemap` generates `/sitemap.xml`. `/image-sitemap.xml` automatically
lists full-size images from the two gallery data files, so prepared images
stay out until added to a gallery. Both sitemaps are advertised in `/robots.txt`.

After publishing, submit `/sitemap.xml` and `/image-sitemap.xml` in Google
Search Console and inspect the homepage and both gallery URLs. Verification
and submission happen in the domain owner's account; a local build does not
submit the site or guarantee indexing.
