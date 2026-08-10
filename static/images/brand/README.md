# Keegoid site mark

The **Tile K** is a solid indigo squircle with the K knocked out of it. It was
chosen over five alternatives because it is the only one that still reads at
16px, which is where a mark actually lives: favicons, tab strips, bookmarks.

`keegoid-tile.svg` is the source of truth. Everything else here is derived from
it, and the masthead inlines the same geometry in
`layouts/partials/header.html` so it can take its colours from CSS.

## Files

- `keegoid-tile.svg` — canonical mark, rounded corners, indigo on transparent.
- `keegoid-tile-square.svg` — same mark without the corner radius. Source for
  the iOS icon only; the geometry lives in SVG so it is never retyped in shell.
- `keegoid-tile-64.png` — 64px PNG icon for browsers without SVG favicon support.
- `keegoid-touch-icon.png` — 180px iOS home-screen icon. **Square, no rounding,
  fully opaque**: iOS applies its own corner mask, and any transparency is
  composited onto black.
- `keegoid-og-card.png` — 1200x630 social card, mark centred on white. Opaque —
  transparent PNGs flatten to black on X, Facebook and iMessage.
- `../../favicon.svg` — favicon. Lifts the tile to `#6D4DF6` under
  `prefers-color-scheme: dark` so it does not sink into a dark tab strip.
- `../../favicon.ico` — 48/32/16 fallback.

## Colour

The mark is `#2B00A6`, the same indigo as the site's links — the palette is
deliberately a single accent. The knocked-out K is the page ground, so in the
masthead it is `var(--bg)` rather than a hardcoded white.

## Regenerating the rasters

Rasterise with `rsvg-convert` (`brew install librsvg`), never with `magick`
directly. **`magick tile.svg out.png` renders a blank indigo tile with no K** —
it uses its internal MSVG coder, which drops stroked paths, and it does this
even when librsvg is installed, and even via the explicit `magick rsvg:` prefix.
It exits 0 and writes a plausible file size, so the failure is silent.

```bash
B=static/images/brand
rsvg-convert -w 64  -h 64  $B/keegoid-tile.svg        -o $B/keegoid-tile-64.png
rsvg-convert -w 180 -h 180 $B/keegoid-tile-square.svg -o $B/keegoid-touch-icon.png
rsvg-convert -w 256 -h 256 $B/keegoid-tile.svg        -o /tmp/tile-256.png
rsvg-convert -w 380 -h 380 $B/keegoid-tile.svg        -o /tmp/tile-380.png

# magick is still fine for compositing and .ico packing — just not for SVG input
magick -size 1200x630 xc:'#FFFFFF' /tmp/tile-380.png -gravity center -composite \
  $B/keegoid-og-card.png
magick /tmp/tile-256.png -define icon:auto-resize=48,32,16 static/favicon.ico
```

Open the output and look at it before committing.

## History

The previous **Principal Node K** mark and the Keegoid LLC lockups were removed
from this repo on 2026-08-09 — the site no longer used them, and they were
carrying about 1.2 MB. They remain in git history and can be recovered with
`git show c7352f0:static/images/brand/<file>`.
