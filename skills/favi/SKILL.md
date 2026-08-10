---
name: favi
description: >-
  Search free icon libraries and export favicon packages (SVG, ICO, apple-touch)
  via the public favi API at favi.joe-taylor.me. Use when the user wants a favicon,
  app icon, tab icon, PWA icon, or to pick/recolor an icon from Lucide, Tabler,
  Phosphor, Hugeicons, or Remix Icon without opening the UI.
---

# favi — favicon API skill

Prefer HTTP against the public API. Do not drive the browser UI unless the user asks for visual QA.

**Base URL:** `https://favi.joe-taylor.me`

Human UI: https://favi.joe-taylor.me  
Agent index: https://favi.joe-taylor.me/llms.txt

## Workflow

1. Search or look up an icon
2. Confirm `library`, `name`, and `style`
3. `POST /api/export` with color/shape options
4. Unpack the zip into the target project and wire HTML `<link>` tags if installing as a site favicon

## API

### Health

```bash
curl -sS https://favi.joe-taylor.me/api/health
```

### List libraries

```bash
curl -sS https://favi.joe-taylor.me/api/libraries
```

### Search icons

```bash
curl -sS "https://favi.joe-taylor.me/api/icons?q=image&library=lucide&style=outline&limit=12"
```

Query params: `q`, `library`, `style`, `limit` (1–300), `offset`.

Each hit includes `library`, `name`, `style`, and raw `svg`.

### Exact icon

```bash
curl -sS "https://favi.joe-taylor.me/api/icons/lucide/image?style=outline"
```

### Export favicon zip

```bash
curl -sS -X POST https://favi.joe-taylor.me/api/export \
  -H 'Content-Type: application/json' \
  -d '{
    "library": "lucide",
    "name": "image",
    "style": "outline",
    "bg": "#0f172a",
    "fg": "#ffffff",
    "fill": null,
    "stroke": "#ffffff",
    "padding": 0.18,
    "stroke_scale": 1.25,
    "shape": "rounded-square",
    "include_apple_touch": true
  }' \
  -o favicon.zip
```

Zip contains:

- `favicon.svg`
- `favicon.ico`
- `apple-touch-icon.png` (when `include_apple_touch` is true)
- `README.txt` (HTML snippet)

### Export body defaults

| Field | Default | Notes |
|-------|---------|-------|
| `bg` | `#0f172a` | Use `null` with `shape: "none"` for transparent plate |
| `fill` | `null` | Icon fill color; `null` / `"none"` = no fill |
| `stroke` | inherits `fg` | Icon stroke color; `null` / `"none"` = no stroke |
| `fg` | `#ffffff` | Legacy alias for `stroke` when `stroke` omitted |
| `padding` | `0.18` | 0–0.4 inset |
| `stroke_scale` | `1.25` | 0.5–3.0 |
| `shape` | `rounded-square` | `rounded-square` \| `circle` \| `none` |
| `include_apple_touch` | `true` | |

## Install into a web project

After export, unzip and follow the matching stack. Zip `README.txt` has the same snippets (and omits apple-touch lines when that file is not in the zip).

```bash
unzip -o favicon.zip -d /tmp/favi-favicon
```

### Vite

```bash
cp /tmp/favi-favicon/favicon.svg /tmp/favi-favicon/favicon.ico \
  /tmp/favi-favicon/apple-touch-icon.png web/public/
```

Add to `index.html` `<head>`:

```html
<link rel="icon" href="/favicon.svg" type="image/svg+xml" />
<link rel="icon" href="/favicon.ico" sizes="any" />
<link rel="apple-touch-icon" href="/apple-touch-icon.png" />
```

### Next.js (App Router)

- **`public/` + layout:** copy files into `public/`, add the same `<link>` tags in `app/layout.tsx`.
- **File-based metadata:** `app/icon.svg`, `app/favicon.ico`, `app/apple-icon.png` (from `apple-touch-icon.png`) — Next wires these automatically.

### Astro

Copy files into `public/`. Add the `<link>` tags in the layout head (e.g. `src/layouts/Layout.astro`).

### Generic HTML

Same files into the static/public root; same `<link>` tags in `<head>`.

Remove leftover default assets (e.g. `vite.svg`) if unused. Prefer the framework section that matches the target project.

## Choosing an icon

- Prefer exact names when known (`lucide` + `image` + `outline`)
- Otherwise search with a short `q`, skim the first page, then export
- Match library style names from `/api/libraries` (`outline`, `filled`, etc.)
- Keep contrast high for tiny favicon sizes (dark plate + light glyph is a safe default)

## Install this skill

```bash
npx skills add JoeBuildsStuff/favi
# or specifically:
npx skills add JoeBuildsStuff/favi --skill favi
```
