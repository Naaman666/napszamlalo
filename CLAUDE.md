# CLAUDE.md

This file provides guidance to Claude when working with this repository.

## Project Overview

Napszámláló — egyszerű, böngészőben futó eszköz, amely két dátum között eltelt napok számát számolja ki (mindkét végpont inkluzív). Magyar nyelvű felület, témaválasztás (3 szín × 2 mód), localStorage-ben tárolt beállítás. **Egyetlen `index.html` fájl, nulla függőség, nincs build, nincs csomagkezelő.**

## Development Setup

Nincs telepítés. A fájl közvetlenül megnyitható:

```bash
xdg-open index.html    # Linux
open index.html        # macOS
start index.html       # Windows
```

## Common Commands

Nincs build / teszt / lint pipeline. Manuális ellenőrzés a böngészőben.

## Code Style

- Egyetlen fájl, vanilla HTML5 + CSS + JS. Új függőséget, build lépést, transpilert ne vezess be.
- A kódot kicsi, fókuszált függvényekre tagold; csak akkor írj kommentet, ha a logika nem önmagyarázó.
- Ne adj hozzá felesleges error handlinget, loggingot vagy absztrakciót.

## Architecture Notes

- **Téma-rendszer:** `data-theme` attribútum a `<body>`-n + CSS custom property tokenek (`--bg`, `--text`, `--accent`, ...). Minden téma a 6 kombináció valamelyike (`{default,purple,green}-{dark,light}`). A perzisztálás `localStorage` kulcs: `napszamlalo-theme`.
- **Dátumszámítás:** `Math.round((end - start) / msPerDay) + 1` — a kerekítés DST-átmenetet kompenzál, a `+1` az inkluzív végpontokat biztosítja. ISO bemenet (`YYYY-MM-DD`) → local-time Date.
- **Külső erőforrás:** Google Fonts (JetBrains Mono, Inter). Hálózat nélkül a fontok visszaesnek a fallback `monospace` / `sans-serif` családra.

## Git Workflow

- Csak két ág van: `develop` (aktív munka) és `main` (kiadások).
- Minden commit a `develop`-ra megy. Soha ne pusholj közvetlenül `main`-re.
- Ne hozz létre feature / topic / claude/* ágat — ha véletlenül egy ilyenen találod magad, lépj át `develop`-ra mielőtt commitolsz, és töröld a kósza ágat (lokálisan és remote-on).
