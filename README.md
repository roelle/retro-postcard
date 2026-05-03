# Retro Postcard Maker

A browser-based tool for making vintage-style "Greetings from…" postcards with 3D block letters, photo fill, and script text — all in a single HTML file, no server or build step required.

## [→ Open the app](https://roelle.github.io/retro-postcard/postcard.html)

Or download `postcard.html` and open it directly in Chrome or Firefox — no server, no install.

> **Stock images**: the tool can also auto-load images from a local `images/` folder when served over HTTP. Run `node serve.js` and open `http://localhost:3000` to use that.

## Features

- **3D block letters** with smooth bezier-extruded side faces and per-letter perspective sizing (letters grow larger left-to-right for the classic receding-road look)
- **Photo fill** clipped through letter shapes — one shared image, per-letter overrides, or none
- **Arc + diagonal baseline** with configurable radius and angle
- **Pacifico script** header and footer with italic shear, drop shadow, and independent baseline angle
- **Vintage aging filter** — matte, warmth, film grain, and vignette, each independently adjustable 0–1
- **Image loading** via drag-and-drop, file picker, or URL (paste any publicly accessible image URL)
- **Export** to SVG (vector, lossless) or PNG at 1×/2×/3× scale
- **YAML config** with live preview — every parameter is documented in-line; `Ctrl+Enter` to re-render, `Ctrl+/` to toggle comments

## Quick start

1. Open `postcard.html` in your browser
2. Edit the YAML on the left — change `text.lines`, pick colours, adjust angles
3. Drop in photos or paste image URLs to fill the letters
4. Hit **▶ Render**, then **↓ SVG** or **↓ PNG**

## Config reference

The YAML panel in the app is fully self-documented with inline comments. The main sections:

| Section | What it controls |
|---|---|
| `text` | Block letter content, position, kerning |
| `header` / `footer` | Script text above/below the block letters |
| `images` | Background photo, letter fill (shared or per-letter) |
| `style` | Fonts, sizes, colours, 3D depth, spacing, aging filters |
| `canvas` | Output dimensions |

### Images

Images can be referenced by filename after loading them into the tool. Three loading methods:

- **Drag & drop** onto the drop zone
- **File picker** — click the drop zone
- **URL** — paste any direct image link (e.g. a Wikimedia Commons file URL) into the URL field and press Enter

Once loaded, images appear as thumbnails and can be referenced by filename in the YAML.

**Per-letter images** — use `images.letters` with either a character-keyed object or a positional array:

```yaml
images:
  background: "sky.jpg"          # card background
  block: "mountains.jpg"         # same photo through all letters
  letters:
    S: "beach.jpg"               # override individual letters by character
    O: { file: "city.jpg", scale: 1.2, offset_x: -50 }
```

## Files

| File | Purpose |
|---|---|
| `postcard.html` | The entire app — open this in a browser |
| `serve.js` | Optional Node.js dev server for auto-loading local images |
| `images/` | Optional folder of stock images (used by `serve.js`) |

## Dependencies (loaded from CDN)

- [opentype.js](https://github.com/opentypejs/opentype.js) — glyph path extraction
- [js-yaml](https://github.com/nodeca/js-yaml) — YAML config parsing
- [Anton](https://fonts.google.com/specimen/Anton) and [Pacifico](https://fonts.google.com/specimen/Pacifico) fonts via jsDelivr

No npm, no build step, no backend.

## License

MIT
