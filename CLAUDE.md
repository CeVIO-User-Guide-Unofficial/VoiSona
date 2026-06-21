# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a MkDocs-based documentation site — an unofficial Chinese translation of the VoiSona (formerly CeVIO Pro) user guide. The source content is translated from the official Japanese manual at manual.voisona.com.

## Commands

```bash
# Install dependencies
pip install mkdocs-material mkdocs-glightbox mkdocs-git-revision-date-localized-plugin

# Serve locally with live reload
mkdocs serve

# Build static site
mkdocs build
```

## Architecture

**`mkdocs.yml`** — single source of truth for site config, navigation, theme, plugins, and Markdown extensions. All nav structure is defined here; adding a page requires both creating the `.md` file and adding it to the `nav:` section.

**`docs/`** — all Markdown content, split into three sections:
- `docs/song/` — VoiSona Song (singing synthesizer) pages
- `docs/talk/` — VoiSona Talk (speech synthesizer) pages
- `docs/others/` — about, contact, website changelog

**`overrides/`** — Material theme customizations:
- `overrides/partials/footer.html` and `footer_link.html` — custom footer templates (Jinja2, replacing the default Material footer)
- `overrides/material/assets/stylesheets/extra.css` — custom admonition type `new` (yellow star icon, used to mark newly added content); also defines a `voisona` color scheme variable
- `overrides/material/assets/stylesheets/footer.css` — footer-specific styles

## Content Conventions

- All content is written in Simplified Chinese (zh).
- The `!!! new` admonition type (defined in `extra.css`) marks content that was newly added in a VoiSona release.
- Images for each section live alongside the docs in `docs/song/images/` and `docs/talk/images/`.
- `change-log.md` at the repo root contains the raw Japanese VoiSona release notes (untranslated); the translated website changelog lives at `docs/others/change-log-website.md`.

## Key MkDocs Plugins

- `glightbox` — lightbox for images (click to enlarge)
- `git-revision-date-localized` — shows page creation/modification dates from git history; committing new pages is necessary for dates to appear
- `pymdownx.keys` with custom `key_map` — maps `mouse-wheel-up-down` to a Chinese label
