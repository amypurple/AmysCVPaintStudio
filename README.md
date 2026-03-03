# Amy's CV Paint Studio

A retro-inspired pixel art editor that emulates the iconic ColecoVision graphics system (TMS9918A), built entirely as a single HTML file with no build steps required.

## Versions

| Version | Status | Description |
|---------|--------|-------------|
| [v1.8.1](v1.8/index.html) | **Latest** | Responsive Layout & Fluid Canvas — full-viewport layout, fluid non-integer canvas scaling, palette strip beside canvas, smooth sidebar scaling via clamp() |
| [v1.8.0](v1.8/index.html) | Previous | Brush & Airbrush — solid brush + time-based airbrush mode with density control |
| [v1.7.0](v1.7/index.html) | Previous | Animation Export & Curve — GIF / PNG sequence / sprite sheet export, Bézier curve tool |
| [v1.6.1](v1.6/index.html) | Previous | Touch & ICVGM — touch/stylus, two-finger pan, .dat import/export |
| [v1.5.0](v1.5/index.html) | Previous | Font & Code — Text tool, code export, compactor, stamps |
| [v1.1.1](v1.1/index.html) | Legacy | Animation — proven, production-ready |

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
- **Curve** *(v1.7+)* — Deluxe Paint-style quadratic Bézier; drag to set start→end, move to bend live, click to commit (C)
- **Select** — Area selection for copy/paste/stamp operations (S)
- **Fill Bucket** — Flood fill by tile row color (B)
- **Tile Stamp** — Capture and place single or multi-tile stamps (K)
- **Text** *(v1.5+)* — Type ColecoVision ROM font glyphs onto the canvas (T)
- **Brush / Airbrush** *(v1.8+)* — Solid round or square brush (radius 1–8 px) or airbrush scatter mode (density 10–100%, time-based rate); Mirror H/V supported (A)
- **Sprite Select** — Click and nudge sprites on canvas (M, visible when sprites loaded)

### Canvas Features
- **256×192 resolution** — Authentic ColecoVision/TMS9918A display dimensions
- **16-color palette** — Period-accurate TMS9918A colors; FG + BG per 8×1 tile row
- **Undo/Redo** — Full history (Ctrl+Z / Ctrl+Y)
- **Grid overlay** — Toggle 8×8 character grid (X)
- **Zoom mode** — 2× magnification with persistence (Z)
- **Crosshair guide** — Canvas alignment aid; toggle between system crosshair and custom gap-crosshair *(v1.7+)* (H)
- **Mirror drawing** — Horizontal and vertical symmetry (Shift+H / Shift+V)
- **Pan** — Space+drag to scroll canvas; two-finger pan on touch devices *(v1.6+)*
- **Touch & stylus support** — Full Pointer Events API, works on tablets and drawing tablets *(v1.6+)*
- **Color picker** — Sample colors from canvas (Alt+click)
- **Reference image** — Load translucent overlay with opacity slider
- **Tile Usage Heatmap** *(v1.3+)* — Color-coded duplicate tile overlay
- **3-tier collision overlay** *(v1.5+)* — Yellow/orange/red sprite collision visualization

### File Support

**Import:**
- `.pc` (pattern+color combined), `.pattern`, `.color`, `.grp`
- `.sc2` MSX Screen 2, `.sc4` MSX2/V9938 Screen 4 — identical tile encoding *(v1.5.1+)*
- `.pp` (10k and 40k variants)
- ZX Spectrum: `.scr`, `.mlt`, `.mc`, `.img`, `.gig`
- `.dat` ICVGM plain-text include (v2 GM1 + v3 GM2, with optional SATTR) *(v1.5.2+)*
- `.fcv` ColecoVision font file *(v1.5+)*
- `.cvstamp` multi-tile stamp *(v1.4+)*
- `.cvproj` full project snapshot
- PNG, JPG, GIF, BMP, WebP — with dithering engine
- Sprite sheet import (PNG/JPG → sprite patterns) *(v1.5+)*

**Export:**
- `.pc`, `.pattern`, `.color`, `.grp`, `.sc2`, `.pp`, `.png`
- `.dat` ICVGM plain-text include with optional SATTR sprite extension *(v1.6.1+)*
- `.fcv` ColecoVision font file *(v1.5+)*
- `.cvstamp` multi-tile stamp *(v1.4+)*
- `.cvproj` project snapshot
- Code export: CVBasic, C Header (SDCC), SJASMplus, WLA-DX, TNIASM *(v1.5+)*
- **Animated GIF** — full LZW compression, TMS9918A palette, infinite loop *(v1.7+)*
- **PNG Sequence** — one lossless PNG per keyframe packaged in a ZIP with meta.json *(v1.7+)*
- **Sprite Sheet** — all animation frames tiled side-by-side as one PNG + JSON *(v1.7+)*

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
- **Animation export** *(v1.7+)* — Animated GIF, PNG Sequence (ZIP), or Sprite Sheet from the Animation tab Export… dropdown
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

