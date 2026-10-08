# Synthetic file examples and measured outputs

These inspectable examples cover two different file-preparation problems:

- [An image under 20 MB can still exceed Shopify's pixel limit](image-resize-shopify/README.md).
  Synthetic input plus an actual downloaded PNG; fewer pixels can still mean more bytes.
- [Why a PDF can stay almost the same size](#why-a-pdf-can-stay-almost-the-same-size).
  Original PDFs and independently checked lossless/lossy examples below.

## Why a PDF can stay almost the same size

“Compress PDF” can mean cleaning the file structure or changing embedded images.
Those operations can produce very different results. These examples let you
inspect the difference yourself, including the actual copies returned by
[Refentra's PDF compressor](https://refentra.com/tools/compress-pdf/).

[Download the synthetic examples and actual outputs](pdf-compression-demo.zip)
(about 9.3 MB). The ZIP contains five PDFs, a README and an exact byte/hash manifest.
No customer information is included. The greenhouse photograph is AI-generated.

| File | Bytes | Embedded photo |
| --- | ---: | --- |
| Original photo + selectable text/vector PDF | 4,397,793 | PNG-derived, Flate, 1536 × 1024 |
| Lossless clean-up output | 4,397,274 | Same photograph bytes |
| Balanced output | 336,783 | JPEG, 1536 × 1024 |
| Smallest file output | 209,405 | JPEG, 1400 × 933 |
| Compact text/vector source | 1,990 | No photo; lossless offered no smaller download |

The lossless photo example saves **519 bytes**, so both sizes round to 4.2 MB in
the tool. Almost all original bytes belong to the separately embedded photo.
Balanced changes that image's encoding. Smallest file also reduces its resolution.
All three photo outputs were produced from the same original, not from repeated
lossy compression of an earlier output.

The larger saving is specific to this **PNG-derived artificial photograph**.
Already compressed JPEGs, unsupported images, masks and other documents can behave
differently. These examples do not guarantee a chosen size, portal acceptance or
unchanged image quality.

Before sharing a copy, open it and inspect its pages, text and important details.
Keep the original. At equal crop/display scale, Balanced changes are subtle here;
Smallest file adds modest softening of fine detail. There is no dramatic damage in
these examples. Choosing the smallest number is a tradeoff.

The actual outputs were observed on 7 October 2026 in the hosted browser tool.
Independent pypdf and PDFium reads found exact unchanged text, page count and
geometry. At 144 dpi, rendered pixels outside the photograph match the original.
The lossless whole-page render and photograph bytes also match. This is one
bounded inspection, not a universal correctness certificate. Image encoding can
vary between browsers/versions. The offered output Blob was read back; physical
OS saving and external portal acceptance were not tested.

Primary explanations of the mechanism:
[Adobe PDF optimization settings](https://helpx.adobe.com/uk/acrobat/desktop/create-documents/optimize-pdfs/pdf-optimizer-settings.html),
[Adobe space audit](https://helpx.adobe.com/ca/acrobat/desktop/create-documents/optimize-pdfs/audit-space.html),
[Ghostscript PDF optimization](https://www.ghostscript.com/blog/optimizing-pdfs.html).

Published by Refentra's maker as tutorial companion material. The synthetic asset
and accompanying material were assembled with AI/automated assistance; file
measurements come from actual outputs and independent readers.

ZIP SHA-256: `750617b868cbc4801ced2002e0acc118ac944f03dba24fd20628acfa7848bbdb`.
