# Spec-Driven Design Kit — Test-Checkliste

Für Tester:innen, die das Kit im **eigenen Projekt** ausprobieren und prüfen, ob alles wie erwartet
funktioniert. In Claude Code (VS Code) ausführen, **im Repo, in dem du das Kit installiert hast**.
Abhaken und unten Feedback notieren.

> Hinweis: Die Skills/Agents werden aus dem `.claude/` deines Workspaces geladen — du musst Claude
> Code **in diesem Workspace** öffnen, nicht woanders.

## 0. Setup
- [ ] Inhalt von `claude-kit/` (bzw. `ts-setup/.claude/`) nach `<dein-repo>/.claude/` kopiert.
- [ ] **Quellen in `PROJECT-CONTEXT.md` verlinkt** (Produkt-Repo, Design-System, Content-Guidelines).
- [ ] Die 3 Projektdateien gefüllt **oder** verlinkt (`PROJECT-CONTEXT`, `_ux-reference`, `_content-guidelines`).
- [ ] `specs/briefing.md` geschrieben (Produkt, Redesign-Ziel, Scope, Constraints).
- [ ] Optional: `research/` angelegt (Heatmaps/Analytics/Audits/Interviews, falls vorhanden).

## 1. Roadmap (`/roadmap`)
- [ ] Erstellt `specs/roadmap.md` aus dem Briefing.
- [ ] Items enthalten **nur Probleme/Requirements** — **keine** Lösungs-/Tech-Entscheidungen.
- [ ] Max-Item-Grenze respektiert, Abhängigkeiten + Parallelisierung benannt.
- [ ] Wird **dir zur Abnahme vorgelegt** (entscheidet nicht eigenmächtig).

## 2. Research (`/research-design <item>`)
- [ ] **Modus-Triage:** schlägt **Express** oder **Full** vor und **bestätigt einmal per Rückfrage**.
- [ ] Ohne Repo/Figma/Material: **stoppt und fragt** nach der Quelle (auditiert nicht blind).
- [ ] Fragt **aktiv** nach vorhandener Evidenz (Clarity/Analytics/Audits/Interviews) — scannt nicht nur den Ordner.
- [ ] Erzeugt einen eigenständigen **`AUDIT.md`** im Standard-Format (Findings **als Tabelle**, nach Severity).
- [ ] `AUDIT.md` nennt **4 Lenses** (Nielsen-Heuristiken, Conversion-Psychologie, Brand/CI, Dark Patterns) und enthält den Disclaimer „Ergebnisse von UX-Fachkraft validieren lassen".
- [ ] `RESEARCH.md` hat **Insights, Wissens-Lücken (erstklassig), Baseline/Ziel, erste Hypothesen, Evidenz-Abdeckung**.
- [ ] „weiß nicht"-Antworten werden als **Lücke** protokolliert, nicht erfunden.

## 3. Brainstorm (`/brainstorm-design <item>`)
- [ ] Fehlt `RESEARCH.md`: **stoppt** und verweist auf `/research-design`.
- [ ] **Full-Modus:** stellt Survey-Fragen **aktiv per Rückfrage** (4 Optionen, eine „Recommended", nie selbst gewählt).
- [ ] Fragt **mit dir** weiter bis **Confidence > 90 %** — schließt das Gate **nicht selbst**, erfindet keine Antworten.
- [ ] **Express-Modus:** leichter Durchlauf ohne hartes 90%-Gate.
- [ ] `Confidence:`-Zeile + Q&A-Log werden gepflegt.

## 4. Spec (`/spec-design <item>`)
- [ ] Definiert **Problem + Constraints + Akzeptanz**, **nicht** die visuelle Lösung.
- [ ] Akzeptanz ist **UX-Outcome-first** (Research-Ziel), a11y AA als Baseline.
- [ ] Alt→Neu-Token-Mapping als **Referenz** (Quelle = Produkt-Repo-Config).

## 5. Explore (`/explore-design <item>`)
- [ ] Fragt nur **explore-spezifisches** Scoping (Anzahl Richtungen, Fidelity, Differenzierungs-Achse).
- [ ] Baut **2–3 schnelle HTML-Richtungen** + einen **Vergleichs-Canvas** (Tabs + Live-Regler).
- [ ] **DS-treu**, wenn Produkt-Repo/DS registriert — sonst **Wireframe-Fallback** (klar gekennzeichnet).
- [ ] **Real content** aus dem Produkt-Repo, **kein Lorem Ipsum**.
- [ ] a11y-Baseline schon im Prototyp (Fokus, Labels, Semantik).
- [ ] Wahl mit **Begründung am Research-Ziel**; verworfene Richtungen festgehalten.

## 6. Implement (`/implement-design <item>`)
- [ ] Fehlt schreibfähiges Figma-MCP: **versucht zuerst zu installieren/verbinden**, **erst dann** HTML-Blueprint-Alternative.
- [ ] Mit Write-MCP: baut die **gewählte Richtung** final in Figma (nur DS-Tokens, keine festen Hex).

## 7. Verify (`/verify-design <item>`)
- [ ] Prüft Design ↔ Spec, **UX-Ziel**, a11y, Token-Compliance; optionale leichte Validierung.
- [ ] Empfehlung **Pass/Fail**; bei Fail → kleinste passende Phase zurück.

## 8. Handoff (`/handoff-design <item>`, optional)
- [ ] Nur bei **Pass** (sonst stoppt es).
- [ ] Erzeugt `HANDOFF.md` (Element→Token→Komponente, Alt→Neu-Diff, Code-Connect) + `Code-Epic`-Zeile.

## 9. Advisors
- [ ] `ux-advisor`, `research-advisor`, `content-advisor`, `conversion-advisor`, `ds-architecture-advisor`, `feasibility-advisor` lassen sich aufrufen.
- [ ] Sie **ändern nie Dateien** (read-only) und liefern Befunde + Empfehlung.
- [ ] Nicht registrierte Advisors → das Skill macht einen **sauberen Inline-Fallback**.

## Querschnitt — überall prüfen
- [ ] **Nirgends ausgedachte Daten/Findings** ohne Quelle (belegt vs. angenommen getrennt).
- [ ] **a11y AA** ist durchgängig Pflicht-Baseline.
- [ ] Artefakte landen unter `docs/redesign/<item>/`; Projekt-Dateien werden zuerst gelesen.
- [ ] Der Design-Loop läuft **standalone** (ohne Code-Track).

## Feedback (bitte ausfüllen)
| Phase | Funktioniert? (✅/⚠️/❌) | Beobachtung / Vorschlag |
|---|---|---|
| Setup | | |
| Roadmap | | |
| Research | | |
| Brainstorm | | |
| Spec | | |
| Explore | | |
| Implement | | |
| Verify / Handoff | | |
| Advisors | | |

**Getestet von:** `<Name>` · **Projekt:** `<Repo/Touchpoint>` · **Datum:** `<YYYY-MM-DD>`
