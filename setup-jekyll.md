---
layout: default
title: Jekyll + GitHub Pages Setup Guide
---

# Jekyll + GitHub Pages Setup Guide

This guide walks through setting up a Jekyll site on GitHub Pages with GitHub Actions, choosing a theme, and writing content in Markdown.

## 1) Create or use a GitHub repository

- Create a new repository or use an existing one.
- Push your site files (like this repo) containing `_config.yml`, `index.md`, and optionally `assets/`, `_includes/`, etc.

## 2) Enable GitHub Pages (Settings → Pages)

1. Go to your repository on GitHub.
2. Open `Settings` → from the left sidebar, click `Pages`.
3. Under "Build and deployment → Source", select `GitHub Actions`.
4. Click the suggested Jekyll workflow (or create one) and commit it. This adds `.github/workflows/jekyll.yml`.
5. Wait for the Action to run. When it succeeds, your site will be published at the URL shown on the Pages screen.

Notes:
- If you don’t see the suggested workflow, you can create it manually with the standard Jekyll Pages template from GitHub.
- Changes to your repo will trigger the workflow to rebuild and deploy your site.

## 3) Configure Jekyll (`_config.yml`)

Key fields to set:

```yaml
title: Your Site Title
description: Short description
url: "https://<your-username>.github.io"
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

## 4) Choose and customize a theme

- GitHub provides official themes (e.g., `cayman`, `minimal`, `slate`, `time-machine`).
- Set `remote_theme: pages-themes/<theme-name>@vX.Y.Z` in `_config.yml`.
- Add custom CSS in `assets/css/style.scss` and ensure it’s included by your layout or theme. Many Pages themes automatically load `assets/main.scss` or `assets/css/style.scss`.

Example SCSS header to ensure Jekyll processes it:

```scss
---
---
// Your custom styles here
```

## 5) Create pages and links

- Create Markdown files at the repo root or inside folders (e.g., `about.md`, `docs/getting-started.md`).
- Each page should start with front matter:

```yaml
---
layout: default
title: About
---
```

- Link between pages using `relative_url` to respect `baseurl`:

```md
[Setup Guide]({{ "/setup-jekyll/" | relative_url }})
```

## 6) Optional: Local preview (advanced)

If you want to preview locally:
1. Install Ruby and Bundler.
2. Add `Gemfile` with `jekyll` and required plugins.
3. Run `bundle install` then `bundle exec jekyll serve`.
4. Open `http://localhost:4000`.

For many teams, relying on GitHub Actions builds is enough.

---

# Markdown Essentials (used by Jekyll)

Markdown is a lightweight format for writing content. Quick reference:

## Headings

```md
# H1
## H2
### H3
```

## Emphasis

```md
**bold**
_italic_
~~strikethrough~~
```

## Lists

```md
- Item 1
- Item 2
  - Nested item

1. First
2. Second
```

## Links and images

```md
[Link text](https://example.com)
![Alt text](/path/to/image.png)
```

## Code

Inline code: `` `code` ``

Fenced blocks:

```md
```python
def hello():
    print("hi")
```
```

## Tables

```md
| Name | Value |
| ---- | ----- |
| A    | 1     |
```

## Blockquotes

```md
> Quoted text
```

## Task lists (GFM)

```md
- [x] Done
- [ ] Todo
```

## Math (via MathJax/kramdown)

Inline: `$x = a/b$`

Block:

```md
$$
E = mc^2
$$
```

---

## Troubleshooting

- Page 404s: Check `baseurl`, links using `relative_url`, and that the Action succeeded.
- Theme not applied: Verify `remote_theme` and that `jekyll-remote-theme` is listed in `plugins`.
- Build failures: Open the Actions run logs for error details.


