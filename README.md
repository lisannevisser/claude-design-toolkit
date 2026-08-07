# Spec-Driven Design Kit (Design)

Ein **wiederverwendbares Claude-Code-Setup** für **Spec-Driven *Design*** — ohne Bindung an ein
konkretes Repo. Der Scope ist bewusst **Design**: informierte UX (durch Research & Daten) und
**divergente visuelle Exploration** statt eines dev-fertigen Prototyps.

**Vorbau (einmal):** `specs/briefing.md` (User) → `/roadmap` → `specs/roadmap.md`
**Design-Loop (pro Roadmap-Item):**
`research-design → brainstorm-design → spec-design → explore-design → implement-design → verify-design`
→ optional `handoff-design` (saubere Dev-Übergabe, **außerhalb** des Loops)

Der TDD-**Code-Track** ist bewusst **nicht** Teil dieses Kits (keine konkurrierenden Loops). Er
liegt als Keim für eine spätere, **separate** Kit unter [`code-track-future/`](code-track-future/)
und greift später über `specs/briefing.md` + `specs/roadmap.md` + das `HANDOFF.md` an.

Voller Ablauf: [`claude-kit/WORKFLOW.md`](claude-kit/WORKFLOW.md).

## Aufbau

```
spec-driven-design-kit/
├── claude-kit/              → wird zum .claude/ des Design-Workspaces (drop-in)
│   ├── WORKFLOW.md
│   ├── _audit-standards.md  (neutraler Audit-Standard: 4 Lenses, Severity, Format)
│   ├── agents/             6 read-only Advisors (s. u.)
│   ├── skills/             Design-Loop (7) + roadmap
│   ├── settings.json
│   └── PROJECT-CONTEXT.md + _ux-reference.md + _content-guidelines.md
│                           ↑ die 3 PROJEKTSPEZIFISCHEN Dateien (Template-Stubs)
├── examples/payment-form-new/   gefüllte Referenz (briefing + die 3 Dateien)
└── code-track-future/      Staging für die spätere, separate Code-Kit (nicht drop-in)
```

## In einen Design-Workspace einsetzen

1. Inhalt von `claude-kit/` nach `<workspace>/.claude/` kopieren.
2. **Quellen verlinken statt duplizieren** (am Anfang, in `PROJECT-CONTEXT.md`):
   **Produkt-Repo / Code-Quelle** (echte Komponenten, DS-Tokens, Texte), **Design-System**,
   **Content-Guidelines**. Das Produkt-Repo darf ein **separates** Repo sein (als zusätzliche
   Working-Dir registrieren).
3. Nur falls eine Quelle fehlt, die **3 projektspezifischen Dateien** inhaltlich füllen (Beispiel
   unter `examples/payment-form-new/`):
   - `PROJECT-CONTEXT.md` — Stack, Pfade, Quellen-Links, Constraints *(alle Skills lesen sie zuerst)*
   - `_ux-reference.md` — Brand-Farben, Typo, Komponenten-Palette *(Quelle für `ux-advisor`)*
   - `_content-guidelines.md` — Voice/Tone, Terminologie *(Quelle für `content-advisor`)*
4. `specs/briefing.md` schreiben, dann `/roadmap`.
5. Optional: `research/`-Ordner (Heatmaps, Audits, Interviews) — gestufter Research-Intake.

Alles in `claude-kit/` außer diesen 3 Dateien ist **projekt-neutral**.

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
