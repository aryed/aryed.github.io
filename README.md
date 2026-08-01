# Arye Deutsch's Personal Website

A modern, fast, and dependency-clean academic website built with **[Astro](https://astro.build/)** and hosted on **GitHub Pages**.

## Collaboration and project history

Codex and other coding agents should begin with [`AGENTS.md`](AGENTS.md). Google Antigravity enters through [`GEMINI.md`](GEMINI.md), which points to the same canonical instructions. Current decisions and follow-up work are tracked in [`PROJECT_STATUS.md`](PROJECT_STATUS.md), while detailed reconstruction notes live in [`docs/`](docs/).

## Project Structure

```text
.
├── .github/workflows/deploy.yml   # GitHub Actions automated deployment
├── public/images/                 # Site media & photos
├── src/
│   ├── components/                # Header and Navigation components
│   ├── layouts/                   # Master PageLayout wrapper
│   ├── pages/                     # Markdown pages (home, teaching, seminars, etc.)
│   └── styles/                    # Global CSS styling
└── astro.config.mjs               # Astro site configuration
```

## Local Development

```bash
# Install dependencies
npm install

# Start local dev server
npm run dev

# Build production static bundle
npm run build
```

## Automated GitHub Pages Deployment

Whenever changes are pushed to `main`, GitHub Actions automatically builds the Astro site and deploys it to GitHub Pages at [`https://aryedeutsch.com`](https://aryedeutsch.com). The repository's default `aryed.github.io` address redirects to the custom domain.

## Maintaining the site

Edit the source files under `src/` and keep production assets under `public/`. A normal update should be checked locally and then pushed to `main`:

```bash
npm.cmd run build
git diff --check
```

The GitHub Actions workflow runs the production build and deploys it after the push. Check the workflow result and open the live page after deployment.

### Pages and the sitemap

The `@astrojs/sitemap` integration generates the XML sitemap automatically during every production build. The live sitemap is:

[`https://aryedeutsch.com/sitemap-index.xml`](https://aryedeutsch.com/sitemap-index.xml)

You do not edit the sitemap by hand, and you do not need to resubmit the same sitemap to Google Search Console after every page addition, edit, or deletion. Search Console periodically recrawls a successfully submitted sitemap, and this site also advertises it in `public/robots.txt`.

Use Search Console when one of these applies:

- Submit `https://aryedeutsch.com/sitemap-index.xml` once for the new Search Console property, if it has not already been submitted.
- After adding an important new page, use **URL Inspection → Request indexing** if you want Google to discover it sooner.
- After a large URL/site restructure, or if the sitemap report shows an error, submit the existing sitemap again after the deployment succeeds.
- After moving a page, update internal links and navigation and provide a redirect/retirement plan for the old URL. For a page that should disappear from search, use Search Console’s removal tools only when immediate removal is necessary; otherwise let the deleted/redirected URL be recrawled.

Google’s guidance: [Sitemaps report](https://support.google.com/webmasters/answer/7451001) and [URL Inspection](https://support.google.com/webmasters/answer/9012289).

### Analytics and Search Console

The site uses the existing GA4 Measurement ID through the `PUBLIC_GA_MEASUREMENT_ID` GitHub Actions variable. Keep the new web stream associated with `https://aryedeutsch.com/`. The old Google Sites stream can remain available for historical data.

When reviewing Analytics reports that include both domains, filter or compare by the `Hostname` dimension with an exact value of `aryedeutsch.com`. Do not create a permanent Analytics data filter unless you intentionally want to discard future data from the old domain.

### Before accepting an AI-generated change

Ask the agent to read `AGENTS.md`, preserve unrelated work, run the build, and check the diff. Confirm that it has not removed the custom-domain setting, SEO metadata, sitemap integration, Analytics wiring, or the deployment workflow.
