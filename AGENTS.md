# Shared Agent Instructions

This file is the repository-level handoff for Codex, Google Antigravity, and any other coding agent working on Arye Deutsch's personal website.

## Read first

Before changing the site, read:

1. `README.md` for the project structure and commands.
2. `PROJECT_STATUS.md` for the current state and known follow-up work.
3. Any relevant file in `docs/` for feature-specific history and evidence.

For the recovered Non math gallery, read `docs/non-math-gallery-recovery.md` before changing its markup, images, order, proportions, or responsive behavior.

## Project and source-of-truth rules

- The active repository is this directory. Treat Google Takeout exports and the old Google Sites website as reference material, not as working copies.
- Preserve the complete website: pages, text, images, navigation, direct-only pages, and outbound links.
- Keep source files maintainable. Do not reintroduce Google Sites runtime markup or generated platform code.
- When reproducing a historical visual layout, use evidence in this order: the still-live original page, Takeout assets/HTML, Git history, and only then visual inference.
- A manually composed image layout is content, not decoration. Do not replace one with a generic masonry, columns, or uniform-card layout unless Arye explicitly requests a redesign.
- Store required assets locally under `public/`; do not leave production pages dependent on the old Google Sites host.

## Change workflow

1. Inspect `git status` and preserve unrelated or unfinished changes from another agent.
2. Make the smallest focused change consistent with the existing Astro structure and CSS.
3. Run `npm.cmd run build` on Windows. Also run `git diff --check`.
4. For visual changes, inspect the rendered page at desktop and mobile widths. Check composition, cropping, ordering, missing assets, and horizontal overflow.
5. Update `PROJECT_STATUS.md` or the relevant document when the change affects architecture, historical reconstruction, or the task backlog.
6. Commit the focused change, push it to `main`, and wait for the GitHub Pages workflow to succeed. Arye expects completed website changes to be visible online for review.
7. Report the commit, deployment result, and live page URL.

Do not bundle unrelated existing changes into a commit merely to satisfy step 6. If the working tree contains another agent's work, isolate the intended files or coordinate before committing.

## Repository-specific commands

PowerShell may block `npm.ps1`; use `npm.cmd`:

```powershell
npm.cmd install
npm.cmd run dev
npm.cmd run build
```

If Git reports dubious ownership in this checkout, use:

```powershell
git -c safe.directory='D:/PersonalGoogleDrive/Personal website' <command>
```

Deployment is handled by `.github/workflows/deploy.yml` after a push to `main`.

