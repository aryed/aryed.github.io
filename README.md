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
