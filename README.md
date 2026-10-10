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
