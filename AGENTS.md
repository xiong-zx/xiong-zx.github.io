# Repository Guidelines

## Project Structure & Module Organization

This repository hosts a personal academic website built with Jekyll and the al-folio theme.

- `_pages/`: Markdown pages, including `about.md`, `publications.md`, and `cv.md`.
- `_data/` and `_bibliography/`: YAML profile data and BibTeX publication records.
- `_layouts/` and `_includes/`: reusable Liquid templates.
- `_sass/`, `assets/`, and `_scripts/`: styles, JavaScript, images, PDFs, and generated-script templates.
- `_plugins/`: Ruby build extensions; `_config.yml`: site configuration.
- `_posts/` and `_news/`: future blog posts and announcements; create content directories when needed. Their navigation is currently hidden.
- `.github/workflows/`: build, deployment, formatting, link, and accessibility checks. `_site/` contains generated output.

## Build, Test, and Development Commands

Run commands from the repository root:

- `docker compose pull` then `docker compose up`: recommended local preview at `http://localhost:8080`, with automatic rebuilding.
- `bundle install`: install Ruby dependencies for native development; Docker provides the required runtime without a native setup.
- `bundle exec jekyll serve --livereload`: native preview at `http://localhost:4000`.
- `JEKYLL_ENV=production bundle exec jekyll build`: production build into `_site/`.
- `npm install`: install formatting dependencies; no npm build or test scripts are defined.
- `npx prettier . --check`: repository formatting check. Use `npx prettier --write path/to/file` only on changed files.
- `pre-commit run --all-files`: run configured whitespace, YAML, and large-file checks when pre-commit is installed.

## Coding Style & Naming Conventions

Use two-space indentation for YAML, JavaScript, and SCSS; preserve surrounding Ruby and Liquid conventions. Prettier uses the Liquid plugin, a 150-character print width, and ES5 trailing commas. Keep Markdown front matter valid. Use descriptive filenames and `YYYY-MM-DD-title.md` for posts. Prefer small, direct changes, preserve the existing structure, and fix root causes without unnecessary abstractions.

## Testing Guidelines

There is no dedicated unit-test suite or coverage threshold. Validate changes with a production build and formatting checks. Preview affected pages at desktop and mobile widths; check navigation, images, publication links, and light/dark themes. Workflows provide Lychee link checks and manually triggered Axe accessibility checks.

## Commit & Pull Request Guidelines

History uses short descriptive subjects, such as `Update picture and hide template pages`; no enforced commit prefix is evident. Keep commits focused. PRs should explain the change, link applicable issues, record validation, and include screenshots for visual changes.

## Agent-Specific Instructions

Continue on the current branch unless explicitly asked to create another. Preserve unrelated edits. Do not commit generated output, logs, caches, or datasets. Use the OpenAI developer documentation MCP server for relevant OpenAI work.
