# Architecture Reference — `<projektname>`

> ⚠️ **TEMPLATE — pro Projekt ausfüllen.** Primäres Guideline-Dokument des `architect-advisor`.
> Für Design-System-Tokens/Migration siehe `PROJECT-CONTEXT.md`.

Concise reference für Feature-Entwicklung. Wesentliche Design-Entscheidungen + Leitplanken.

## Stack
`<framework (router/output) · sprache · styling · i18n · validation · data-fetching · testing ·
paketmanager. Path-Aliase.>`

## Layering & where code goes
```
<pfad>     <was dort lebt>
<pfad>     <…>
```
Faustregel: **`<wer holt daten / wer mutiert / wo liegt interaktions-state>`**. Business-Logik
in `<pfad>` (unit-getestet) statt in Komponenten.

## Key design decisions
1. **`<entscheidung>`** — `<begründung + konsequenz>`
2. **`<write-path / actions>`** — `<…>`
3. **`<env-handling>`** — `<…>`
4. **`<i18n-struktur>`** — `<locales, negotiation>`
5. **`<middleware / per-request concerns>`** — `<…>`
6. **`<feature-flags / A-B>`** — `<flag-toleranz>`
7. **`<payment/externe integration>`** — `<styling/dom-grenzen>`
8. **`<validation>`** — `<…>`
9. **`<observability / error-handling>`** — `<…>`

## Conventions (enforced)
- `<die wichtigsten erzwungenen Konventionen kurz>`
- **Reuse existing components before building new.**
- Tokens migrieren `<alt-*>` → `<neu-*>`; kein hardcoded hex.
- Layouts tolerieren lange Übersetzungen; Touch-Targets ≥ 44px; a11y AA.

## When making an architecture decision, check
Passt es ins Layering? · Gehört State in Context/Util statt Komponente? · Env-Var deklariert? ·
Flag-tolerant & i18n-vollständig? · Wiederverwendung bestehender Komponenten? · Write-Path über
die definierte Mutations-Grenze? · Untrusted Input validiert?
