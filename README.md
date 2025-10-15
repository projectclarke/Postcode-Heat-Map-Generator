# UK Customer Heat Map

A single-file, browser-only UK heat map that turns your customer list (CSV/XLSX) into a heat map. Postcode areas are embedded, filters are auto-generated from your columns, and updates are live as you tick/untick values.

> No servers, no builds — just open `Heatmap.html` in a modern browser.

---

## Features

- **Drop-in file loader**: CSV or XLSX (first sheet).
- **Postcode area lookup**: Embedded `Postcode area → lat/lon` table (replace with your own).
- **Live filters**: Multi/single-value aware (auto-detects comma/space/pipe separated fields).
- **Responsive rendering**: Chunked generation + “latest-wins” to keep the UI snappy.
- **Zero external build**: All logic in a single HTML file.

---

## Quick start

1. Open `Heatmap.html` in Chrome/Edge/Firefox.
2. Click **📂 Load Excel/CSV** and select your data file.
3. Pick the column that holds **postcodes** (outward + inward is fine; only the **letters** of the outward area are used for plotting).
4. Adjust filters on the left — the map updates live.

> Tip: The embedded CSV block titled **“Postcodes summary.csv”** must exist. Replace the sample rows with your authoritative list of `[Postcode area, Latitude, Longitude]`.

---

## Data requirements

- Your file must include a column with **UK postcodes** (e.g., `G1 2AB`, `AB10 1XG`, etc.).
- The app reduces each row to its **postcode area letters** (e.g., `G`, `AB`, `EH`) and looks up the centre point from the embedded table.

If a row’s postcode area is unknown (missing from the embedded table), that row is skipped.

---

## Customisation

Open `Heatmap.html` and look for the **CONFIG** block:

```js
const CONFIG = {
  INITIAL_VIEW: { lat: 54.5, lon: -3.0, zoom: 6 },
  HEAT: { radius: 20, blur: 25, maxZoom: 10 },
  SHOW_FIRST_VALUES: 250,
  MULTI_SEP_REGEX: /[,\s;|/]+/,
  MULTI_COL_MIN_SEP_RATIO: 0.05,
  MULTI_COL_MIN_MULTI_RATIO: 0.10,
  CHUNK_SIZE: 3000
};
