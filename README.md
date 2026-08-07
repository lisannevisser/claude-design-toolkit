# Claude Design Toolkit

Ein **Claude-Code-Plugin für Designer:innen, die Builder werden**. Es macht aus Claude ein
Design-Team mit Arbeitsweise: ein wiederverwendbares Setup aus Skills und Advisor-Agents,
ohne Bindung an ein konkretes Repo, eine Firma oder ein Produkt.

**Das Ziel ist ein Looping-Setup:** Die AI iteriert nicht „bis es gefällt", sondern gegen einen
prüfbaren Anker. Vier Zutaten machen das möglich, und sie sind der Kern dieses Kits:

1. **Ein schriftlicher Anker**: messbares Research-Ziel + UX-Outcome-Kriterien im Design Brief.
2. **Ein Verify-Schritt**, der jedes Ergebnis gegen diesen Anker hält (`/verify-design`).
3. **Eine Rücksprungregel**: bei Fail zurück in die kleinste passende Phase, nicht auf Anfang.
4. **Read-only-Kritiker**: sechs Linsen-Advisors, die den Loop mit Evidenz statt Geschmack
   füttern (plus Perspektiven-Add-ons als bewusste Störimpulse, s. u.).

So kann der Loop konvergieren, statt endlos zu drehen, und Menschen mit unterschiedlichem
Erfahrungslevel kommen zum gleichen, belegbaren Arbeitsstand.

## Design Thinking als Rückgrat

Der Loop ist Design Thinking mit einem schriftlichen Define-Artefakt:

| Design-Thinking-Phase | Skill | Artefakt |
|---|---|---|
| (Onboarding) | `/setup-design-workspace` | gefüllte Kontextdateien + `research/`-Inventar |
| (Rahmen) | `/roadmap` | priorisierte Roadmap, nur Probleme, keine Lösungen |
| **Empathize** | `/research-design` | `RESEARCH.md` + `AUDIT.md`: Insights, Lücken, Baseline, messbares Ziel |
| **Define** | `/brainstorm-design` + `/spec-design` | gehärtete Hypothesen + **Design Brief** (Problem, Scope, Erfolgskriterien) |
| **Ideate + Prototype** (divergent) | `/explore-design` | 2–3 HTML-Prototyp-Richtungen auf einem Vergleichs-Canvas |
| **Prototype** (hi-fi) | `/implement-design` | finales Design in Figma, DS-treu |
| **Test** | `/verify-design` | Abgleich gegen Brief + Research-Ziel; Pass schließt den Loop, Fail springt zurück |
| (Übergabe, optional) | `/handoff-design` | eindeutiges Dev-Handoff-Paket |

Die Advisors decken die drei klassischen Design-Thinking-Linsen ab:

| Linse | Advisors |
|---|---|
| **Desirability** (wollen es Menschen?) | `ux-advisor`, `research-advisor`, `content-advisor` |
| **Feasibility** (können wir es bauen?) | `feasibility-advisor`, `ds-architecture-advisor` |
| **Viability** (trägt es das Ziel?) | `conversion-advisor` |

Wichtige Grundregel der Feasibility-Linse: **Aufwand ist Information, kein Veto.** Fehlt einem
Design ein technisches Feature, ist das ein Design-Auftrag, kein K.-o.-Kriterium.

## Add-ons: Perspektiven-Advisors

Bewusst **außerhalb** der drei Linsen und des Evidenz-Systems: Perspektiven-Advisors sind
meinungsstarke Sparringspartner mit einer sehr spezifischen Sicht auf Produkte. Ihre Urteile
sind **Taste als Provokation**, keine Beweise; sie erzeugen Hypothesen und Härtetests, die der
Loop dann mit Evidenz prüft. Nutzen auf Zuruf, als harter Kritiker vor einem Gate oder als
Brainstorming-Partner.

| Advisor | Perspektive |
|---|---|
| `jobs-advisor` | Denkweise von Steve Jobs: kompromisslose Einfachheit, Fokus durch Weglassen, Erlebnis vor Technologie, Weltklasse-Anspruch an Details. Kritisiert in vier Schritten (das Eine, die Streichliste, das Detail, das Verdikt) und brainstormt subtraktiv (10x statt 10 %) |

## Aufbau

