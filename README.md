# Amy's CV Paint Studio

A retro-inspired pixel art editor that emulates the iconic ColecoVision graphics system (TMS9918A), built entirely as a single HTML file with no build steps required.

## Versions

| Version | Status | Description |
|---------|--------|-------------|
| [v1.5.0](v1.5/index.html) | Experimental | Font & Code Update — Text tool, code export, compactor, stamps |
| [v1.1.1](v1.1/index.html) | Stable | Animation Update — proven, production-ready |

Open [index.html](index.html) for the version selector landing page.

---

## Features

### Drawing Tools
- **Pen** — Freehand pixel-by-pixel drawing with smart FG/BG color logic (P)
- **Eraser** — Remove pixels with precision (E)
- **Rectangle** — Filled or outline rectangles (R)
- **Grid Rectangle** — Character-aligned rectangle (G)
- **Circle/Oval** — Circular and elliptical shapes, drawn from center (O)
- **Line** — Straight lines with brush-size support (L)
- **Select** — Area selection for copy/paste/stamp operations (S)
- **Fill Bucket** — Flood fill by tile row color (B)
- **Tile Stamp** — Capture and place single or multi-tile stamps (K)
- **Text** *(v1.5+)* — Type ColecoVision ROM font glyphs onto the canvas (T)
- **Sprite Select** — Click and nudge sprites on canvas (M, visible when sprites loaded)

### Canvas Features
- **256×192 resolution** — Authentic ColecoVision/TMS9918A display dimensions
- **16-color palette** — Period-accurate TMS9918A colors; FG + BG per 8×1 tile row
- **Undo/Redo** — Full history (Ctrl+Z / Ctrl+Y)
- **Grid overlay** — Toggle 8×8 character grid (X)
- **Zoom mode** — 2× magnification with persistence (Z)
- **Crosshair guide** — Canvas alignment aid (H)
- **Mirror drawing** — Horizontal and vertical symmetry (Shift+H / Shift+V)
- **Pan** — Space+drag to scroll canvas
- **Color picker** — Sample colors from canvas (Alt+click)
- **Reference image** — Load translucent overlay with opacity slider
- **Tile Usage Heatmap** *(v1.3+)* — Color-coded duplicate tile overlay
- **3-tier collision overlay** *(v1.5+)* — Yellow/orange/red sprite collision visualization

### File Support

**Import:**
- `.pc` (pattern+color combined), `.pattern`, `.color`, `.grp`
- `.sc2` MSX Screen 2 (with sprite support)
- `.pp` (10k and 40k variants)
- ZX Spectrum: `.scr`, `.mlt`, `.mc`, `.img`, `.gig`
- `.fcv` ColecoVision font file *(v1.5+)*
- `.cvstamp` multi-tile stamp *(v1.4+)*
- `.cvproj` full project snapshot
- PNG, JPG, GIF, BMP, WebP — with dithering engine
- Sprite sheet import (PNG/JPG → sprite patterns) *(v1.5+)*

**Export:**
- `.pc`, `.pattern`, `.color`, `.grp`, `.sc2`, `.pp`, `.png`
- `.fcv` ColecoVision font file *(v1.5+)*
- `.cvstamp` multi-tile stamp *(v1.4+)*
- `.cvproj` project snapshot
- Code export: CVBasic, C Header (SDCC), SJASMplus, WLA-DX, TNIASM *(v1.5+)*

### Sprite System
- Up to 32 sprites with 4-byte attribute table (X, Y, pattern, color+EC)
- 8×8 and 16×16 sprite sizes with undo for size toggle
- Sprite Editor modal: attribute table, pattern grid, pixel-level pattern editor
- Sprite import/export: `.sprpat`, `.sprattr`
- Multi-select, drag, nudge (Arrow keys / Shift for 8px jumps)
- Sprite sheet import to pattern table

### Sprite Animation
- **Keyframe timeline** — Capture/load/copy/delete frames (128-byte hardware snapshots)
- **Animation Mode** — Frame navigation, save, new, delete, play/stop directly on canvas
- **Record Mode** — Auto-capture on sprite drag for stop-motion workflow (`.` key)
- **Onion Skin** — Ghost overlay of previous frame at 35% opacity
- **`.cvproj`** — Saves/loads animation keyframes (backwards compatible)

