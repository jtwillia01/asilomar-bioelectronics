# Logo source files

The organizers' canonical Illustrator masters, plus faithful SVG conversions. The site itself does **not**
load anything from this folder — it is here so the vector artwork lives with the project instead of in
someone's Downloads folder.

## What the site actually uses

| File | Where | Made from |
|---|---|---|
| `../logo-lockup.svg` | header, every page (48px tall) | `AsilomarLogo-B-orange.ai` |
| `../logo-lockup-white.svg` | footer, every page (60px tall) | same, recoloured `#cc6600` → `#ffffff` |
| `../favicon.svg` / `../favicon.png` / `../apple-touch-icon.png` | browser tab, iOS home screen | cypress silhouette from `AsilomarLogo-C-black.ai` on a `#cc6600` square |

Brand orange is **`#cc6600`**. The three artwork variants are: **A** hairline frame around the mark *and*
wordmark, **B** hairline frame around the mark only (widest, airiest), **C** solid filled box with the cypress
knocked out (boldest). The site uses B wherever the hairline frame can actually render, and C only at favicon
size where a hairline cannot exist.

## Two deliberate departures from the masters — tell the organizers

1. **Frame stroke thickened for screen.** B's frame is `stroke-width="3.367"` in a 506-unit viewBox, which
   computes to **0.32 CSS px** at the 48px header size — it renders as a pale grey ghost, so the "canopy breaks
   out of the frame" gesture disappears. The two web copies use `stroke-width="10.5"` (= 1.0px at 48px,
   1.24px at 60px). Nothing else is altered. To re-derive after a re-export:
   `sed -i '' 's/stroke-width="3.367"/stroke-width="10.5"/' logo-lockup.svg`
2. **The favicon's orange is reconstructed** — see defect 1 below.

## Two defects found in the supplied masters

1. **`AsilomarLogo-C-orange.ai` is not orange.** Its PDF content stream is byte-identical
   (sha1 `cbc8c467cc…`) to `AsilomarLogo-C-black.ai` — both contain only `0 0 0 rg` (black) and `1 1 1 rg`
   (white). The orange exists solely in Illustrator's private data, so every standard converter reads that file
   as black. The favicon therefore uses C's geometry recoloured to `#cc6600` by hand. **Ask the organizers to
   re-export C in orange** with "Create PDF Compatible File" checked.
2. **A stray white bar ships inside both A files.** A 949×80-unit opaque white rectangle sits at lower left and
   extends past the artboard:
   `<path transform="matrix(1,0,0,-1,0,684)" d="M905 49H-44V129H905Z" fill="#ffffff"/>`
   Invisible on a white page, a glaring white block on any coloured or dark background. It should be deleted
   from the master. (The older `Asilomar logo.ai` has the same problem.)

## Regenerating the SVGs from the .ai masters

The `.ai` files are PDF 1.5 underneath, so any PDF→SVG path works. What produced these:

```bash
pip3 install pymupdf
python3 -c "
import pymupdf
d = pymupdf.open('AsilomarLogo-B-orange.ai')
open('B-orange.svg','w').write(d[0].get_svg_image(text_as_path=True))"
```

`text_as_path=True` outlines the wordmark so the font is not needed. The conversions here were verified against
the source renders pixel-by-pixel (identical aspect ratios; differences confined to edge antialiasing).
