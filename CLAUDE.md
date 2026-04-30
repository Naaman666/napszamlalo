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

- **External resource:** Google Fonts (JetBrains Mono, Inter). Without network access the fonts fall back to `monospace` / `sans-serif`.

## Git Workflow

Only two persistent branches exist: `develop` (active work) and `main` (stable releases).

- **Humans:** always commit directly to `develop`. Never commit or push to `main`.
- **AI agents (Claude, Codex, etc.):** open pull requests from a short-lived `claude/*` or `codex/* ` branch. The PR must always target `develop`, never `main`. Delete branch after merge.

Do not create feature or topic branches.
