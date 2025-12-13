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
- **Canvas scrolling** - Shift your artwork by 1 or 8 pixels in any direction

### File Support

**Import Formats:**
- Native `.pc` (pattern+color combined)
- `.pattern` and `.color` (separate pattern/color data)
- `.grp` files
- `.pp` files (10k and 40k variants)
- Standard image formats (PNG, JPG, GIF, BMP, WebP) with dithering

**Export Formats:**
- `.pc` - Complete canvas data
- `.pattern` - Pattern data only
- `.color` - Color data only
- `.grp` - Graphics format
- `.pp` - Picture format (10k/40k)
- `.png` - Modern image export

### Advanced Features
- **Drag & drop** - Simply drop image files onto the canvas
- **Dithering engine** - Convert modern images to retro palettes with multiple dithering algorithms
- **Color picker** - Sample colors directly from the canvas (Hotkey: I)
- **Clipboard support** - Cut, copy, and paste selections (Ctrl+X, Ctrl+C, Ctrl+V)

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
| Total Size | Single HTML file (~25KB) |

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

**Coleco Paint Studio v12** by Amy - A tribute to the golden age of 8-bit gaming.

---

*Built with passion for retro computing. No frameworks, no build steps, just pure HTML.*