```
claude-design-toolkit/
├── .claude-plugin/          plugin.json + marketplace.json (Claude-Code-Plugin)
├── skills/                  Onboarding + Design-Loop (9 Skills)
├── agents/                  6 Linsen-Advisors + Perspektiven-Add-ons (read-only)
└── docs/                    WORKFLOW.md, _audit-standards.md, settings.json
                             + Template-Stubs: PROJECT-CONTEXT.md, _ux-reference.md,
                               _content-guidelines.md (die 3 PROJEKTSPEZIFISCHEN Dateien)
```

## Installation als Plugin

Einmalig auf dem Rechner (lädt Skills + Advisors in **jedes** Projekt, nichts muss in
Projekt-Repos committet werden):

```bash
claude plugin marketplace add lisannevisser/claude-design-toolkit
```

```bash
claude plugin install design-toolkit@lisanne-toolkit
```

Solange das Repo privat ist, braucht die Maschine Git-Zugriff auf
`github.com/lisannevisser/claude-design-toolkit` (SSH-Key oder `gh auth login`).
Updates: neue Skills/Advisors hier pushen, dann `claude plugin update design-toolkit`.

## In einen Design-Workspace einsetzen

1. Plugin installieren (s. o.), Skills und Advisors sind damit überall verfügbar.
2. **`/setup-design-workspace` ausführen**: das strukturierte Onboarding-Interview fragt alle
   Quellen aktiv ab (Produkt-Repo, Design-System, Content-Guidelines, Analytics-/Tracking-Tool,
   A/B-Testing-Tool, Competitor-Analysen, Research-Bestand, gewünschte Anbindungen/Zugänge),
   füllt daraus die 3 projektspezifischen Dateien und legt `research/` mit Quellen-Inventar an:
   - `PROJECT-CONTEXT.md`: Stack, Pfade, Quellen-Links, Tools, Constraints *(alle Skills lesen sie zuerst)*
   - `_ux-reference.md`: Brand-Farben, Typo, Komponenten-Palette *(Quelle für `ux-advisor`)*
   - `_content-guidelines.md`: Voice/Tone, Terminologie *(Quelle für `content-advisor`)*
   **Prinzip: Quellen verlinken statt duplizieren.** Fehlende Quellen werden als protokollierte
   Lücken festgehalten (kein Blocker). Auch die Advisors verweisen auf dieses Setup, sobald ihnen
   Kontext fehlt: niemand muss von selbst daran denken.
3. `specs/briefing.md` schreiben, dann `/roadmap`.
4. `research/` wächst mit: gestufter Research-Intake (Heatmaps, Audits, Interviews).

Diese 3 Dateien gehören ins jeweilige Projekt-Repo, nicht hierher. Dieses Kit bleibt
**projekt- und firmenneutral**; firmen- oder projektspezifisches Wissen (Tokens, Prozesse,
Beispiele) lebt im jeweiligen Projekt-Workspace.

### Auf das Produkt-Repo zugreifen (zwei Repos gleichzeitig)

Der Normalfall mit diesem Kit: Deine Session läuft im **Design-Workspace**, aber das echte
Produkt (Komponenten, Tokens, Texte) liegt in einem **anderen Repo**. Das ist kein Problem und
kein Grund, Dateien zu kopieren. Drei Wege, vom schnellsten zum dauerhaftesten:

1. **Pro Session**: In Claude Code `/add-dir /pfad/zum/produkt-repo` eingeben. Damit ist das
   Produkt-Repo für diese Session als zusätzliches Arbeitsverzeichnis registriert und Claude
   kann dort lesen.
2. **Dauerhaft für den Workspace**: In der `.claude/settings.json` des Design-Workspace
   hinterlegen, dann gilt es in jeder Session automatisch:
   ```json
   {
     "permissions": {
       "additionalDirectories": ["/pfad/zum/produkt-repo"]
     }
   }
   ```
3. **Immer zusätzlich**: Den Pfad in `PROJECT-CONTEXT.md` verlinken (macht
   `/setup-design-workspace` automatisch). Das ist die Landkarte, über die Skills und Advisors
   wissen, **wo** sie suchen sollen; Weg 1 oder 2 gibt ihnen die **Erlaubnis** dazu.

Beruhigend dabei: Die Advisors sind read-only, im Produkt-Repo wird nur gelesen, nie geändert.
Fehlt die Freigabe, fragt Claude einfach nach, es kann nichts kaputtgehen.

## Die Bausteine: Skill, Agent, Kontextdatei, Artefakt

