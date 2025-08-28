---
layout: default
title: Themes Guide (GitHub Pages + Jekyll)
---

# Themes Guide (GitHub Pages + Jekyll)

This page explains how to choose, apply, and customize themes with GitHub Pages and Jekyll.

## Theme options on GitHub Pages

1. Official GitHub Pages themes via `remote_theme` (recommended for Pages).
2. Custom remote themes from GitHub.
3. Local themes (requires building via Actions or locally).

## Using an official GitHub Pages theme

In `_config.yml`:

```yaml
remote_theme: pages-themes/cayman@v0.2.0

plugins:
  - jekyll-remote-theme
```

Popular official themes: `cayman`, `minimal`, `slate`, `time-machine`, `primer`. Use the same `pages-themes/<name>@version` format.

## Switching themes

- Change the `remote_theme` value and commit.
- The next GitHub Actions build will apply it automatically.

## Custom CSS overrides

Add or edit `assets/css/style.scss` (or `assets/main.scss`). Ensure it has the SCSS front matter so Jekyll processes it:

```scss
---
---
// Your custom CSS here
```

Common customizations:

- Typography (fonts, sizes, line-height)
- Colors (brand palette)
- Spacing/paddings for headings and sections
- Link styles and hover states

## Overriding theme layouts/partials

You can override theme HTML by adding files with the same name under your project:

- `_layouts/default.html` to adjust the base layout
- `_includes/head.html` or `_includes/head-custom.html` for metadata and assets

When a file exists locally, Jekyll uses it instead of the theme’s version.

## Navigation and structure

- Many themes don’t ship nav; you can add links manually in your layout or pages.
- Create a simple index page with links, or build a sidebar via includes.

## Assets: images, JS, and fonts

- Place images under `assets/` and reference with `{{ "/assets/img.png" | relative_url }}`.
- Load custom scripts in your layout or via includes.
- Use system fonts or host web fonts locally for best performance.

## Troubleshooting

- Theme not applied: ensure `jekyll-remote-theme` is enabled in `plugins` and `remote_theme` is correct.
- CSS not taking effect: confirm SCSS front matter and that selectors are specific enough.
- Layout not changing: verify your local `_layouts` file names match the theme’s.


