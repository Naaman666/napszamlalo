# Napszámláló

Egyszerű, böngészőben futó webalkalmazás, amely két dátum között eltelt napok számát számolja ki (mindkét végpontot beleszámítva).

## Funkciók

- Napok számának kiszámítása két dátum között (inkluzív)
- Alapértelmezett kezdődátum: 2025. december 1.
- Alapértelmezett záródátum: mai nap (automatikusan frissül)
- Témarendszer: 3 színséma × 2 mód (sötét/világos) = 6 kombináció
- Téma mentése böngésző localStorage-ban
- Reszponzív kialakítás (mobilon is működik)
- Nincsenek külső függőségek – egyetlen HTML fájl

## Használat

Nyisd meg az `index.html` fájlt bármilyen modern böngészőben. Nincs szükség szerverre, telepítésre vagy build folyamatra.

```bash
# Klónozás
git clone https://github.com/naaman666/napszamlalo.git
cd napszamlalo

# Megnyitás böngészőben
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Vagy egyszerűen húzd be az `index.html` fájlt a böngészőbe.

## Témák

Az alkalmazás 6 témát támogat:

| Szín    | Sötét mód      | Világos mód      |
|---------|----------------|------------------|
| Default | `default-dark` | `default-light`  |
| Lila    | `purple-dark`  | `purple-light`   |
| Zöld    | `green-dark`   | `green-light`    |

A kiválasztott téma localStorage-ban tárolódik (`napszamlalo-theme` kulcson), így böngésző-újraindítás után is megmarad.

## Technológia

- **HTML5** – szemantikus struktúra
- **CSS3** – egyéni tulajdonságok (CSS Variables), Flexbox, Grid, backdrop-filter
- **Vanilla JavaScript** – keretrendszer nélkül
- **Google Fonts** – JetBrains Mono, Inter

## Projektstruktúra

```
napszamlalo/
└── index.html    # Teljes alkalmazás egyetlen fájlban
```

## Dátumszámítás logikája

```js
const msPerDay = 24 * 60 * 60 * 1000;
const days = Math.round((end - start) / msPerDay) + 1;
```

A `+1` biztosítja az inkluzív számolást (a kezdő- és záródátum is beleszámít).

## Licenc

[MIT](LICENSE)
