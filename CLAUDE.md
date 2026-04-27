# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

griddy-docs is a unified documentation site that aggregates docs from multiple Griddy platform repositories into a single MkDocs Material site. It does not contain application code — only MkDocs configuration, a landing page, and theme overrides.

Docs from subprojects are pulled at build time via [mkdocs-multirepo-plugin](https://github.com/jdoiro3/mkdocs-multirepo-plugin), which clones each repo's `docs/` directory into a `temp_dir/` during `mkdocs serve` or `mkdocs build`.

## Commands

```bash
uv sync                  # Install dependencies
uv run mkdocs serve      # Serve docs locally (live reload at http://127.0.0.1:8000)
uv run mkdocs build      # Build static site into site/
```

There are no tests, linters, or formatters configured for this repo.

## Key Files

- `mkdocs.yml` — Site configuration, navigation, theme settings, markdown extensions, and **multirepo plugin config** (defines which repos/branches to pull docs from)
- `docs/index.md` — Landing page with card grid linking to each subproject's docs
- `overrides/` — MkDocs Material theme overrides (custom icons, templates)
- `pyproject.toml` — Python 3.14+, depends on `mkdocs-material` and `mkdocs-multirepo-plugin`

## Subproject Repos (docs pulled via multirepo plugin)

| Section in site | Source repo | Branch | Docs dir |
|---|---|---|---|
| griddy-sdk-python | Thistle-Grow-Software/griddy-sdk-python | master | docs/* |
| fbcm | Thistle-Grow-Software/fbcm | master | docs/* |
| griddy-archive-manager | Thistle-Grow-Software/griddy-archive-manager | main | docs/* |
| griddy-web-portal | Thistle-Grow-Software/griddy-web-portal | main | docs/* |

To change which docs are included or update branch targets, edit the `plugins.multirepo.repos` section in `mkdocs.yml`.

## Build Artifacts

- `site/` — Built static site (gitignored)
- `temp_dir/` — Cloned subproject docs created by multirepo plugin at build time (gitignored)