Damit klar ist, was dieses Repo eigentlich anbietet (und wann man was baut):

| Baustein | Was es ist | Wann es das Richtige ist |
|---|---|---|
| **Skill** (`skills/`) | Ein abrufbarer **Prozess**: ein Schritt-für-Schritt-Rezept, das per `/name` in deiner Session läuft und dich bis zu einem definierten Ergebnis führt | Wiederholbarer Ablauf mit klarem Output, z. B. `/research-design` (Ablauf → `RESEARCH.md`) oder `/setup-design-workspace` (Interview → gefüllte Kontextdateien) |
| **Agent** (`agents/`) | Eine **Perspektive**: ein Spezialist mit eigenem Kontextfenster und eigenen Tools, der von der Session oder aus einem Skill heraus gerufen wird, separat arbeitet und Findings zurückliefert | Ein Prüfblick oder Sparringspartner statt eines Ablaufs, z. B. alle Advisors. Der `jobs-advisor` ist deshalb ein Agent: man konsultiert ihn, man führt ihn nicht aus |
| **Kontextdatei** (`.claude/` im Projekt) | **Wissen**: Fakten über dein Projekt (Stack, Tokens, Guidelines, Quellen), die Skills und Agents zuerst lesen | Alles, was projektspezifisch ist und sich nicht bei jedem Aufruf ändern soll |
| **Artefakt** (`docs/redesign/…` im Projekt) | Ein **Ergebnis** des Loops: `RESEARCH.md`, Design Brief, `EXPLORE.md`, `VERIFY.md`. Der prüfbare Anker, gegen den iteriert wird | Entsteht durch die Skills; wird nie von Hand ins Kit geschrieben |

Faustregel: **Prozess → Skill · Perspektive → Agent · Wissen → Kontextdatei · Ergebnis → Artefakt.**

Noch zwei Begriffsklärungen: **„Agent" und „Sub-Agent" meinen hier dasselbe**, die Advisors
laufen technisch als Subagents deiner Hauptsession (eigener Kontext, kommen mit einem Report
zurück). Und Skills und Agents arbeiten zusammen, nicht konkurrierend: Skills **rufen** Agents
an den passenden Stellen (z. B. holt `/explore-design` beim Vergleich die Zweitmeinung der
Advisors ein); Agents ändern nie etwas, Skills schon.

## Inventar

### Skills (`skills/`)

| Skill | Phase | Was er tut |
|---|---|---|
| `/setup-design-workspace` | Onboarding | Quellen-Interview bei Projektstart: Produkt/Code, DS, Content, Analytics/Tracking, A/B-Tool, Competitor-Analysen, Anbindungen → füllt die Kontextdateien + `research/`-Inventar |
| `/roadmap` | Vorbau | Zerlegt `specs/briefing.md` in eine priorisierte Redesign-Roadmap (nur Probleme/Requirements, keine Lösungen) |
| `/research-design` | Empathize | Evidenzbasierte Discovery: Daten synthetisieren, Ist-Produkt heuristisch auditieren, messbares Research-Ziel formulieren |
| `/brainstorm-design` | Define | Research-Hypothesen priorisieren, schärfen und per Frage-Loop bis ~90 % Confidence härten |
| `/spec-design` | Define | Design Brief: Problem, Scope, Constraints, Komponenten-Intent, UX-Outcome-Akzeptanzkriterien |
| `/explore-design` | Ideate/Prototype | Divergente Exploration: 2–3 HTML-Prototyp-Richtungen auf einem Vergleichs-Canvas mit Live-Reglern, dann Wahl |
| `/implement-design` | Prototype (hi-fi) | Baut die gewählte Richtung in Figma zur finalen Fidelity aus (DS-Tokens des Projekts) |
| `/verify-design` | Test | Gleicht das Figma-Ergebnis gegen Design Brief und Research-Ziel ab (Screenshot-Diff, a11y, Token-Compliance) |
| `/handoff-design` | Übergabe (optional) | Dev-Handoff-Paket: Element→Token→Komponente-Mapping aus dem verifizierten Design |

### Advisor-Agents (`agents/`, read-only: kritisieren & schlagen vor, ändern nie)

