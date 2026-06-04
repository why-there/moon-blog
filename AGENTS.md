# AGENTS.md

This file provides guidance to Qoder (qoder.com) when working with code in this repository.

## Project Overview

This is “月亮加盐”, a personal blog built with Hugo and the [Hextra](https://github.com/imfing/hextra) theme (imported as a Hugo module via Go). Deployed to GitHub Pages at `https://why-there.github.io/moon-blog/`.

- **Hugo version**: 0.156.0 (extended edition required)
- **Go version**: 1.26
- **Theme**: `github.com/imfing/hextra` v0.12.3 (Hugo module, not a git submodule)

## Common Commands

```bash
# Tidy/resolve Hugo module dependencies (run after cloning or adding modules)
hugo mod tidy

# Start local dev server with live reload on port 1313
hugo server --logLevel debug --disableFastRender -p 1313

# Build production site (output to public/)
hugo --gc --minify

# Update the Hextra theme to the latest version
hugo mod get -u
hugo mod tidy
```

There are no test or lint commands configured for this project.

## Architecture

### How the theme works

Hextra is pulled in as a Hugo module declared in `go.mod` and referenced in `hugo.yaml` under `module.imports`. There is no local theme directory — all theme templates, assets, and layouts live inside the Go module cache. To override any theme template or partial, create the matching file path under the project root's `layouts/` directory (Hugo's lookup order takes precedence over module-provided templates).

### Content structure

Content follows Hugo's standard conventions:

- `content/_index.md` — site landing page (uses Hextra `cards` shortcode)
- `content/posts/` — blog articles; `_index.md` sets `cascade: type: blog` so all child pages inherit Hextra's blog layout
- `content/about.md` — standalone “关于” page (`type: about`)

Front matter uses YAML format delimited by `---`.

### Configuration

All site configuration is in `hugo.yaml`:
- Navigation menu items are defined under `menu.main`
- Hextra-specific settings (navbar, footer, edit URL) are under `params`
- Raw HTML in Markdown is enabled (`markup.goldmark.renderer.unsafe: true`)

### Deployment

- **GitHub Pages**: `.github/workflows/pages.yaml` builds with Hugo and deploys on push to `main`. The `--baseURL` is hardcoded to `https://why-there.github.io/moon-blog/` — update this if the repo is renamed or moved.
- GitHub Pages settings: ensure Source is set to “GitHub Actions” (not “Deploy from a branch”).

### Customisation entry points

| Goal | Where to act |
|---|---|
| Add/override a theme layout or partial | Create file under `layouts/` mirroring the theme's path |
| Add custom CSS/JS | Create `assets/css/custom.css` or `assets/js/custom.js` (Hextra convention) |
| Change site metadata, menu, or theme params | Edit `hugo.yaml` |
| Add a new content section | Create a new folder under `content/` with an `_index.md` |
| Use Hextra shortcodes (cards, tabs, callout, etc.) | Reference: https://imfing.github.io/hextra/docs/guide/shortcodes/ |
