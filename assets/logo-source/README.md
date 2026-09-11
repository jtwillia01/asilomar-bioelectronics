# Logo source files

The organizers' canonical Illustrator masters, plus faithful SVG conversions. The site itself does **not**
load anything from this folder — it is here so the vector artwork lives with the project instead of in
someone's Downloads folder.

## What the site actually uses

| File | Where | Made from |
|---|---|---|
| `../logo-lockup.svg` | header, every page (48px tall, 162px wide) | `AsilomarLogo-C-black.ai`, box + wordmark recoloured `#cc6600` |
| `../logo-lockup-white.svg` | footer, every page (60px tall, 203px wide) | same, but the wordmark flipped to `#ffffff` for the pine background |
| `../favicon.svg` / `../favicon.png` / `../apple-touch-icon.png` | browser tab, iOS home screen | cypress silhouette from the same C artwork on a `#cc6600` square |

Brand orange is **`#cc6600`**. The three artwork variants are: **A** hairline frame around the mark *and*
wordmark, **B** hairline frame around the mark only (widest, airiest), **C** solid filled box with the cypress
knocked out — the "reverse tone" lockup. **The site uses C throughout**, chosen by Jonathan. A and B are kept
here for print and for anyone who wants the lighter lockup.

## Three deliberate departures from the masters — tell the organizers

1. **C's orange is reconstructed** — see defect 1 below.
2. **C is clipped to its box.** The master's cypress canopy (and a shape at lower left) extend *outside* the
   solid rectangle, painted opaque white. On a white page that is invisible, so the intended look is a tree
   contained by the box — but on the site's sand background (`#f6f3ec`) those strays show as faint ghosts. The
   web copies set the viewBox to the box bounds (`y 50 → 531`), which renders identically to the master on white
   and cleanly on sand. No path data is altered; nothing visible is removed.
3. **The footer wordmark is white, not orange.** Orange type on pine measures 3.47:1 and sinks into the
   background; white is 12.6:1. The box stays brand orange. This is a standard reversal treatment, but it is a
   colourway that does not exist in the supplied artwork.

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