| Advisor | Linse | Fokus |
|---|---|---|
| `jobs-advisor` | Add-on (Perspektive) | Steve-Jobs-Denkweise als Kritiker & Brainstorming-Partner: Einfachheit, Fokus, Detail-Anspruch (Taste als Provokation, kein Beweis) |
| `ux-advisor` | Desirability | UX-Entscheidungen, a11y (Pflicht-Baseline), Heuristiken, Verhaltensdaten |
| `research-advisor` | Desirability | Heuristik-/Experten-Audit des Ist-Produkts nach `_audit-standards.md` (4 Lenses), opt. Live-Walkthrough |
| `content-advisor` | Desirability | Copy/Microcopy/Tonalität gegen Content-Guidelines, i18n-Längen |
| `conversion-advisor` | Viability | CRO-/Trust-Linse, an messbaren Research-Zielen verankert |
| `ds-architecture-advisor` | Feasibility | Design-System-Architektur, Library-Pflege, Token-Migration |
| `feasibility-advisor` | Feasibility | Aufwand (= Info, kein Veto), Wiederverwendung, dev-ready Handoff |

### Templates & Referenzdocs (`docs/`)

`WORKFLOW.md` (voller Ablauf) · `_audit-standards.md` (neutraler Audit-Standard) ·
Template-Stubs `PROJECT-CONTEXT.md`, `_ux-reference.md`, `_content-guidelines.md` ·
`settings.json`

## Für Devs

Auch wenn die Zielgruppe Designer:innen sind: Devs sollen sich hier wohlfühlen. Der Loop endet
auf Wunsch in `/handoff-design` mit einem eindeutigen Übergabe-Paket (Element→Token→Komponente,
Alt→Neu-Diff), das ohne Rückfragen umsetzbar sein soll. Die Feasibility-Linse holt technische
Realität früh in den Prozess, als Information für Entscheidungen, nicht als Bremse. Ein
TDD-Code-Track (Spec → Tests → Implementierung → Verify) existierte hier als Keim und wurde
bewusst ausgelagert; er ist unter dem Git-Tag `code-track-archive` konserviert und wird bei
Bedarf ein **eigenes Plugin**.

## Backlog / Ziele

- [x] Entfirmung: alle firmenspezifischen Referenzen aus Skills/Advisors entfernt
- [x] Onboarding-Verhalten: Skills/Advisors fragen aktiv nach, wenn Projekt-Kontextdateien fehlen
- [x] `/setup-design-workspace`: strukturiertes Quellen-Interview bei Projektstart (Tracking, A/B, Competitor-Analysen, Anbindungen)
- [x] Dev-Erbe ausgelagert: Code-Track entfernt (Git-Tag `code-track-archive`), Positionierung auf Design-Loop geschärft
- [ ] **Übersetzung auf Englisch** (alle Skills, Advisors, Docs), Voraussetzung fürs Public-Schalten
- [ ] **Vokabular-Migration mit dem EN-Pass**: Dev-Sprache aus den Skill-Inhalten („Spec" → „Design Brief", ggf. Skill-Umbenennung `/spec-design` → `/design-brief`, Artefakt-Namen)
- [ ] Repo **public** schalten (nach EN-Übersetzung + finalem Review)
- [ ] **Zwiegespräch-Add-on: Steve Jobs × Jony Ive.** Zwei Perspektiven-Advisors im Dialog, die eine Design-Frage untereinander abwägen (Jobs: Fokus/Verdikt, Ive: Material/Form/Care) und dem User das destillierte Für/Wider liefern (beschlossen, kommt später)
- [ ] Nachschärfen: Advisors explizit als Desirability/Feasibility/Viability-Panel framen (auch in den Agent-Beschreibungen)
- [ ] Nachschärfen: Test-/Eval-Checkliste neu aufsetzen (plugin-basiert statt Kopier-Installation)
- [ ] Eval: Kit einmal in einem fremden Projekt durchspielen und Reibungspunkte fixen
- [ ] Code-Kit als eigenes Plugin aus dem Tag `code-track-archive` heben, wenn gebraucht

## Credits

- Der Loop-Ansatz stammt ursprünglich aus einem internen **Workshop zu Spec-Driven
  Development**; hier vom Dev-Kontext gelöst und auf Design Thinking umgemünzt.
- Der HTML-Prototyp-Canvas-Ansatz in `explore-design` (mehrere Varianten auf Tabs + Live-Regler)
  ist inspiriert von
  **[dan-carino/design-directions-skill](https://github.com/dan-carino/design-directions-skill)**,
  hier DS-treu und evidenzbasiert adaptiert.
