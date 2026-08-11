# Spec-Driven Design — Design-Kit (Figma + HTML)

Doku des **Design-Kits**. Fokus: **informierte UX (durch Research & Daten)** und **divergente
visuelle Exploration**, nicht ein dev-fertiger Prototyp. Der Scope ist **bewusst Design** — der
TDD-Code-Track ist bewusst ausgelagert (archiviert im Git-Tag `code-track-archive`, künftig ein eigenes Plugin) und konkurriert hier
nicht. Das Dev-Handoff ist ein **optionaler Schluss-Schritt** und die saubere Brücke dorthin.

## Vorbau: Briefing → Roadmap (einmal pro Projekt)
- **`specs/briefing.md`** — vom User geschriebene Projektbeschreibung (Produkt, Redesign-Ziel,
  messbare Erfolgsziele, Scope, Constraints).
- **`/roadmap`** zerlegt das Briefing in **priorisierte Redesign-Bereiche** (`specs/roadmap.md`) —
  nur Probleme/Requirements, keine Lösungen/Tech; Abhängigkeiten + Parallelität; Abnahme-Gate.

Die Roadmap ist das **geteilte Rückgrat**: jedes Item durchläuft erst den Design-Loop und (optional,
später, in einem separaten Code-Plugin) den Code-Loop.

## Der Design-Loop (6 Phasen + optionaler Handoff)
Research- und explorationsgetrieben: Daten zuerst, dann divergieren, dann eine informierte Wahl
konvergieren. **Discovery ist zweistufig (B2):** Research kartiert Wissen **und Lücken**, Brainstorm
härtet bis ~90 %.

| Phase | Skill | Output | Kern |
|---|---|---|---|
| ⓪ Research | `research-design` | `RESEARCH.md` (+ `AUDIT.md`/`AUDIT.html`) | Daten + **Heuristik-Audit** synth.; Baseline/Ziel; **Lücken**; erste Hypothesen. Survey mit „weiß nicht", **kein** Gate |
| ① Brainstorm | `brainstorm-design` | `BRAINSTORM.md` | Hypothesen priorisieren/schärfen; **Survey bis ~90 %** (das eine Gate) |
| ② Spec | `spec-design` | `SPEC.md` | **Problem + Constraints** (nicht die Lösung) |
| ③ Explore | `explore-design` | `EXPLORE.md` (+ `explore/`) | **schnelle HTML-Richtungen** auf Vergleichs-Canvas, vergleichen, wählen |
| ④ Implement | `implement-design` | Figma-Nodes (+ opt. HTML) | gewählte Richtung **final in Figma** |
| ⑤ Verify | `verify-design` | `VERIFY.md` | Abgleich + **UX-Ziel**, optionale Validierung |
| ＋ Handoff | `handoff-design` | `HANDOFF.md` | *(optional, nach Pass)* dev-ready ableiten + Relay |

## Der Loop (ASCII)
```
  briefing.md ─▶ /roadmap ─▶ roadmap.md
                                 │  (pro Item)
   research/  ┌─────────────────▼────────────────────────────────────────────────────┐
   (Daten) ──▶│ ⓪ RESEARCH ─▶ ① BRAINSTORM ─▶ ② SPEC ─▶ ③ EXPLORE ─▶ ④ IMPLEMENT ─▶ ⑤ VERIFY │
   Ist-Prod. ▶│  Daten+Audit   ~90%-Gate      Problem    HTML-Richt.   Figma final     UX-Ziel │
              │  +Lücken+Ziel                  +Constr.   +wählen                              │
              │                                                                          │     │
              └─────────────────────  nein: zurück zur kleinsten Phase ◀── Pass? ────────┘     │
                                                                              │ ja              │
                                                                              ▼                 │
                                          ＋ HANDOFF (optional) ─▶ HANDOFF.md ─▶ Dev-Prozess / späteres Code-Plugin
```

## Brücke zum Code (optional, separate Kit)
Der Design-Loop ist **vollständig standalone**. Soll ein abgenommenes Design in Code:
- `spec-design` setzt **`Code-Epic: <ID>`** (= Roadmap-Item-ID); `handoff-design` trägt sie ins
  `HANDOFF.md`.
- Ein **späteres Code-Plugin** liest `HANDOFF.md` als bindenden Input
  (Token-Mapping & Komponenten-Intent übernehmen, nicht neu erfinden) und notiert `Design-Feature:`
  zurück.
