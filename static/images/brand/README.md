# Keegoid — Alien Artifact identity

`keegoid-master.svg` is the canonical full lockup, traced from the approved September 12, 2026 original rather than hand-redrawn. The sibling accounting brand folder retains the original PNG, trace script, and silhouette verification (99.71% overall; 99.92% for d). Production paths require no font, network resource, or generative rebuild.

Rebuild from the sibling accounting repository with `./scripts/python brand/build.py`. This creates `keegoid-logo.svg`, PNG lockup, standalone `keegoid-tile.svg`, white-backed square app icon, 64px favicon, 180px Apple touch icon, SVG/ICO favicons, and the opaque 1200 × 630 social card. Legacy tile filenames remain stable for existing references, but contain the new design. The masthead uses the shared full logo instead of separately typeset lettering.

Use charcoal #16151B and indigo #2B00A6 on white. Rasterize SVG through librsvg, never ImageMagick's SVG renderer; use ImageMagick only to pack already-rendered PNG into ICO. Check the visual output, especially at small sizes.

The earlier Tile K design is retained in git history. No trademark-clearance claim is made.
