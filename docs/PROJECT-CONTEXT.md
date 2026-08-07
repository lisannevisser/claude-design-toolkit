# PROJECT-CONTEXT

> ⚠️ **TEMPLATE — pro Projekt ausfüllen.** Dies ist eine von drei projektspezifischen Dateien
> dieses Design-Kits (zusammen mit `_ux-reference.md` und `_content-guidelines.md`). Alles übrige
> (Skills, Advisors, WORKFLOW.md) ist projekt-neutral. **Alle Skills lesen diese Datei zuerst.**

## Projekt
- **Name:** `<projektname>`
- **Stack:** `<framework · sprache · styling · i18n · payment/backend · testing · paketmanager>`
- **Komponenten-Pfade:**
  - `<pfad>` — `<generische UI-Bausteine>`
  - `<pfad>` — `<Fachkomponenten>`
  - `<pfad>` — `<State/Contexts>`
- **Konventionen (Quelle z. B. `AGENTS.md`):** `<wichtigste Code-Konventionen kurz>`

## Quellen — am Anfang verlinken (Pflicht, keine Doppelablage)
Bevor der Loop startet, **diese Quellen verlinken statt Infos zu duplizieren**. Nur wenn eine
Quelle nicht existiert, wird die jeweilige Referenzdatei (`_ux-reference.md` /
`_content-guidelines.md`) inhaltlich gefüllt.
- **Produkt-Repo / Code-Quelle:** `<pfad-oder-url>` — echtes Produkt (Komponenten, **DS-Tokens**,
  echte Texte/Längen). Die Skills lesen hier den Ist-Code und ziehen Tokens für DS-treue
  HTML-Prototypen. (Kann ein **separates** Repo neben dem Design-Workspace sein — als zusätzliche
  Working-Dir registrieren.)
- **Design-System (Quelle der Wahrheit):** `<figma-url / DS-repo / md-link>`.
- **Content-Guidelines:** `<link/pfad>` (Tonalität, Terminologie, Schreibregeln).

## Projektdokumentation & Domänenwissen
Wenn Domänenwissen gebraucht wird, **zuerst den Domain-Index lesen** und von dort in die
jeweilige Domänendoku springen:
- **`<../docs/domain-index.md>`** — Navigationskarte, eine Zeile je Domäne.

Falls Domänendocs existieren, hier verlinken. Das Erzeugen solcher Code-Domänendocs (`init-docs`)
ist dev-facing und liegt außerhalb dieses Kits (späteres Code-Plugin); der Design-Loop liest das Produkt-Repo direkt
(via `research-design`/`research-advisor`).

## Designsystem — alt vs. neu
Quelle der Wahrheit für Tokens: **`<tailwind.config.* / tokens-datei>`**.

| Aspekt | ALT (auslaufend) | NEU (Ziel) |
|---|---|---|
| Token-Prefix Farben | `<alt-prefix-*>` | `<neu-prefix-*>` |
| Beispiel Primär | `<alt-token>` `<#hex>` | `<neu-token>` `<#hex>` |
| Beispiel Neutral | `<alt-token>` | `<neu-token>` |
| Typo | `<alt>` | `<neu>` |
| Quelle der Wahrheit | `<datei>` | `<datei>` |

> Migrationsrichtung: **`<alt-*>` → `<neu-*>`**. Im Endzustand bleiben **keine `<alt-*>`-Reste**.

## Figma
- Datei / Projekt: `<name oder URL>`
- Library / Design-System-Datei (Quelle der Wahrheit für `<neu-*>`-Tokens):
  `<figma-url>`
  - `fileKey`: `<key>` · Einstiegs-Node: `<node-id>`
- Relevante Node-IDs je Feature: `<bitte ausfüllen>`

## Research-Quellen (gestuft; Ablage: `research/`)
1. **a11y — immer Pflicht** (braucht keine Datei; WCAG AA, Fokus, Labels/aria, Touch-Targets).
2. **Heuristiken — jederzeit** (Nielsen + Form-Design; braucht keine Datei).
3. **Verhaltensdaten — wenn vorhanden** → `research/` (z. B. Heatmaps/Recordings, Analytics).
4. **Audits — wenn vorhanden** → `research/`.
5. **Interviews / Usability-Tests — nur bedingt** → `research/`; fehlen = Risiko, nicht Blocker.

## Technische Constraints (für Advisors)
- **`<payment/integration-constraint>`:** `<z. B. extern gehostete Felder begrenzt stylbar>`
- **i18n / lange Sprachen:** Locales `<…>` — manche laufen länger → Layouts müssen
  Textlängen tolerieren.
- **Feature-Flags / A/B (`<tool>`):** Varianten können parallel live sein — Redesign muss
  flag-tauglich sein.
- **Tests:** `<teststrategie + coverage-schwelle>`.

## Akzeptanz-Defaults (gelten für jede Spec/Verify)
- **Keine Alt-Token-Reste** (`<alt-*>`) — vollständig auf `<neu-*>` migriert.
- **a11y AA** + sichtbarer Fokus + Labels/aria + Touch-Targets ≥ 44px.
- **Bestehende Komponenten wiederverwenden** statt neu bauen.
