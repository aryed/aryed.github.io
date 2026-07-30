# Google Sites to GitHub Pages cutover

Old site: <https://sites.google.com/view/aryedeutsch/>

New site: <https://aryedeutsch.com/>

## Technical migration status

- The site content and local assets have been rebuilt in maintainable Astro source.
- GitHub Actions deploys `main` to GitHub Pages.
- Each page publishes a canonical URL, description, and social-sharing metadata.
- The build publishes `robots.txt` and an XML sitemap.
- Google Analytics and Search Console verification are enabled when the matching GitHub repository variable and secret are set.

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

1. In Cloudflare DNS, add four `A` records for `@`, pointing to `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, and `185.199.111.153`. Add a `CNAME` record for `www` pointing to `aryed.github.io`. Set all five records to **DNS only** initially, not Proxied.
2. After DNS resolves, enable **Enforce HTTPS** in GitHub under repository **Settings → Pages**. GitHub should redirect both `aryed.github.io` and `www.aryedeutsch.com` to `https://aryedeutsch.com`.
3. Keep the old Google Site published during the transition. Replace its homepage introduction with a prominent link to `https://aryedeutsch.com/`, and add the matching new-page link near the top of every old page. Google Sites does not provide page-level HTTP redirects.
4. In Google Analytics, keep the existing GA4 property and measurement ID for historical continuity. Change the web stream URL to `https://aryedeutsch.com/`; the deployed tag continues using the existing `PUBLIC_GA_MEASUREMENT_ID` repository variable.
5. In Google Search Console, add a **Domain property** for `aryedeutsch.com`. Add Google's supplied TXT verification record in Cloudflare DNS, then verify the property and submit `https://aryedeutsch.com/sitemap-index.xml` in **Sitemaps**. Inspect the homepage and principal pages with **URL Inspection**.
6. Do not use Search Console's Change of Address tool for the original Google Sites move. The old site is a path under `sites.google.com`, while that tool requires a domain-level source property and working redirects.
7. Update profiles, institutional pages, email signatures, CVs, and controlled external links to the custom domain. Keep the old Google Site and its migration links available for at least six months; a year is safer.
