# Keegoid site mark

The **Tile K** is a solid indigo squircle with the K knocked out of it. It was
chosen over five alternatives because it is the only one that still reads at
16px, which is where a mark actually lives: favicons, tab strips, bookmarks.

`keegoid-tile.svg` is the source of truth. Everything else here is derived from
it, and the masthead inlines the same geometry in
`layouts/partials/header.html` so it can take its colours from CSS.

## Files

- `keegoid-tile.svg` — canonical mark, rounded corners, indigo on transparent.
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

ImageMagick on this machine has no librsvg delegate. Its fallback SVG renderer
silently drops stroked paths and will emit a blank indigo tile with no K, at a
plausible file size and with a success exit code. Draw with MVG primitives
instead, render at 1024px, and downsample:

```bash
magick -size 1024x1024 xc:none \
  -fill '#2B00A6' -stroke none -draw "roundrectangle 0,0 1023,1023 246,246" \
  -draw "stroke-linecap round stroke-linejoin round stroke-width 113 stroke #FFFFFF fill none path 'M 348,266 L 348,758'" \
  -draw "stroke-linecap round stroke-linejoin round stroke-width 113 stroke #FFFFFF fill none path 'M 717,266 L 430,512 L 717,758'" \
  /tmp/tile-1024.png
```

Coordinates are the SVG's 100-unit grid scaled by 10.24. Use `rectangle` in
place of `roundrectangle` for the iOS icon. Always open the output and look at
it before committing.

## History

The previous **Principal Node K** mark and the Keegoid LLC lockups were removed
from this repo on 2026-08-09 — the site no longer used them, and they were
carrying about 1.2 MB. They remain in git history and can be recovered with
`git show c7352f0:static/images/brand/<file>`.