- Bis dahin dient `HANDOFF.md` jedem beliebigen Dev-Prozess als dev-ready Vorlage.

## Die Advisors (read-only — kritisieren & schlagen vor, ändern nie)
Frühe Phasen (⓪–③) sind UX-/Research-lastig:
- **`ux-advisor`** — UX-Entscheidungs-Richter: a11y (Pflicht-Baseline), Heuristiken, Clarity.
- **`research-advisor`** — Discovery-Auditor: Heuristik-/Experten-Audit des Ist-Produkts nach
  `audit-standards.md` (Lenses inkl. Projekt-Lenses, Severity, AUDIT.md + interaktiver Pin-Report
  AUDIT.html; kanonisch im `research-design`-Skill-Ordner, Projekt-Kopie via Setup), optional
  Live-Walkthrough per Browser (Phase ⓪).
- **`content-advisor`** — Copy/Microcopy/Tonalität gegen Content-Guidelines, i18n-Längen.
- **`conversion-advisor`** — CRO-/Trust-Linse, an den messbaren Research-Zielen verankert.
- **`ds-architecture-advisor`** — Design-System-Architektur, Library-Pflege, Token-Migration.
- **`feasibility-advisor`** — Umsetzbarkeit & Wiederverwendung; voller dev-ready-Check im Handoff.

> Tiefer Code-Stil/Software-Architektur liegt außerhalb dieses Kits (späteres Code-Plugin).

## Artefakt-Baum (pro Redesign-Item)
```
specs/briefing.md · specs/roadmap.md            (Projekt-Vorbau)
docs/redesign/<item>/
├── RESEARCH.md    (Phase 0)
├── AUDIT.md + AUDIT.html  (Phase 0, Heuristik-Audit + interaktiver Pin-Report)
├── BRAINSTORM.md  (Phase 1)
├── SPEC.md        (Phase 2)
├── EXPLORE.md  + explore/ (HTML-Prototypen + Canvas)   (Phase 3)
├── VERIFY.md      (Phase 5)
└── HANDOFF.md     (optionaler Schluss-Schritt)
```

## Werkzeuge
- **HTML-Prototypen (Phase 3):** schnelle Vanilla-HTML/CSS/JS-Richtungen, DS-treu (Tokens aus dem
  Produkt-Repo) oder Wireframe-Fallback; Vergleichs-Canvas mit Tabs + Live-Reglern. *(Ansatz
  inspiriert von dan-carino/design-directions-skill.)*
- **Figma (Phase 4):** zuerst `/figma-use` laden (ganze Screens: `/figma-generate-design`), dann
  `use_figma` — nur neue Tokens (`<neu-*>`), keine festen Hex-Werte, DS-Komponenten bevorzugen.
  Lesen: `get_screenshot`, `get_metadata`, `get_design_context`, `get_variable_defs`,
  `search_design_system`.
- **Code-Connect (Handoff):** `/figma-code-connect` → `add_code_connect_map`.

## Portabilität
Projekt-neutral **außer drei Dateien** (`PROJECT-CONTEXT.md`, `_ux-reference.md`,
`_content-guidelines.md`). Alle Skills lesen `PROJECT-CONTEXT.md` zuerst. **Am Anfang Quellen
verlinken** (Produkt-Repo, DS, Content-Guidelines) statt zu duplizieren — siehe PROJECT-CONTEXT.

## Quickstart
```
/roadmap                      → specs/roadmap.md            (aus specs/briefing.md; Abnahme-Gate)
/research-design <item>       → docs/redesign/<item>/RESEARCH.md   (Daten, Audit, Ziel, Lücken)
/brainstorm-design <item>     → docs/redesign/<item>/BRAINSTORM.md (Hypothesen bis ~90%)
/spec-design                  → docs/redesign/<item>/SPEC.md       (Problem + Constraints)
/explore-design               → docs/redesign/<item>/EXPLORE.md    (HTML-Richtungen + Wahl)
/implement-design             → Figma-Nodes (gewählte Richtung final)
/verify-design                → docs/redesign/<item>/VERIFY.md     (Pass → Handoff · Fail → zurück)
/handoff-design               → docs/redesign/<item>/HANDOFF.md    (optional, nach Pass)
```
