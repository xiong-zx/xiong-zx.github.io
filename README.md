# Zhixiao Xiong's Homepage

Personal academic website built with Jekyll and [al-folio](https://github.com/alshedivat/al-folio).

## Local preview

With Docker Desktop running:

```bash
docker compose up
```

Open <http://localhost:8080>. Content changes rebuild automatically. Stop with `Ctrl+C`; restart after changing `_config.yml`.

If the existing preview container is already running, use it directly. Manage it with `docker stop xiong-homepage-preview`, `docker start xiong-homepage-preview`, or `docker restart xiong-homepage-preview` after configuration changes.

## Content

- `_pages/about.md`: biography and homepage settings.
- `_data/cv.yml` and `assets/pdf/CV.pdf`: CV content and download.
- `_bibliography/my_papers.bib`: publications.
- `_data/socials.yml`: verified contact links.
- `assets/img/`: personal photographs.
- `_config.yml`: site settings and optional features.

Blog and News navigation is hidden until populated. Add posts to `_posts/YYYY-MM-DD-title.md` or announcements to `_news/`; enable the corresponding page's `nav` setting. Enable `announcements.enabled` in `_pages/about.md` to show news on the homepage.

## Validation and publishing

- `npm install` and `npx prettier . --check`: check formatting.
- `JEKYLL_ENV=production bundle exec jekyll build`: production build with native Ruby dependencies installed, or run inside the Jekyll container.
- `.github/workflows/deploy.yml`: publishes `_site/` to GitHub Pages after source changes are pushed to `main`.
- Keep generated output, caches, logs, and datasets out of commits.

## Optional features

Example articles and media have been removed. Small theme integrations for charts, mathematics, and media remain available; they load when enabled by their existing page or site settings. For example, set `chart: { plotly: true }` in front matter when adding a Plotly chart.

Use [upstream examples](https://github.com/alshedivat/al-folio/tree/main/_posts) or recover an old example with `git show HEAD:_posts_/2025-03-26-plotly.md`. After committing the cleanup, replace `HEAD` with the earlier revision `79bf853`.

The theme's MIT license and copyright notice are retained in `LICENSE`.