### Text Tool *(v1.5+)*
- Full ColecoVision ROM font embedded (all 122 glyphs, $05–$7F)
- Click to anchor, type to insert at caret position
- Arrow keys navigate within text; Ctrl+Arrow moves the entire block by tile
- Enter splits line at caret; Backspace deletes (merges lines at column 0)
- Escape or tool switch commits text to tile data (Ctrl+Z to revert)
- Three alignment modes: Left / Center / Right
- **Solid BG** mode: glyph written with selected FG + BG colors
- **Transparent BG** mode (default): FG pixels only; non-glyph positions sample dominant existing tile color to preserve image underneath
- Special Characters picker ($05–$1F graphic glyphs)

---

## Changelog

### v1.5.0 — 2026-02-24 *(experimental)*
- **Text tool** (T): type ColecoVision ROM font glyphs directly onto the canvas; full caret navigation, multi-line, alignment, solid/transparent BG modes, special character picker
- **FCV font import/export** (Font menu): reads/writes ICVGM-format `.fcv` files; 40 standard char slots ($21–$2A, $30–$39, $40–$49, $4A–$53)
- **Multi-dialect code export** (was "Export CVBasic"): CVBasic, C Header (SDCC), SJASMplus, WLA-DX, TNIASM; Full Screen and Selection scopes; download extension auto-updates
- **Sprite sheet import** (Sprites → Import Sprite Sheet…): load PNG/JPG, pick tile size (8×8 or 16×16) and start pattern index; grid overlay preview
- **3-tier collision visualization**: yellow (2 sprites overlap pixel), orange (3+), red (5+ sprites on scanline = hardware dropout); transparent sprites correctly counted toward scanline limit
- **Dithering progress indicator**: status bar shows "COMPUTING DITHER…" / "CONVERTING…" during import
- **Zoom persistence**: zoom state saved to localStorage and restored on reload
- **Sprite size undo**: Ctrl+Z reverts 8×8 ↔ 16×16 toggle
- Navbar reorganised: Stamp and Font promoted to their own top-level menus
- Toolbar restructured: tool buttons in two balanced rows; sprite tool relocated to dedicated Sprite controls row shown only when sprites are loaded
- Redundant inline keyboard cheatsheet removed (About modal is now the single reference)

### v1.4.0 — 2026-02-24
- **`.cvstamp` export**: save current selection as binary + JSON multi-tile stamp file
- **`.cvstamp` import**: load stamp → activate multi-tile stamp tool with preview under cursor (zoom-aware)
- **Stamp Refinement modal**: toggle individual tiles transparent before placing
- **Auto-stamp from selection**: pressing K while a selection is active builds a stamp without exporting
- Stamp tool rebound from T → K (T reserved for Text tool)
- **Bug fix**: select tool — clicking without dragging no longer clears active selection; Escape clears it
- **Bug fix**: drag-and-drop file import no longer triggers a drawing action after the file loads

### v1.3.0 — 2026-02-21
- **Tileset Compactor** (Tools → Compactor…): deduplicate and merge similar tiles
  - Pattern tolerance (0–100%) → Hamming distance over 64 bits
  - Color tolerance (0–100%) → fg/bg mismatch penalty per row
  - Greedy cluster preview: green = canonical tile, pink = merged-away
  - Apply rewrites MODEL, pushes undo, re-renders canvas
- **Tile Usage Heatmap** (Tools → Heatmap): color-coded duplicate tile overlay
  - Red = unique tile, yellow = ×2–4, lime = ×5–15, green = ×16+
  - Usage count badge per tile; works in normal and zoom view

### v1.2.0 — 2026-02-21
- **CVBasic export** (Tools → Export CVBasic…): matching TMSColor output format
  - Full Screen: `MODE 1` + `DEFINE VRAM` (matches TMSColor `-b` output)
  - Selection: `MODE 0` + `DEFINE CHAR` + `SCREEN` name table (matches TMSColor `-t`)
  - Export-time exact deduplication: identical tiles share one char slot
  - Reserved chars $00 and $20 always skipped
  - `DATA BYTE` blocks in `$XX` hex format, 8 bytes per line, tab-indented

