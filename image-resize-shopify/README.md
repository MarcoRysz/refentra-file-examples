# An image can be small in MB and still have too many pixels

Shopify's theme-image help lists two separate upload limits: **20 megapixels and
20 MB**. Its product/collection-image page lists **up to 5000 × 5000 pixels or
25 MP, and less than 20 MB**. Check the particular upload area; there is no single
pixel limit for every Shopify image field. Sources were read on **8 October 2026**:
[theme images](https://help.shopify.com/en/manual/online-store/images/theme-images),
[product media](https://help.shopify.com/en/manual/products/product-media/product-media-types).

Megapixels = width × height ÷ 1,000,000. Compressing the bytes alone does not
necessarily reduce those dimensions. This synthetic example lets you inspect both
quantities independently:

| File | Dimensions | Megapixels | Exact bytes |
| --- | --- | ---: | ---: |
| [Original synthetic grid](source-6000x4000.png) | 6000 × 4000 | 24 | 82,643 |
| [Actual downloaded output](output-4000x2666.png) | 4000 × 2666 | 10.664 | 244,764 |

The original is far below 20 MB but exceeds the theme-image pixel limit. The copy
has fewer pixels **and more bytes**. This demonstrates why file weight and pixel
count must be checked separately; it does not isolate a particular encoder cause
or predict what another photograph will do. Both files remain below 20 MB.

## How this copy was produced and checked

The original is an entirely synthetic, code-drawn grid with four orange corner
markers; it contains no customer data or real photograph. On 8 October 2026 it
was processed in the public French Refentra resizer, using the guide's preset:
width 4000, height 4000, **fit within maximum dimensions**, prevent upscaling,
input/output PNG. The browser filechooser event was unavailable in this operator
session; the tool's supported clipboard-paste route selected the same synthetic
input. The actual offered PNG was downloaded to the operator's local filesystem.

An independent Pillow decode confirmed its PNG signature, 4000 × 2666 dimensions,
244,764-byte size, and all four orange markers at their scaled positions. The
aspect ratio is retained with rounding down to whole pixels. The exact source and
output SHA-256 values are in [manifest.json](manifest.json).

This was one desktop in-app Chromium check. **No Shopify upload, theme preview,
mobile test or universal quality/compatibility result was performed.** Keep the
original; examine the copy and its format, byte size and actual display in your
Shopify upload area. Do not keep reducing an image which already meets its limits
without diagnosing the real error.

The full guide explains the separate limits and remaining failure cases:
[English](https://refentra.com/guides/shopify-image-too-large-under-20mb/),
[French](https://refentra.com/fr/guides/shopify-image-trop-grande-moins-20-mo/).
The measurements are specific examples, not guarantees of platform acceptance.

Published by Refentra's maker with AI/automated assistance. The files are original
synthetic examples and actual browser outputs; the website's application source
is not part of this resource. Publication is not evidence of traffic or adoption.
