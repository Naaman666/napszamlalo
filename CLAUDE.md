# CLAUDE.md

This file provides guidance to Claude when working with this repository.

## Project Overview

Napszámláló — a simple, browser-based tool that calculates the number of days between two dates (both endpoints inclusive). Hungarian UI, theme selection (3 colors × 2 modes), settings persisted in localStorage. **Single `index.html` file, zero dependencies, no build step, no package manager.**

## Development Setup

No installation needed. Open the file directly:

```bash
xdg-open index.html    # Linux
open index.html        # macOS
start index.html       # Windows
```

## Common Commands

No build / test / lint pipeline. Manual verification in the browser.

## Code Style

- Single file, vanilla HTML5 + CSS + JS. Do not introduce new dependencies, build steps, or transpilers.
- Structure code into small, focused functions; only add comments where the logic is non-obvious.
- Do not add unnecessary error handling, logging, or abstractions.

## Architecture Notes

- **Theme system:** `data-theme` attribute on `<body>` + CSS custom property tokens (`--bg`, `--text`, `--accent`, ...). Every theme is one of 6 combinations (`{default,purple,green}-{dark,light}`). Persistence uses localStorage key: `napszamlalo-theme`.
- **Date calculation:** `Math.round((end - start) / msPerDay) + 1` — rounding compensates for DST transitions, `+1` ensures inclusive endpoints. ISO input (`YYYY-MM-DD`) → local-time Date.
- **External resource:** Google Fonts (JetBrains Mono, Inter). Without network access the fonts fall back to the `monospace` / `sans-serif` families.

## Git Workflow

- Always work on the `develop` branch.
- Never push/commit directly to `main`.
- Every commit should go to the `develop` branch.
- Only two branches are used: `develop` (active work) and `main` (stable releases).
- Do not create feature branches, topic branches, or any other branches.