### v1.8.1 — 2026-03-02 — Responsive Layout & Fluid Canvas
- **Full-viewport layout**: app locks to browser height on screens ≥ 992px; mobile retains natural scrolling
- **Fluid canvas scaling**: canvas fills all available space at any non-integer scale; `image-rendering: pixelated` keeps pixels crisp; coordinate mapping via `getBoundingClientRect` was already scale-agnostic so drawing precision is unaffected
- **Palette strip** moved to a vertical column beside the canvas; height auto-tracks the canvas frame so Remap is always visible; swatches divide available height equally
- **Clear button** moved to toolbar as a compact icon-only delete button beside the scroll arrows
- **Sidebar compaction**: Filled/Outline toggle merged into pen-size row; Grid/Zoom/Crosshair/Mirror H/V/Cursor condensed into one 6-icon row; FG/BG Active heading removed
- **Smooth sidebar scaling via `clamp()`**: icons, padding, color boxes, and swatches scale continuously with viewport width; sidebar itself has fluid clamped width so it grows with the screen

### v1.8.0 — 2026-03-01 — Brush & Airbrush Tool
- **Brush tool** (A): solid filled stamp in round or square shape, radius 1–8 px; dragging uses `TOOLS.line()` interpolation to prevent gaps at fast movement speeds
- **Airbrush mode**: scatters random pixels within a circular radius; density slider 10–100%; driven by a `requestAnimationFrame` loop so the stamp rate is time-based — density is clearly visible at any movement speed, and the airbrush continues building up while held still (80 ms/stamp at 10% → 8 ms/stamp at 100%); behaves identically for mouse, touch, and drawing tablets regardless of device polling rate
- Mirror H / Mirror V support — same as pen tool

### v1.7.0 — 2026-03-01 — Animation Export & Curve Tool
- **Animated GIF export** (.gif): GIF89a with full variable-width LZW compression, TMS9918A 16-colour global palette, Netscape infinite-loop extension, frame delay from animation FPS setting
- **PNG Sequence export** (.zip): one lossless PNG per keyframe + meta.json, assembled as a PKZIP STORED archive with no external library
- **Sprite Sheet export** (.png + .json): all frames tiled side-by-side into a single wide PNG; companion JSON records frameCount, fps, frameWidth, frameHeight, layout
- **Curve tool** (C): Deluxe Paint-style quadratic Bézier; phase 1 drag sets start→end, phase 2 move bends the curve live with a visible yellow control point handle and tangent skeleton; click to commit, Escape cancels at any phase; respects pen size and FG/BG color
- **PLETTER compression** via Web Worker — no UI freeze during export
- **Cursor toggle** (H): switch between system crosshair and custom gap-crosshair; preference saved to localStorage
- Uniform modal backgrounds; Remap colour swatch border fix

### v1.6.1 — 2026-02-26 — ICVGM DAT Export
- **ICVGM `.dat` export** (File → Export .dat…): lossless tile deduplication via Compactor, GM2 MCOLOR format, optional SPATT section; optional SATTR sprite attribute extension (user warned that SATTR breaks ICVGM compatibility)
- **SATTR round-trip**: `.dat` files containing an SATTR section restore sprite positions on import
- `.sc4` accepted as alias for SC2 import — MSX2/V9938 Screen 4 has identical tile encoding; sprite section skipped; status message distinguishes formats *(also in v1.5.1)*
- ICVGM `.dat` import: v2 GM1 (32-byte COLOR expanded to 2048-byte MCOLOR) and v3 GM2; NAME table remapping; SPATT loaded to sprite pattern table *(also in v1.5.2)*
- **Touch screen & stylus support**: all mouse event listeners replaced with Pointer Events API (`pointerdown/pointermove/pointerup`); `setPointerCapture` keeps strokes on canvas edge; `touch-action:none` prevents browser gesture interference
- **Two-finger pan**: second pointer tracked via `_ptrs` Map; midpoint delta translates canvas in normal and zoom modes

### v1.5.0 — 2026-02-24
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

1. Open [index.html](index.html) in any modern browser — choose your version (v1.8 recommended)
2. Select foreground and background colors from the palette
3. Pick a drawing tool and start creating retro pixel art
4. On touch devices: draw with a single finger or stylus; two fingers to pan the canvas

### Keyboard Shortcuts (v1.8)

| Keys | Action |
|------|--------|
| P / E / S / B / T | Pen / Eraser / Select / Fill / Text |
| R / G / O / L / K | Rect / GridRect / Circle / Line / Stamp |
| C | Curve (Bézier) |
| A | Brush / Airbrush |
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
| **Curve tool active** | |
| Escape | Cancel curve at any phase |

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

Chrome/Edge 90+ · Firefox 88+ · Safari 14+ · iOS Safari 13+ (touch) · Android Chrome 90+

## Credits

**Amy's CV Paint Studio** by Amy Purple — a tribute to the golden age of 8-bit gaming.
Based on original Visual Basic tools by Daniel Bienvenu (NewColeco):
*Coleco Paint* v1.7.1 (July 2003) · *CV Dithering* (Nov 2005)

---

*Built with passion for retro computing. No frameworks, no build steps, just pure HTML.*
