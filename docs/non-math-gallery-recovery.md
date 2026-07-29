# Non math Photo Gallery Recovery

Date recovered: 2026-07-30  
Live historical source: <https://sites.google.com/view/aryedeutsch/non-math>  
New page: <https://aryed.github.io/non-math/>  
Implementation commit: `a65fbc2`

## What had been lost

The photos themselves survived the Google Sites migration, but their composition did not. The original page was manually arranged as a sequence of asymmetric rows, a nested stack, and full-width landscapes. Later implementations treated the photos as a generic grid or CSS-columns masonry gallery. That retained the image files but changed:

- the order in which images appeared visually;
- which photographs were paired in each row;
- the relative width of each photograph;
- the portrait and panoramic crops;
- the transition from mixed rows to full-width landscapes.

This distinction matters: the arrangement and crop choices were part of the authored gallery.

## Evidence used

The still-live Google Sites page was the strongest source because it preserved both the selected images and the rendered composition. The recovery used three kinds of evidence from that page:

1. A full-page visual capture to identify the row groupings and focal framing.
2. The rendered bounding rectangle of every image to measure its position, width, and height.
3. Each image's rendered source URL and natural dimensions.

The repository and Takeout export were also inspected. They contained the original high-resolution photographs, but not enough maintainable layout information to reconstruct the manual composition reliably from the later Astro code. Git history showed the failed approximations: a regular grid and then CSS-columns masonry.

## Recovered composition

At the inspected 1280 px browser width, the old page's gallery content was 1154 px wide. Its measured layout was:

| Section | Left | Middle | Right | Structure |
| --- | ---: | ---: | ---: | --- |
| Row 1 | Mountain, 760 x 548 | — | Grape hyacinth, 365 x 548 | Approximately 8:4 |
| Row 2 | Dragonfly, 464 x 773 | — | Bee, 661 x 439, above butterfly, 661 x 309 | Approximately 5:7 with a nested right stack |
| Row 3 | Backlit flower, 464 x 619 | Dew flower, 365 x 618 | Rosebud, 266 x 618 | Approximately 5:4:3 |
| Row 4 | Soap bubble, 661 x 477 | — | Eye-like stone, 464 x 476 | Approximately 7:5 |
| Row 5 | Meadow, 1154 x 768 | — | — | Full width |
| Row 6 | Sea, 1154 x 526 | — | — | Full width panorama |
| Row 7 | Sunset, 1154 x 850 | — | — | Full width |
| Row 8 | Stars, 1154 x 685 | — | — | Full width |

The measured gaps on the original page were about 29 px. The rebuilt site uses `1.5rem` gaps so the rhythm stays close while fitting the new site's 1076 px content width. The column ratios come directly from the measured rectangles rather than generic integer guesses.

The separate climbing photograph above the gallery was also recovered from its rendered Google Sites crop.

## Why the rendered image variants were necessary

Several local Takeout images had very different aspect ratios from what appeared on the original page. Examples included:

- a landscape source cropped into the tall dragonfly portrait;
- landscape macro photographs cropped into the three narrow portrait cells;
- ordinary landscape sources cropped into the sea panorama and differently proportioned sunset/star images.

Google Sites served already-cropped JPEG variants whose natural dimensions matched the manually chosen boxes. Recovering those variants preserved the exact focal selections without guessing `object-position` values. They were downloaded and stored locally under:

`public/images/non-math/recovered/`

The production page therefore does not hotlink or depend on Google Sites. The earlier high-resolution files remain in `public/images/non-math/`; do not delete them casually, because they are the uncropped source photographs.

## Implementation

The gallery markup is in `src/pages/non-math.astro`. Instead of allowing an algorithm to flow all images, it explicitly represents the authored groups:

- `photo-gallery-row--8-4`
- `photo-gallery-row--5-7`, containing a nested `photo-gallery-stack`
- `photo-gallery-row--5-4-3`
- `photo-gallery-row--7-5`
- four full-width images

The corresponding rules are in `src/styles/global.css`. At widths up to 768 px, every composed row becomes one column in reading order. The recovered crops remain intact, so mobile does not need separate focal-position rules.

## Reusable recovery procedure

For another manually composed page or gallery:

1. Preserve the current repository and assets before changing anything.
2. Identify the strongest surviving source: live page first, then export/Takeout, then Git history or archives.
3. Capture the complete rendered page, not only its text or DOM outline.
4. Record every relevant image's source, natural dimensions, and rendered `x`, `y`, `width`, and `height`.
5. Group images by aligned coordinates. Look for nested stacks, unequal columns, full-width transitions, intentional gaps, and repeated heights.
6. Compare rendered aspect ratios with local source aspect ratios. If they differ, recover the historical crop or determine the focal position explicitly; do not assume `width: 100%; height: auto` is faithful.
7. Store recovered assets locally with stable, descriptive, ordered filenames.
8. Encode the composition explicitly with row/group markup and measured grid ratios. Avoid masonry or auto-placement when the evidence shows manual arrangement.
9. Add a simple responsive rule that preserves reading order and avoids horizontal overflow.
10. Build and inspect the new page visually at desktop and mobile widths. Also compare measured rectangles proportionally when possible.
11. Verify every referenced asset exists, run `git diff --check`, commit, push, and wait for deployment.

## Verification performed for this recovery

- Astro production build succeeded.
- Every image reference in the Non math page resolved locally.
- Desktop rendering reproduced the original row groupings, crops, sequence, and proportional widths.
- At a 390 px viewport, the gallery itself fit in one column without horizontal overflow.
- GitHub Pages successfully deployed commit `a65fbc2`.

