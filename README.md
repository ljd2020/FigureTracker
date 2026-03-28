# FigureTracker

A client-side anime figure collection manager. Track what you own, monitor pre-orders, plan wishlists with character hunts, and visualise your spending — all stored locally in your browser with no account required.

---

## Features at a Glance

| Feature | Description |
|---|---|
| Owned collection | Log figures you have with full cost tracking |
| Pre-orders | Track upcoming figures and mark them received |
| Character Hunts | Dedicated per-character tabs with wishlist and progress |
| Analytics | Spending charts and KPIs |
| Export / Import | Full JSON backup and restore |
| Image support | URL paste or file upload (auto-resized, stored locally) |

---

## Getting Started

Open `index.html` in any modern browser. No server, build step, or account needed. All data is saved in your browser's **localStorage** automatically.

---

## Tabs

### Owned

Your main collection. Each figure entry stores:

- **Title** (required)
- **Character**, **Brand**, **Type** (Scale, Prize, Nendoroid, Bunny, Model, Mini, …)
- **Scale** — enter as `1/7`, `1/8`, etc.
- **Release Date**
- **Landed Cost** — the total you paid (price + shipping)
- **Price** and **Shipping** as separate fields
- **Site** — where you bought it
- **Month Paid** — used for monthly spend charts

**Views:** Toggle between **Table** (sortable columns) and **Gallery** (card grid) with the buttons in the toolbar.

**Filters:** Narrow down by Type, Brand, or Site using the dropdowns. Search by title, character, or brand using the search box.

**Sorting:** Click any column header to sort ascending or descending.

---

### Pre-orders

Figures you've ordered but not yet received. Fields include:

- **Best Price** — the lowest price found
- **Est. Shipping** — estimated shipping cost
- **Landed Cost** — pre-calculated total
- **Paid in Advance** — any deposit already paid
- **Release Date**, **Site**, and the usual figure metadata

When your figure arrives, click **✓ Recv** to automatically move it to Owned, preserving all its data.

---

### Character Hunts

Hunts let you focus on collecting all figures of a specific character.

**Creating a hunt:**
1. Click the **+** tab at the right end of the tab bar.
2. Type the character's name (e.g. `Zero Two`, `Rem`, `Megumin`).
3. A new tab appears showing every figure matching that character name across your Owned figures, Pre-orders, and a dedicated **Wishlist**.

**Inside a hunt:**
- A progress bar shows **Received / Total** (owned vs. everything including wishlisted).
- Spend stats show how much you've spent and how much the remaining wishlist would cost.
- Add items directly to the wishlist with **+ Add to Hunt**.
- Promote wishlist entries: **→ Pre-order** or **→ Owned** when you're ready to buy or receive.

**Closing a hunt:** Click the **×** on the hunt tab. This removes the wishlist data for that hunt but leaves your Owned and Pre-order figures untouched.

> **Tip:** Hunts match figures by the **Character** field, so keep character names consistent (e.g. always `Zero Two`, not `02` or `Darling`).

---

### Analytics

A live dashboard built from your Owned collection:

| KPI | Description |
|---|---|
| Total Figures Owned | Count of all owned entries |
| Total Collection Spend | Sum of all Landed Costs |
| Avg Landed Cost | Mean spend per figure |
| Pre-order Pending | Sum of pre-order Landed Costs |

**Charts:**
- **Monthly Spend & Cumulative** — bar + line chart by Month Paid
- **By Figure Type** — doughnut showing spend breakdown
- **By Purchase Site** — horizontal bar ranked by spend
- **Top Brands by Spend** — horizontal bar, top 10
- **Price Distribution** — histogram of landed cost buckets

---

## Export & Import

All data lives in your browser. Export regularly to keep a backup.

### Export

Click **Export** in the Owned tab toolbar. A `.json` file is downloaded containing:
- All owned figures, pre-orders, and hunt wishlists
- All images (stored as base64 or URLs)

File name format: `figure-tracker-YYYY-MM-DD.json`

### Import

Click **Import** in the Owned tab toolbar and select a previously exported `.json` file. This **replaces** your current data with the file contents, so export first if you want to keep your current collection.

> Import works across devices and browsers — use it to migrate your collection or share it.

---

## Images

When adding or editing a figure you can attach an image two ways:

1. **Paste a URL** — paste any direct image link into the URL field.
2. **Upload a file** — click the upload button to pick a local image. It is automatically resized to a max of 300 px and stored as base64 in localStorage.

Click any thumbnail to open a fullscreen **lightbox** view. Click outside the image or press **Escape** to close it.

---

## Data Storage

- Stored in browser `localStorage` under keys `figureTracker_v2` and `figureImages_v2`.
- Nothing is sent to any server.
- Data persists across sessions as long as you don't clear your browser storage.
- Use **Export** to back up before clearing storage or switching browsers.
- The **Reset** button (red, in the Owned toolbar) wipes all data after confirmation.

---

## Tips

- Keep the **Character** field consistent so Hunts aggregate correctly.
- Use **Month Paid** on owned figures to populate the monthly spend chart in Analytics.
- The header always shows your total figure count and total spend; if you have an active hunt tab open it also shows the hunt's progress.
- On mobile, the layout adapts to a single-column view.
