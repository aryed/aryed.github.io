# Google Sites to GitHub Pages cutover

Old site: <https://sites.google.com/view/aryedeutsch/>

New site: <https://aryed.github.io/>

## Technical migration status

- The site content and local assets have been rebuilt in maintainable Astro source.
- GitHub Actions deploys `main` to GitHub Pages.
- Each page publishes a canonical URL, description, and social-sharing metadata.
- The build publishes `robots.txt` and an XML sitemap.
- Google Analytics and Search Console verification are enabled when the matching GitHub repository variables are set.

## Old-to-new page map

| Google Sites path | GitHub Pages path |
| --- | --- |
| `/view/aryedeutsch/` and `/view/aryedeutsch/home` | `/` |
| `/view/aryedeutsch/non-math` | `/non-math/` |
| `/view/aryedeutsch/teaching` | `/teaching/` |
| `/view/aryedeutsch/photo-albums` | `/photo-albums/` |
| `/view/aryedeutsch/meta-math` | `/meta-math/` |
| `/view/aryedeutsch/archived-seminars/floer-homotopy-seminar` | `/seminars/floer-homotopy/` |
| `/view/aryedeutsch/lagrangian-tori-seminar` | `/seminars/lagrangian-tori/` |
| `/view/aryedeutsch/global-kuranishi-charts-seminar` | `/seminars/global-kuranishi/` |

Verify the three seminar source paths against the Google Sites page settings before using this table as a public migration notice.

## Manual cutover checklist

1. Keep the old Google Site published during the transition. Replace its homepage introduction with a prominent link to `https://aryed.github.io/`, and add the matching new-page link near the top of every old page. Google Sites does not provide page-level HTTP redirects.
2. In Google Analytics, reuse the existing GA4 property if historical continuity matters. Create or edit a web data stream for `https://aryed.github.io/`, copy its Measurement ID (`G-...`), and add it in GitHub under repository **Settings → Secrets and variables → Actions → Variables** as `PUBLIC_GA_MEASUREMENT_ID`.
3. In Google Search Console, add a URL-prefix property for `https://aryed.github.io/`. Choose the HTML-tag verification method, copy only the value of the tag's `content` attribute, and add it as the repository variable `PUBLIC_GOOGLE_SITE_VERIFICATION`.
4. Run the GitHub Pages deployment again after adding either variable. Verify the new Search Console property, then submit `https://aryed.github.io/sitemap-index.xml` in **Sitemaps** and inspect the homepage plus the principal pages with **URL Inspection**.
5. Do not use Search Console's Change of Address tool for this move. The old site is a path under `sites.google.com`, while that tool requires a domain-level source property and working redirects.
6. Update profiles, institutional pages, email signatures, CVs, and controlled external links to the new URL. Keep the old site and its migration links available for at least six months; a year is safer.
7. Optionally buy a personal domain before broadly advertising the new address. Configure it in GitHub Pages first, then at the DNS provider, enable HTTPS, update `astro.config.mjs` and `robots.txt`, and repeat the Search Console/Analytics URL setup. A personal domain makes future hosting changes much easier.
