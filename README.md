# blog.haeusler-wein

Jekyll + GitHub Pages blog at <https://blog.haeusler-wein.ch>. German posts about
the Rebberg «Auf Offenburg» and experiments with AI in viticulture.

## Structure

- `_posts/` — published posts (`YYYY-MM-DD-title.md`)
- `_drafts/` — work in progress (not built on the live site)
- `_layouts/` — `default.html` (shell) and `post.html`
- `assets/` — `styles.css`, images
- `_config.yml` — site config and plugins

## Local preview

Requires **Ruby 3.x** (the macOS system Ruby 2.6 is too old). Install a current
Ruby first, e.g. `brew install ruby` or via rbenv.

```sh
bundle install
bundle exec jekyll serve --drafts   # http://localhost:4000, includes _drafts
```

Without `--drafts`, drafts are excluded — same as the live site.

## Deploy

Push to `main`. GitHub Pages builds and deploys automatically (its build uses a
modern Ruby, independent of your local version).