### v1.1.1 — 2026-01-31
- Replace all blocking `alert()` calls with `UI.setStatus()` status bar messages
- Add `cancelAnimationFrame` to dither preview slider to prevent stale renders
- Add explicit `parseInt(x, 10)` radix to all bare `parseInt()` calls
- Document animation record shortcut (Period key) in About modal

### v1.1.0 — 2026-01-31 — Animation Update
- **Sprite Animation Timeline** — Keyframe system with capture, load, copy, delete, playback
- **Animation Mode** — Canvas-integrated toolbar with frame navigation, record, play/stop
- **Record Mode** — Auto-capture keyframes on sprite drag for stop-motion animation
- **Onion Skin** — Ghost overlay of previous frame at 35% opacity
- **Inline Sprite Properties** — Edit pattern, Early Clock, color from sidebar
- **Tile Reuse Analyzer** — Highlights duplicate tiles with color-coded overlays
- **Pattern Editor Onion Skin** — Compare patterns while drawing
- **`.cvproj` Animation Support** — Project files save/load animation keyframes
- Circle/Oval now expands from click point as center
- Reference images follow the zoom viewport correctly
- 9-slice canvas frame with pixel-perfect rounded corners

### v1.0.0 — 2026-01-27 — Initial Release
- Drawing tools: Pen, Eraser, Rectangle, Grid Rectangle, Circle, Line, Select, Fill Bucket, Tile Stamp
- Brush-size selector, fill/outline toggle, crosshair guide, mirror buttons, spacebar panning
- Palette utilities with Remap Colors modal (canvas picking, swaps, global recolor)
- `.cvproj` project snapshots; reference image overlay with opacity slider
- Sprite workflow: `.sprpat`/`.sprattr` import/export, multi-select, drag/nudge, collision overlay
- Sprite Editor: card-based UI, Add/Sort, Pattern Grid + Pattern Editor tabs (draw/invert/flip/rotate)
- SC2 export auto-detects sprite data for embedding

---

## Getting Started

1. Open [index.html](index.html) in any modern browser — choose v1.1 (stable) or v1.5 (experimental)
2. Select foreground and background colors from the palette
3. Pick a drawing tool and start creating retro pixel art

### Keyboard Shortcuts (v1.5)

| Keys | Action |
|------|--------|
| P / E / S / B / T | Pen / Eraser / Select / Fill / Text |
| R / G / O / L / K | Rect / GridRect / Circle / Line / Stamp |
| M | Sprite Select (when sprites loaded) |
| Z / X | Zoom / Grid toggle |
| F / H | Fill-Outline / Crosshair toggle |
| Shift+H / Shift+V | Mirror Horizontal / Vertical |
| Ctrl+Z / Ctrl+Y | Undo / Redo |
| Ctrl+C / V / X | Copy / Paste / Cut |
| Alt+click | Color picker |
| Space+drag | Pan canvas |
| `.` (period) | Toggle animation Record Mode |
| **Text tool active** | |
| Arrow keys | Move text caret |
| Ctrl+Arrow | Move text block by 1 tile |
| Enter / Backspace | New line / Delete at caret |
| Escape | Commit text to canvas |

---

## Technical Specifications

| Property | Value |
|----------|-------|
| Canvas Resolution | 256 × 192 pixels |
| Color Depth | 16 colors (TMS9918A palette) |
| Character Grid | 32 × 24 tiles (8×8 pixels each) |
| Pattern Memory | 6,144 bytes |
| Color Memory | 6,144 bytes |
| Sprite Attributes | 128 bytes (32 sprites × 4 bytes) |
| Sprite Patterns | 2,048 bytes |
| Animation Keyframes | Up to 120 frames (128 bytes each) |
| Distribution | Single HTML file, no build steps |

## Browser Compatibility

Chrome/Edge 90+ · Firefox 88+ · Safari 14+

## Credits

**Amy's CV Paint Studio** by Amy Purple — a tribute to the golden age of 8-bit gaming.
Based on original Visual Basic tools by Daniel Bienvenu (NewColeco):
*Coleco Paint* v1.7.1 (July 2003) · *CV Dithering* (Nov 2005)

---

*Built with passion for retro computing. No frameworks, no build steps, just pure HTML.*