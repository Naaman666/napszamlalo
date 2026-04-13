# CLAUDE.md

This file provides guidance to Claude Code when working on this repository.

## Project Overview

**Napszámláló** ("Day Counter" in Hungarian) is a single-file web application (`index.html`) that calculates the number of days between two dates (inclusive). It has no build step, no package manager, and no external runtime dependencies.

## Architecture

The entire application lives in `index.html` with three embedded sections:

- **CSS** – theme tokens (CSS custom properties), layout, responsive styles
- **HTML** – two date inputs, a calculate button, and a display area
- **JavaScript** – theme persistence (localStorage), date parsing, day calculation

## Development Guidelines

### Running the app

Open `index.html` directly in a browser. No server, no build, no install step needed.

### Making changes

Since the project is a single HTML file, all edits go into `index.html`. The file is organized with clear section comments:

```
/* ---------- THEME TOKENS ---------- */
/* ---------- THEME BAR ---------- */
/* ---------- CONTENT ---------- */

/* ---------- THEME ---------- */   (JS)
/* ---------- DAY COUNTER ---------- */ (JS)
```

### Theme system

Themes are defined as CSS custom properties on `[data-theme="<name>"]` attribute selectors. The six theme names follow the pattern `{color}-{mode}`:

- `default-dark`, `default-light`
- `purple-dark`, `purple-light`
- `green-dark`, `green-light`

To add a new color scheme, duplicate an existing pair of `[data-theme]` blocks and update the CSS variable values. Then add the corresponding swatch button in the HTML theme bar.

### Date calculation

The core calculation is intentionally simple:

```js
const msPerDay = 24 * 60 * 60 * 1000;
const days = Math.round((end - start) / msPerDay) + 1; // inclusive
```

Do not change `Math.round` to `Math.floor` – rounding handles DST edge cases.

### Localization

- UI labels and messages are in **Hungarian**
- Date format displayed to users: `YYYY. MM. DD.` (Hungarian standard)
- The `formatHU(iso)` function converts ISO date strings to this format

### localStorage key

Theme state is stored under the key `napszamlalo-theme` as JSON:

```json
{ "color": "default", "mode": "dark" }
```

## Common Tasks

| Task | Notes |
|---|---|
| Change default start date | Edit the `value` attribute of `#start` input and the `todayISO()` call in `calculate()` |
| Add a new theme color | Add two `[data-theme]` CSS blocks + swatch button in HTML |
| Change fonts | Update the Google Fonts `<link>` URL and the `font-family` CSS variables |
| Add a new language | All user-facing strings are in the HTML; search for Hungarian text to find them |

## General Behavior Rules

- **Ha menüpontot keresel (bármely UI-ban, pl. GitHub, szoftverek):** mindig keress rá a weben (`WebSearch`), hogy az adott menüpont valójában hol helyezkedik el. Ne tippelj, ne a régi memóriádra hagyatkozz – a felületek változnak.

## Testing

There is no automated test suite. Manual testing checklist:

- [ ] Default dates load correctly on page open
- [ ] Day count updates when either date changes
- [ ] Error shows when end date is before start date
- [ ] Error shows for invalid date input
- [ ] Theme switches apply immediately and persist after page reload
- [ ] Layout looks correct on a 320px-wide viewport (mobile)
