# Spec-Driven Design Kit (Design)

Ein **wiederverwendbares Claude-Code-Setup** für **Spec-Driven *Design*** — ohne Bindung an ein
konkretes Repo. Der Scope ist bewusst **Design**: informierte UX (durch Research & Daten) und
**divergente visuelle Exploration** statt eines dev-fertigen Prototyps.

**Vorbau (einmal):** `specs/briefing.md` (User) → `/roadmap` → `specs/roadmap.md`
**Design-Loop (pro Roadmap-Item):**
`research-design → brainstorm-design → spec-design → explore-design → implement-design → verify-design`
→ optional `handoff-design` (saubere Dev-Übergabe, **außerhalb** des Loops)

Der TDD-**Code-Track** ist bewusst **nicht** Teil dieses Kits (keine konkurrierenden Loops). Er
liegt als Keim für eine spätere, **separate** Kit unter [`code-track/`](code-track/)
und greift später über `specs/briefing.md` + `specs/roadmap.md` + das `HANDOFF.md` an.

Voller Ablauf: [`docs/WORKFLOW.md`](docs/WORKFLOW.md).

## Aufbau

```
claude-design-toolkit/
├── .claude-plugin/          plugin.json + marketplace.json (Claude-Code-Plugin)
├── skills/                  Design-Loop (7) + roadmap
├── agents/                  6 read-only Advisors (s. u.)
├── docs/                    WORKFLOW.md, _audit-standards.md, settings.json
│                            + Template-Stubs: PROJECT-CONTEXT.md, _ux-reference.md,
│                              _content-guidelines.md (die 3 PROJEKTSPEZIFISCHEN Dateien)
└── code-track/              Staging für die spätere, separate Code-Kit (wird nicht
                             als Plugin geladen — Skills/Agents dort sind inaktiv)
```

## Installation als Plugin

Einmalig auf dem Rechner (lädt Skills + Agents in **jedes** Projekt, nichts muss in
Projekt-Repos committet werden):

```bash
claude plugin marketplace add lisannevisser/claude-design-toolkit
```

```bash
claude plugin install design-toolkit@lisanne-toolkit
```

Solange das Repo privat ist, braucht die Maschine Git-Zugriff auf
`github.com/lisannevisser/claude-design-toolkit` (SSH-Key oder `gh auth login`).
Updates: neue Skills/Agents hier pushen, dann `claude plugin update design-toolkit`.

## In einen Design-Workspace einsetzen

1. Plugin installieren (s. o.) — Skills und Advisors sind damit überall verfügbar.
2. **Quellen verlinken statt duplizieren** (am Anfang, in `<workspace>/.claude/PROJECT-CONTEXT.md`):
   **Produkt-Repo / Code-Quelle** (echte Komponenten, DS-Tokens, Texte), **Design-System**,
   **Content-Guidelines**. Das Produkt-Repo darf ein **separates** Repo sein (als zusätzliche
   Working-Dir registrieren).
3. Nur falls eine Quelle fehlt, die **3 projektspezifischen Dateien** inhaltlich füllen
   (Template-Stubs unter `docs/`, gefülltes TS-Beispiel im Repo `trustedshops/product-design-lab`
   unter `docs/kit-examples/payment-form-new/`):
   - `PROJECT-CONTEXT.md` — Stack, Pfade, Quellen-Links, Constraints *(alle Skills lesen sie zuerst)*
   - `_ux-reference.md` — Brand-Farben, Typo, Komponenten-Palette *(Quelle für `ux-advisor`)*
   - `_content-guidelines.md` — Voice/Tone, Terminologie *(Quelle für `content-advisor`)*
4. `specs/briefing.md` schreiben, dann `/roadmap`.
5. Optional: `research/`-Ordner (Heatmaps, Audits, Interviews) — gestufter Research-Intake.

Diese 3 Dateien gehören ins jeweilige Projekt-Repo, nicht hierher — dieses Kit bleibt
**projekt- und firmenneutral**. (Offener Punkt: einige Skills/Advisors referenzieren noch
`payment-form-new` und `trstd-*`-Tokens aus der Entstehungszeit — Entfirmung steht aus.)

## Die 6 Advisors (read-only — kritisieren & schlagen vor, ändern nie)

| Advisor | Fokus |
|---|---|
| `ux-advisor` | UX-Entscheidungen, a11y (Pflicht-Baseline), Heuristiken, Clarity |
| `research-advisor` | Heuristik-/Experten-Audit des Ist-Produkts nach `_audit-standards.md` (4 Lenses), opt. Live-Walkthrough |
| `content-advisor` | Copy/Microcopy/Tonalität gegen Content-Guidelines, i18n-Längen |
| `conversion-advisor` | CRO-/Trust-Linse, an messbaren Research-Zielen verankert |
| `ds-architecture-advisor` | Design-System-Architektur, Library-Pflege, Token-Migration |
| `feasibility-advisor` | Aufwand, Wiederverwendung, dev-ready Handoff |

## Credits
Der HTML-Prototyp-Canvas-Ansatz in `explore-design` (mehrere Varianten auf Tabs + Live-Regler) ist
inspiriert von **[dan-carino/design-directions-skill](https://github.com/dan-carino/design-directions-skill)** —
hier DS-treu und evidenzbasiert adaptiert.
