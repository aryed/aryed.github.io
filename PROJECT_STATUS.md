# Project Status

Last updated: 2026-07-30

## Current site

- Canonical live site: <https://aryedeutsch.com/>
- GitHub Pages fallback: <https://aryed.github.io/> (redirects to the canonical domain)
- Repository: `aryed/aryed.github.io`
- Branch deployed by GitHub Pages: `main`
- Framework: Astro 7, producing a static site in `dist/`
- Shared styling: `src/styles/global.css`
- Deployment workflow: `.github/workflows/deploy.yml`

## Established decisions

- This repository is the active, editable website. Google Takeout and the old Google Sites site are historical/reference sources.
- Keep the site as ordinary maintainable Astro, HTML, and CSS rather than generated Google Sites markup.
- Preserve all existing pages and assets. `Meta math` remains directly accessible but intentionally absent from public navigation.
- Completed website changes should be built, committed, pushed to `main`, and checked through the Pages deployment so Arye can review them online.
- Historical/manual visual compositions should be reconstructed explicitly rather than approximated with generic layout algorithms.

## Recently completed

- Migrated the full Google Sites export and rebuilt it as a clean static website.
- Migrated the site to Astro with automatic GitHub Pages deployment.
- Added light/dark theme support and repaired page rendering issues introduced during the migration.
- Recovered the original Non math photo gallery's image crops, ordering, and asymmetric composition. See `docs/non-math-gallery-recovery.md` and commit `a65fbc2`.
- Recovered original favicon from historical Google Site and configured standard PNG and ICO favicons in layout headers.
- Added the GitHub Pages cutover layer: canonical and social metadata, XML sitemap, `robots.txt`, and repository-variable hooks for Google Analytics and Search Console verification. See `docs/google-sites-cutover.md`.
- Configured `aryedeutsch.com` as the GitHub Pages custom domain and updated canonical URLs, sitemap output, and migration guidance.
- Upgraded framework to Astro 7 (`^7.1.6`) stable production release line, resolving Dependabot security alerts and verifying clean static site builds.

## Known follow-up work

These are candidates for future work, not authorization to change the site without a request.

1. Fix the mobile header/navigation overflow. During gallery QA at a 390 px viewport, the page content fit correctly but the header extended horizontally.
2. Perform a page-by-page visual preservation audit against the still-live Google Sites version, prioritizing layouts that were manually composed.
3. Complete the manual Google Sites, Analytics, and Search Console cutover checklist in `docs/google-sites-cutover.md`.

## Documentation map

- `AGENTS.md`: operating rules shared by Codex, Antigravity, and future agents.
- `GEMINI.md`: Antigravity entrypoint that delegates to the canonical `AGENTS.md` rules.
- `README.md`: project overview, structure, and local commands.
- `docs/non-math-gallery-recovery.md`: detailed recovery evidence, method, implementation, and reusable procedure.
- `docs/google-sites-cutover.md`: URL map and manual Google/SEO migration checklist.
