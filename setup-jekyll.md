---
layout: default
title: Jekyll + GitHub Pages Setup Guide
---

# Jekyll + GitHub Pages Setup Guide

This guide walks through setting up a Jekyll site on GitHub Pages with GitHub Actions. For themes and Markdown specifics, see:

- [Themes Guide]({{ "/themes-guide/" | relative_url }})
- [Markdown Guide (In‑Depth)]({{ "/markdown-guide/" | relative_url }})

## 1) Create or use a GitHub repository

- Create a new repository or use an existing one.
- Push your site files (like this repo) containing `_config.yml`, `index.md`, and optionally `assets/`, `_includes/`, etc.

![1](/assets/flow/1.png)

## 2) Enable GitHub Pages (Settings → Pages)

1. Go to your repository on GitHub.
2. Open `Settings` → from the left sidebar, click `Pages`.
3. Under "Build and deployment → Source", select `GitHub Actions`.
4. Click the suggested Jekyll workflow (or create one) and commit it. This adds `.github/workflows/jekyll.yml`.
5. Wait for the Action to run. When it succeeds, your site will be published at the URL shown on the Pages screen.

![2](/assets/flow/2.png)
![3](/assets/flow/3.png)
![4](/assets/flow/4.png)

Notes:

- If you don’t see the suggested workflow, you can create it manually with the standard Jekyll Pages template from GitHub.
- Changes to your repo will trigger the workflow to rebuild and deploy your site.

## 3) Configure Jekyll (`_config.yml`)

Key fields to set:

```yaml
title: Your Site Title
description: Short description
url: "https://<your-gh-username>.github.io"
baseurl: "/<repo-name>" # empty for user/organization sites, set for project sites

# Theme (using GitHub Pages remote theme)
remote_theme: pages-themes/cayman@v0.2.0

plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-remote-theme
  - jekyll-include-cache

markdown: kramdown
highlighter: rouge
kramdown:
  input: GFM
  math_engine: mathjax
```

Tips:

- For a project site (repo like `username.github.io/repo`), set `baseurl: "/repo"` and use `{{ "/path/" | relative_url }}` for internal links.
- For a user/organization site (repo named `username.github.io`), leave `baseurl` empty.

## 4) Pick a theme

See the [Themes Guide]({{ "/themes-guide" | relative_url }}) for choosing an official theme, switching, and customizing via SCSS and layouts.

## 5) Create pages and links

- Create Markdown files at the repo root or inside folders (e.g., `about.md`, `docs/getting-started.md`).
- Use YAML front matter for title/layout.
- Link between pages using `relative_url` to respect `baseurl`.
- For Markdown syntax and kramdown features, see the [Markdown Guide]({{ "/markdown-guide" | relative_url }}).

## 6) Optional: Local preview (advanced)

If you want to preview locally:

1. Install Ruby and Bundler.
2. Add `Gemfile` with `jekyll` and required plugins.
3. Run `bundle install` then `bundle exec jekyll serve`.
4. Open `http://localhost:4000`.

For many teams, relying on GitHub Actions builds is enough.

---

## File Structure

Below is how common file paths map to final URLs. A folder with an `index.md` (or `index.html`) produces a clean trailing-slash URL. A single Markdown file at a path produces a `.html` URL (and is typically also reachable without the `.html`).

Project tree (excerpt):

```text
/
├─ index.md                  -> /
├─ about.md                  -> /about (also /about.html)
├─ test/
│  ├─ 1/
│  │  └─ index.md            -> /test/1/
│  ├─ 2/
│  │  └─ index.md            -> /test/2/
│  └─ 3/
│     └─ index.md            -> /test/3/
└─ powertrain/
   ├─ index.md               -> /powertrain/
   └─ m1/
      ├─ cascadia.md         -> /powertrain/m1/cascadia (also .html)
      └─ msd.md              -> /powertrain/m1/msd (also .html)
```

Equivalents and examples:

- `test/1/index.md` → URL: `/test/1/`
- `test/1.md` → URL: `/test/1.html` (also usually `/test/1`)
- Root `index.md` → URL: `/`
- `about.md` → URL: `/about.html` (also usually `/about`)

Pretty permalinks (optional):

```yaml
# _config.yml
permalink: pretty
```

Per-page permalink (overrides the default):

```yaml
---
title: Getting Started
permalink: /docs/getting-started/
---
```

Note: If your site is a project site with `baseurl: "/repo"`, the actual URL will be prefixed, e.g. `/repo/test/1/`.

---

## Troubleshooting

- Page 404s: Check `baseurl`, links using `relative_url`, and that the Action succeeded.
- Theme not applied: Verify `remote_theme` and that `jekyll-remote-theme` is listed in `plugins`.
- Build failures: Open the Actions run logs for error details.
- Call Brians 💀
