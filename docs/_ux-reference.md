# UX Reference — `<projektname>`

> ⚠️ **TEMPLATE — pro Projekt ausfüllen.** Primäres Guideline-Dokument des `ux-advisor`.

`<Ein-Satz-Beschreibung des Produkts/der Flows. Stack-Kurzform. Falls zwei Designsysteme
parallel existieren: welches ist neu (Ziel), welches wird migriert.>`

## Themes
`<Falls Theming: wie wird das Theme gesetzt (z. B. data-theme), was tauscht es (CSS-Variablen,
Fonts)? Tabelle Legacy vs. Neu mit Font + Schlüsselfarben.>`

## Brand Colors
### `<neu>` (current system) — use these for new work
- **Primary:** `<token #hex + Abstufungen>`
- **Neutral:** `<token #hex …>`
- **Success / Error / Warning:** `<token #hex …>`

### `<alt>` (legacy)
- `<die wichtigsten Legacy-Token + Hex, die noch im Code vorkommen>`

## Typography
`<Font-Size-Scale (Token → rem, Zeilenhöhe). Heading-Helper-Klassen.>`

## Elevation & Shape
- **Shadows:** `<token-namen + Verwendung>`
- **Radius:** `<inputs / cards / chips / buttons>`

## Component Palette
Primitives in `<pfad>`, composed elements in `<pfad>`.

- **`<Button>`** (`<datei>`) — `<Kurzbeschreibung: Variante, Farben, States>`
- **`<Input>`** (`<datei>`) — `<…>`
- **`<Notice/Alert>`** (`<datei>`) — `<Varianten>`
- **`<Stepper>`** / **`<Card>`** / **`<Chip>`** / **`<Dialog>`** — `<…>`
- `<weitere relevante Primitives>`

## Conventions
- `<Styling-Regeln: nur Utility-Klassen? Farben nur via Token, kein raw hex? etc.>`
- `<Theme-bedingtes Styling, falls vorhanden>`
- Für neue/redesignte UI: bevorzugt `<neu-*>`-Tokens, `<neu>`-Font-Scale, `<neue Button-Komponente>`.
