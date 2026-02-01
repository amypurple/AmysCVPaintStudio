# Amy's CV Paint Studio

A retro-inspired pixel art editor that emulates the iconic ColecoVision graphics system, built entirely as a single HTML file with no external dependencies.

## Overview

**Amy's CV Paint Studio** is a fully-featured paint application that recreates the nostalgic 8-bit graphics experience of the ColecoVision era. Despite being a single [index.html](index.html) file, it packs impressive functionality for creating authentic retro artwork with period-accurate color palettes and resolution.

## Features

### Drawing Tools
- **Pen** - Freehand pixel-by-pixel drawing (Hotkey: P)
- **Eraser** - Remove pixels with precision (Hotkey: E)
- **Rectangle** - Draw filled rectangles (Hotkey: R)
- **Grid Rectangle** - Character-aligned rectangle tool (Hotkey: G)
- **Circle/Oval** - Create circular and elliptical shapes (Hotkey: O)
- **Line** - Draw straight lines (Hotkey: L)
- **Select** - Area selection tool for copy/paste operations (Hotkey: S)

### Canvas Features
- **256×192 resolution** - Authentic ColecoVision display dimensions
- **16-color palette** - Period-accurate color selection with foreground/background support
- **Undo/Redo** - Full history management (Ctrl+Z / Ctrl+Y)
- **Grid overlay** - Toggle 8×8 character grid for precise alignment (Hotkey: X)
- **Zoom mode** - 2× magnification for detailed work (Hotkey: Z)
- **Canvas scrolling** - Scroll in four directions

### File Support

**Import Formats:**
- Native `.pc` (pattern+color combined)
- `.pattern` and `.color` (separate pattern/color data)
- `.grp` files
- `.sc2` - MSX Screen 2 format (with sprite support)
- `.pp` files (10k and 40k variants)
- ZX Spectrum formats (`.scr`, `.mlt`, `.mc`, `.img`, `.gig`)
- Standard image formats (PNG, JPG, GIF, BMP, WebP) with dithering

**Export Formats:**
- `.pc` - Complete canvas data
- `.pattern` - Pattern data only
- `.color` - Color data only
- `.grp` - Graphics format
- `.sc2` - MSX Screen 2 (standard or with sprites)
- `.pp` - Picture format (10k/40k)
- `.png` - Modern image export

### MSX SC2 Sprite Support
- Load and display sprites from SC2 files
- Toggle sprite layer visibility
- Sprite Editor with attribute table and pattern grid viewer
- Export sprites as companion files (`.sprattr`, `.sprpat`)

### Sprite Animation
- **Keyframe-based timeline** – Capture sprite states as animation frames (128-byte snapshots, hardware-ready)
- **Animation Mode** – Edit animations directly on canvas with frame navigation, save, and playback
- **Record Mode** – Auto-capture frames on sprite drag for stop-motion workflow
- **Onion Skin** – See previous frame as ghost overlay while positioning sprites
- **Inline editing** – Change sprite pattern, color, and Early Clock from sidebar
- **.cvproj support** – Save/load animations with full project state

### Advanced Features
- **Drag & drop** - Simply drop image files onto the canvas
- **Dithering engine** - Convert modern images to retro palettes with multiple dithering algorithms
- **Color picker** - Sample colors directly from the canvas (Hotkey: I)
- **Clipboard support** - Cut, copy, and paste selections (Ctrl+X, Ctrl+C, Ctrl+V)

## Changelog

