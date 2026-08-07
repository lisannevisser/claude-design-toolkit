# Spec-Driven Design Kit (Design)

Ein **wiederverwendbares Claude-Code-Setup** für **Spec-Driven *Design*** — ohne Bindung an ein
konkretes Repo. Der Scope ist bewusst **Design**: informierte UX (durch Research & Daten) und
**divergente visuelle Exploration** statt eines dev-fertigen Prototyps.

**Vorbau (einmal):** `/setup-design-workspace` (Quellen-Onboarding) → `specs/briefing.md` (User) → `/roadmap` → `specs/roadmap.md`
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
2. **`/setup-design-workspace` ausführen** — das strukturierte Onboarding-Interview fragt alle
   Quellen aktiv ab (Produkt-Repo, Design-System, Content-Guidelines, Analytics-/Tracking-Tool,
   A/B-Testing-Tool, Competitor-Analysen, Research-Bestand, gewünschte Anbindungen/Zugänge),
   füllt daraus die 3 projektspezifischen Dateien und legt `research/` mit Quellen-Inventar an:
   - `PROJECT-CONTEXT.md` — Stack, Pfade, Quellen-Links, Tools, Constraints *(alle Skills lesen sie zuerst)*
   - `_ux-reference.md` — Brand-Farben, Typo, Komponenten-Palette *(Quelle für `ux-advisor`)*
   - `_content-guidelines.md` — Voice/Tone, Terminologie *(Quelle für `content-advisor`)*
   **Prinzip: Quellen verlinken statt duplizieren.** Fehlende Quellen werden als protokollierte
   Lücken festgehalten (kein Blocker). Auch die Advisors verweisen auf dieses Setup, sobald ihnen
   Kontext fehlt — niemand muss von selbst daran denken.
3. `specs/briefing.md` schreiben, dann `/roadmap`.
4. `research/` wächst mit — gestufter Research-Intake (Heatmaps, Audits, Interviews).

Diese 3 Dateien gehören ins jeweilige Projekt-Repo, nicht hierher — dieses Kit bleibt
**projekt- und firmenneutral**. Firmen- oder projektspezifisches Wissen (Tokens, Prozesse,
Beispiele) lebt im jeweiligen Projekt-Workspace.

## Inventar

### Design-Loop-Skills (`skills/` — aktiv im Plugin)

| Skill | Phase | Was er tut |
|---|---|---|
| `/setup-design-workspace` | Onboarding | Quellen-Interview bei Projektstart: Produkt/Code, DS, Content, Analytics/Tracking, A/B-Tool, Competitor-Analysen, Anbindungen → füllt die Kontextdateien + `research/`-Inventar |
| `/roadmap` | Vorbau | Zerlegt `specs/briefing.md` in eine priorisierte Redesign-Roadmap (nur Probleme/Requirements, keine Lösungen) |
| `/research-design` | 0 | Evidenzbasierte Discovery: Daten synthetisieren, Ist-Produkt heuristisch auditieren, messbares Research-Ziel formulieren |
| `/brainstorm-design` | 1 | Research-Hypothesen priorisieren, schärfen und per Frage-Loop bis ~90 % Confidence härten |
| `/spec-design` | 2 | Redesign-Brief (Design-Spec): Problem, Scope, Constraints, Komponenten-Intent, UX-Outcome-Akzeptanzkriterien |
| `/explore-design` | 3 | Divergente Exploration: 2–3 HTML-Prototyp-Richtungen auf einem Vergleichs-Canvas mit Live-Reglern, dann Wahl |
| `/implement-design` | 4 | Baut die gewählte Richtung in Figma zur finalen Fidelity aus (DS-Tokens des Projekts) |
| `/verify-design` | 5 | Gleicht das Figma-Ergebnis gegen Design-Spec und Research-Ziel ab (Screenshot-Diff, a11y, Token-Compliance) |
| `/handoff-design` | optional | Dev-Handoff-Paket: Element→Token→Komponente-Mapping aus dem verifizierten Design |

### Advisor-Agents (`agents/` — read-only: kritisieren & schlagen vor, ändern nie)

| Advisor | Fokus |
|---|---|
| `ux-advisor` | UX-Entscheidungen, a11y (Pflicht-Baseline), Heuristiken, Verhaltensdaten |
| `research-advisor` | Heuristik-/Experten-Audit des Ist-Produkts nach `_audit-standards.md` (4 Lenses), opt. Live-Walkthrough |
| `content-advisor` | Copy/Microcopy/Tonalität gegen Content-Guidelines, i18n-Längen |
| `conversion-advisor` | CRO-/Trust-Linse, an messbaren Research-Zielen verankert |
| `ds-architecture-advisor` | Design-System-Architektur, Library-Pflege, Token-Migration |
| `feasibility-advisor` | Aufwand, Wiederverwendung, dev-ready Handoff |

### Templates & Referenzdocs (`docs/`)

`WORKFLOW.md` (voller Ablauf) · `_audit-standards.md` (neutraler Audit-Standard) ·
Template-Stubs `PROJECT-CONTEXT.md`, `_ux-reference.md`, `_content-guidelines.md` ·
`settings.json`

### Code-Track (`code-track/` — Staging, im Plugin NICHT aktiv)

Skills `brainstorm`, `write-spec`, `implement-epic`, `verify-epic`, `init-docs` +
Agents `architect-advisor`, `coding-advisor` + Templates `_architecture-reference.md`,
`_coding-guidelines.md`. Keim für eine spätere, separate Code-Kit (TDD-Track).

## Backlog / Ziele

- [x] Entfirmung: alle firmenspezifischen Referenzen aus Skills/Advisors entfernt (07.2026 / 08.2026)
- [x] Onboarding-Verhalten: Skills/Advisors fragen aktiv nach, wenn Projekt-Kontextdateien fehlen
- [x] `/setup-design-workspace`: strukturiertes Quellen-Interview bei Projektstart (Tracking, A/B, Competitor-Analysen, Anbindungen)
- [ ] **Übersetzung auf Englisch** (alle Skills, Advisors, Docs) — Voraussetzung fürs Public-Schalten
- [ ] Repo **public** schalten (nach EN-Übersetzung + finalem Review)
- [ ] Code-Track zu einem eigenständigen Kit ausbauen (separates Plugin), wenn gebraucht
- [ ] Eval: Kit einmal in einem fremden Projekt (nicht-TS) durchspielen und Reibungspunkte fixen

## Credits
Der HTML-Prototyp-Canvas-Ansatz in `explore-design` (mehrere Varianten auf Tabs + Live-Regler) ist
inspiriert von **[dan-carino/design-directions-skill](https://github.com/dan-carino/design-directions-skill)** —
hier DS-treu und evidenzbasiert adaptiert.
