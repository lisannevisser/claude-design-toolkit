---
name: spec-design
description: Phase 2 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Schreibt den Redesign-Brief (Design-Spec) — Problem, Scope, Constraints, Komponenten-Intent und UX-Outcome-Akzeptanzkriterien. Definiert das ZU LÖSENDE PROBLEM, nicht die visuelle Lösung (die findet die Exploration). Nutzen, nachdem die brainstorm-design-Hypothesen stehen.
argument-hint: "[feature]"
---

# Phase 2/5 — Spec (Design-Track): der Redesign-Brief

Design-Track (Figma). Output ist ein **Design Brief** (Design-Spec), kein technisches Dev-Dokument.
**Wichtig:** Die Spec definiert das **Problem + die Constraints + die Erfolgskriterien** — sie
schreibt **nicht** die visuelle Lösung vor. Die entsteht divergent in `explore-design`. Antworte
auf Deutsch.

Feature: **`$ARGUMENTS`**.

## Harte Vorbedingung — stoppen, wenn kein BRAINSTORM existiert
Suche `docs/redesign/$ARGUMENTS/BRAINSTORM.md`. **Existiert es nicht, STOPPE sofort** und
verweise auf **/brainstorm-design `$ARGUMENTS`**. Keine Spec aus dem Nichts erfinden.

## Zuerst lesen (Pflicht)
1. `docs/redesign/$ARGUMENTS/BRAINSTORM.md` — Hypothesen + Evidenz.
2. `docs/redesign/$ARGUMENTS/RESEARCH.md` — **messbares Ziel** (wird zum Erfolgskriterium).
3. `.claude/PROJECT-CONTEXT.md` — Stack, Pfade, Token-Sets, Constraints, Defaults.
4. Token-Quelle des Projekts **im registrierten Produkt-Repo** (z. B. `tailwind.config.*` / CSS-Vars)
   — Quelle der Wahrheit fürs Alt→Neu-Mapping (als Referenz; verbindliche Bindung später).

## Inhalt der Design-Spec
1. **Problem & Ziel** (1–2 Sätze, an ein Brainstorm-Finding + das messbare RESEARCH-Ziel gekoppelt).
   Beschreibe **was besser werden muss**, nicht wie es aussieht.
2. **Scope / Out-of-Scope.**
3. **Constraints** — i18n-Längen, Feature-Flags, extern gehostete Felder, Responsiveness,
   Wiederverwendung bestehender Komponenten.
4. **Komponenten-Intent** — welche **Zustände** (default/hover/focus/disabled/error/loading …) und
   **Varianten** die Lösung abdecken muss. (Funktionaler Intent, keine Pixel.)
5. **Alt→Neu-Token-Mapping** als **Referenz** (verbindliche Token-Bindung erfolgt erst in
   implement-design/handoff):

   | Element | Alt (`<alt-*>`) | Neu (`<neu-*>`) | Notiz |
   |---|---|---|---|

6. **Akzeptanzkriterien — UX-Outcome zuerst:**
   - **Das messbare RESEARCH-Finding ist adressiert** (Ziel benennen; Messweg in verify),
   - Clarity/Trust-Kriterien aus den Hypothesen (prüfbar formuliert),
   - **a11y AA** (Kontrast, sichtbarer Fokus, Labels/aria, Touch-Targets ≥ 44px) — Baseline,
   - **Handoff-Readiness-Baseline** (gilt erst an der Dev-Übergabe): keine Alt-Token-Reste,
     Wiederverwendung bestehender Komponenten.
7. **Offene Punkte** beantwortet oder als Risiko markiert.
8. **Relay-Handle** — oben in `SPEC.md` eine Zeile **`Code-Epic: <ID|tbd>`** (die Roadmap-Epic,
   die dieses Redesign später in Code umsetzt). So findet der Dev-Prozess das passende Artefakt.

## Zweitmeinung (Agent-Tool — früh = UX-lastig)
- `ux-advisor` — Problem/Akzeptanz an Evidenz & Heuristik geschärft, a11y-Baseline.
- `content-advisor` — Copy-/Microcopy-Intent gegen die Content-Guidelines, i18n-Längen.
- `conversion-advisor` — bei Bezahl-/Trust-Strecken: ist das Conversion-Ziel sauber adressiert?
- `feasibility-advisor` — Scope realistisch / Wiederverwendung maximiert.
- `ds-architecture-advisor` — Token-Mapping-Referenz & DS-Konsistenz (leichtgewichtig hier).
Findings einarbeiten.

## Output — `docs/redesign/$ARGUMENTS/SPEC.md`

## Gate
Spec vom Team abnehmen → dann **/explore-design `$ARGUMENTS`** (divergente Richtungen).