### v1.1 – January 31, 2026 – Animation Update
- **Sprite Animation Timeline** – Full keyframe-based animation system with capture, load, copy, delete, and playback controls in the Sprite Editor modal.
- **Animation Mode** – New "Anim" button reveals a canvas-integrated toolbar with frame navigation (prev/next), save frame, new frame, delete frame, and play/stop controls.
- **Record Mode** – Click Rec to auto-capture keyframes as you drag sprites; each mouse release creates a new frame for stop-motion style animation.
- **Onion Skin** – Toggle ghost overlay showing previous frame's sprites at 35% opacity while editing current frame.
- **Inline Sprite Properties** – When a single sprite is selected, edit Pattern #, Early Clock, and Color directly in the sidebar without opening the modal.
- **Tile Reuse Analyzer** – New tool (Tools menu) scans the canvas and highlights duplicate tiles with color-coded overlays and per-third statistics.
- **Pattern Editor Onion Skin** – Ghost overlay in the sprite pattern editor to compare with another pattern while drawing.
- **.cvproj Animation Support** – Project files now save/load animation keyframes (backwards compatible).
- **UX Improvements** – Unsaved changes indicator (●), undo/redo step counts, scroll button tooltips, improved sprite button tooltips.
- **Circle/Oval from Center** – Ovals now expand from click point as center rather than corner.
- **Reference Image Zoom** – Reference images now follow the zoom viewport correctly.
- **9-slice Canvas Frame** – Pixel-perfect 512×384 display with proper rounded corner frame.
- **Bug Fixes** – Sprite preview in 8x8 mode, pan direction, undo grouping for sprite operations, animation keyframe list display.

### v1.1.1 – January 31, 2026
- Replace blocking alerts with status bar messages
- Add cancelAnimationFrame to dither preview slider
- Add parseInt radix for safer parsing
- Document animation record shortcut (Period key)

### v1.0 – January 27, 2026 – Initial Release
- **Drawing & navigation** – Added Tile Stamp (T), Fill Bucket (B), brush-size selector, fill/outline toggle, crosshair guide, mirror buttons, and spacebar panning for faster layout work.
- **Palette utilities** – Remap Colors modal now supports canvas picking, swaps, and global recolors without repainting.
- **Reference & projects** – File menu gains `.cvproj` snapshots (patterns, colors, sprites) plus translucent reference image loading with opacity slider and clear control.
- **Sprite workflow** – Sprites menu handles `.sprpat/.sprattr` import/export, initialization, clearing, and exposes on-canvas sprite tools (multi-select, drag/nudge, collision overlay, layer dropdown, size toggle).
- **Sprite editor overhaul** – Card-based UI with Add Sprite, Sort by Y, Early Clock toggles, inline previews, drag-to-reorder, and new Pattern Grid + Pattern Editor tabs (draw/invert/flip/rotate).
- **SC2 export upgrade** – Saving `.sc2` now auto-detects when to embed sprite patterns, removing the separate “+ sprites” command.

## Getting Started

1. Open [index.html](index.html) in any modern web browser
2. Select a foreground and background color from the palette
3. Choose a drawing tool
4. Start creating retro pixel art!

### Quick Tips
- **Left-click** draws with the foreground color
- **Right-click** draws with the background color
- Use keyboard shortcuts for faster workflow
- Toggle the grid (X) to align artwork to 8×8 character boundaries
- Import existing images and let the dithering engine convert them to retro style

## Technical Specifications

| Property | Value |
|----------|-------|
| Canvas Resolution | 256 × 192 pixels |
| Color Depth | 16 colors (4-bit) |
| Character Grid | 32 × 24 tiles (8×8 pixels each) |
| Pattern Memory | 6,144 bytes |
| Color Memory | 6,144 bytes |
| Sprite Attributes | 128 bytes (32 sprites × 4 bytes) |
| Sprite Patterns | 2,048 bytes |
| Animation Keyframes | Up to 120 frames (128 bytes each) |
| Total Size | Single HTML file (~255KB) |

## Architecture

This application implements a complete retro graphics system using:
- **Canvas API** for rendering
- **Pattern/Color separation** - Authentic ColecoVision memory model
- **Character-based rendering** - 8×8 pixel tile system
- **Binary format support** - Read/write vintage file formats
- **No external dependencies** - Pure HTML/CSS/JavaScript

## Browser Compatibility

Works in all modern browsers supporting HTML5 Canvas and ES6:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

## Use Cases

- Create authentic 8-bit game sprites and backgrounds
- Design retro art with period-accurate limitations
- Convert modern images to ColecoVision-compatible graphics
- Export artwork for use in homebrew game development
- Learn about vintage graphics architecture

## Credits

**Amy's CV Paint Studio** by Amy Purple - A tribute to the golden age of 8-bit gaming.

---

*Built with passion for retro computing. No frameworks, no build steps, just pure HTML.*
