# Spec-Driven Design — Redesign-Loop

Doku des gesamten Loops für Team & Leitung. Läuft in der **Claude-Code-Extension in VS Code**.

## Grundidee
Der bewährte **Loop bleibt** — wir tauschen nur das Material: Statt Code zu schreiben, ist das
**Material = Design + Spec**. **Code und Research sind Input & Leitplanke**, nicht das Ergebnis.
Jede Phase liefert ein Artefakt; jedes Artefakt ist Input der nächsten Phase. Bei einem Fehler
springt der Loop zur kleinsten passenden Phase zurück.

## Der Loop (ASCII)
```
                ┌─────────────────────────────────────────────────────────┐
                │                                                         │
   research/ ──▶│  ① BRAINSTORM ──▶ ② SPEC ──▶ ③ IMPLEMENT ──▶ ④ VERIFY  │
   (Evidenz)    │   Discovery       Brief      A) Figma bauen   Abgleich   │
   Code  ──────▶│                              B) Handoff       │         │
   (Ist-Stand)  │                                               ▼         │
                │                                          Pass? ─ja─▶ Dev-Handoff
                │                                               │         │
                └───────────────────  nein: zurück zur kleinsten Phase ◀──┘
```

## Begriffstabelle (Workshop-Begriff → Bedeutung hier)
| Workshop-Begriff | Bedeutung in diesem Setup |
|---|---|
| `brainstorm` | Phase 1 — Epic aus der Roadmap zur Epic-PRD härten, Fragen-Schleife bis ~90 % Confidence |
| `spec` | Phase 2 — Redesign-Brief mit Token-Mapping & Akzeptanzkriterien |
| `implement` | Phase 3 — A) Design in Figma bauen, B) Handoff ableiten |
| `verify` | Phase 4 — Abgleich Design/Handoff ↔ Spec, Loop-Entscheidung |
| `ux-advisor` | UX Advisor → a11y (Pflicht) + Heuristiken + Clarity |
| `ds-architecture-advisor` | Architecture Advisor → Design-System-Architektur & Migration |
| `architect-advisor` | Architect Advisor → Software-/Code-Architektur (Layering, Datenfluss) |
| `coding-advisor` | Coding Advisor → Code-Stil & Code-Organisation |
| `feasibility-advisor` | Feasibility Advisor → Aufwand, Wiederverwendung & dev-ready Handoff |

## Die vier Phasen
| Phase | Input | Tätigkeit | Advisors | Output |
|---|---|---|---|---|
| ① brainstorm | PROJECT-CONTEXT, `specs/roadmap.md`, Ist-Code, `research/`, Figma-Ist | Epic → Requirements/Akzeptanzkriterien, Fragen-Schleife bis ~90 % Confidence | alle drei | `PRD.md` |
| ② spec | PRD, PROJECT-CONTEXT, `tailwind.config.ts` | Ziel, Scope, Alt→Neu-Mapping, Intent, Akzeptanzkriterien | architect, coding, feasibility | `SPEC.md` |
| ③ implement | SPEC, PROJECT-CONTEXT | A) Figma mit den DS-Tokens des Projekts bauen · B) Handoff zurücklesen | ds-architecture (A), coding · feasibility (B) | Figma-Nodes + `HANDOFF.md` |
| ④ verify | SPEC, HANDOFF, PRD, PROJECT-CONTEXT | Screenshot-Diff, Token/a11y/Finding-Check | alle drei | `VERIFY.md` |

## Die Advisors (read-only — kritisieren & schlagen vor, ändern nie)
- **UX Advisor** (`ux-advisor`) — Fokus: a11y als Pflicht-Baseline, Heuristiken, Clarity;
  Interviews nur bedingt.
- **Architecture Advisor** (`ds-architecture-advisor`) — Fokus: Design-System-Architektur,
  aktive Library-Pflege, Integrität der Alt→Neu-Token-Migration (falls vorhanden).
- **Architect Advisor** (`architect-advisor`) — Fokus: Software-/Code-Architektur — Layering,
  Datenfluss, Server Action vs. Client, Integrationsgrenzen (`.claude/_architecture-reference.md`).
- **Coding Advisor** (`coding-advisor`) — Fokus: Code-Stil & Code-Organisation — Namen,
  Datei-/Ordnerstruktur, Imports, Typen, Konventionen (`.claude/_coding-guidelines.md`).
- **Feasibility Advisor** (`feasibility-advisor`) — Fokus: Umsetzbarkeit, Wiederverwendung,
  technische Constraints, dev-ready Handoff.

## Meetingstruktur (Annahme — anpassbar)
> **Annahme: „Phase = Ceremony"** — jede Phase ist ein eigenes Meeting/Arbeitsschritt.
> Hartes **Gate: „Spec abgenommen, bevor Implement startet."**
> Diese Struktur ist **bewusst als Annahme markiert** und mit der Leitung final zu justieren
> (siehe offenes To-do in WORKFLOW/PROJECT-CONTEXT).

## Research-Intake (gestuft)
a11y & Heuristiken sind **immer** verfügbar (kein File nötig). Clarity, Audits und Interviews
kommen **wenn vorhanden** nach `research/`. Fehlt eine Stufe → **offene Frage / Risiko**,
kein Blocker.

## Artefakt-Baum (pro Redesign)
```
specs/<epic>/
├── PRD.md          (Phase 1)
├── SPEC.md         (Phase 2)
├── HANDOFF.md      (Phase 3, Step B)
└── VERIFY.md       (Phase 4)
```

## Figma-MCP-Cheatsheet
- **Lesen:** `get_screenshot`, `get_metadata`, `get_design_context`, `get_variable_defs`,
  `search_design_system`.
- **Bauen:** **zuerst `/figma-use` laden** (für ganze Screens zusätzlich
  `/figma-generate-design`), dann `use_figma` / `generate_figma_design` — nur die DS-Tokens
  des Projekts, keine festen Hex-Werte, bestehende DS-Komponenten bevorzugen.
- **Code-Connect:** `/figma-code-connect` → `add_code_connect_map` (Figma-Komponente ↔
  `src/components/...`).

## Portabilität
Alles ist projekt-neutral **außer `.claude/PROJECT-CONTEXT.md`** — beim Projektwechsel **nur
diese eine Datei tauschen**. Alle Skills lesen sie zuerst.

## Quickstart
```
/brainstorm <epic>  → specs/<epic>/PRD.md
/spec               → specs/<epic>/SPEC.md
/implement          → Figma-Nodes + specs/<epic>/HANDOFF.md
/verify             → specs/<epic>/VERIFY.md  (Pass → Dev · Fail → zurück zur kleinsten Phase)
```
