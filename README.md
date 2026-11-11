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

## Galleries

The art gallery is at `/art/`, with links to Cara for more work. Its order,
layout and alt text live in `_data/art.json`; web-sized JPEGs live in
`assets/art/`. Each entry names a full image (`file.jpg`) and thumbnail
(`file-small.jpg`), their dimensions and a `landscape`, `portrait` or `half`
layout. Original artwork in `my_work/art/` is kept out of the published site.

Photography uses `_data/photos.json` and `assets/photos/`. Both galleries share
the photography stylesheet and keyboard-accessible image viewer.
