# CLAUDE.md — FigureTracker

## Project Overview

FigureTracker is a client-side anime figure collection manager. It's a single-page web application that runs entirely in the browser with no backend — all data lives in `localStorage`.

**Live site**: Deployed via GitHub Pages from `main` branch.

## Repository Structure

```
├── index.html              # Main application (single-file SPA)
├── FigureTracker.html      # Older/alternative version
├── sample-figures.json     # Example seed data
├── README.md               # User-facing documentation
├── .github/workflows/
│   └── pages.yml           # GitHub Pages deployment
└── .nojekyll               # Disables Jekyll processing
```

The entire app is a **single HTML file** (`index.html`) with embedded `<style>` and `<script>` blocks. There is no build system, no package manager, and no bundler.

## Tech Stack

- **Vanilla JavaScript** — no frameworks, direct DOM manipulation
- **HTML5 / CSS3** — embedded in `index.html`
- **Chart.js 4.4.1** — loaded via CDN, used for analytics charts
- **localStorage** — data persistence (`figureTracker_v2`, `figureImages_v2`)

## Key Architecture

### Data Model

```javascript
DATA = {
  owned: [...],       // Figures in collection
  preorders: [...],   // Upcoming purchases
  hunts: { slug: { character, wished: [...] } },  // Per-character tracking
  wishlist: [...]     // Global wishlist
}
IMGS = { "tab_id": "base64_or_url" }  // Image storage
```

### Tab System

- `Owned` — main collection with filters (Type, Brand, Site)
- `Pre-orders` — upcoming figures
- `Wishlist` — global wish items
- Dynamic `Hunt` tabs — per-character wishlists with status tracking
- `Analytics` — spending charts and KPIs

### Important Functions

| Function | Purpose |
|---|---|
| `persist()` | Saves `DATA` to localStorage |
| `persistImgs()` | Saves `IMGS` to localStorage |
| `hydrate()` | Loads data on startup |
| `renderOwned()`, `renderPreorders()`, etc. | Re-renders specific tabs |
| `exportJSON()` / `importJSON()` | Backup/restore as JSON file |
| `esc(s)` | HTML-escapes user input (XSS prevention) |
| `imgKey(tab, id)` | Generates image storage key: `{tab}_{id}` |
| `huntSlug(name)` | Converts character name to slug: `"Zero Two"` → `"zero-two"` |

### Status Labels (Hunts)

- `R` = Received (Owned), `O` = Ordered (Pre-order), `W` = Wished, `B` = Bid

## Code Conventions

- **Variables/functions**: `camelCase`
- **Data object fields**: `PascalCase` (e.g., `Title`, `Brand`, `Character`)
- **Hunt slugs**: lowercase, hyphen-separated
- **All user-displayed text** must be escaped with `esc()` to prevent XSS
- **Images**: resized to max 300px, JPEG at 85% quality, stored as base64

## Development Workflow

### Running Locally

Open `index.html` in a browser. No server needed, though a local HTTP server avoids some browser restrictions:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Testing

No automated test suite. Test manually in the browser after changes. Key areas to verify:
- Adding/editing/deleting figures across all tabs
- Import/export round-trip
- Analytics chart rendering
- Image upload and display
- Sorting and filtering
- localStorage persistence across page reloads

### Deployment

Pushes to `main` trigger GitHub Actions (`.github/workflows/pages.yml`) which deploys to GitHub Pages automatically.

## Guidelines for AI Assistants

- **Single-file app**: All changes go into `index.html`. Don't split into separate files unless explicitly asked.
- **No build step**: Don't introduce bundlers, transpilers, or package managers.
- **No external dependencies**: Don't add npm packages. If a library is needed, use a CDN link.
- **Escape user input**: Always use `esc()` when rendering user data in HTML.
- **Persist after mutations**: Call `persist()` after changing `DATA` and `persistImgs()` after changing `IMGS`.
- **Maintain dark theme**: Use existing CSS variables (`--bg`, `--card`, `--text`, `--accent`, etc.).
- **Keep responsive**: The app uses CSS Grid and Flexbox for mobile support.
- **Match existing patterns**: Follow the modal-based form system for create/edit, event delegation for tabs, and the render function pattern for displaying data.
