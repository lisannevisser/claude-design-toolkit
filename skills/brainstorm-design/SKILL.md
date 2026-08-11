---
name: brainstorm-design
description: Phase 1 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Nimmt die rohen Research-Hypothesen, priorisiert und schärft sie und härtet sie über einen Survey-Loop bis ~90% Confidence zu spec-reifen Redesign-Hypothesen. Das eine harte Discovery-Gate. Nutzen, nachdem research-design die Datenlage + Lücken geschärft hat.
argument-hint: "[feature/roadmap-item]"
---

# Phase 1/5 — Brainstorm (Design-Track): Hypothesen härten bis ~90%

Design-Track (Figma). Output ist ein gehärtetes Hypothesen-Dokument. Hier wird **priorisiert und
committet**, was `research-design` roh geliefert hat. Antworte in der in `.claude/PROJECT-CONTEXT.md` hinterlegten Arbeitssprache; fehlt der Eintrag, in der Sprache, in der der User schreibt.

Feature: **`$ARGUMENTS`**. Ist `$ARGUMENTS` leer/unklar, frage über `AskUserQuestion` nach.

## Harte Vorbedingung — auf Research aufsetzen
Suche `docs/redesign/$ARGUMENTS/RESEARCH.md`. **Fehlt sie, STOPPE** und verweise auf
**/research-design `$ARGUMENTS`**. Keine Hypothesen aus dem Nichts.

## Zuerst lesen (Pflicht)
1. `docs/redesign/$ARGUMENTS/RESEARCH.md` — Insights, **Lücken**, Baseline/Ziel, **erste Hypothesen**.
2. `.claude/PROJECT-CONTEXT.md` — Produkt-Repo, Token-Sets, Constraints, Defaults.
3. Ist-Code/Ist-UI der Zielkomponente im Produkt-Repo.

## Vorgehen
1. **Ist-Zustand verorten** — Zustände/Varianten, Flows, Fehlerfälle; genutzte Alt-Tokens (Inventar
   ggf. aus RESEARCH). Out-of-Scope explizit (z. B. Zahlungslogik, Pricing, Backend).
2. **Hypothesen priorisieren & schärfen** — aus den rohen RESEARCH-Hypothesen die **3–5 stärksten**
   wählen, je an ein belegtes Finding **und das messbare Ziel** gekoppelt, im Format **„Wenn wir X
   ändern, erwarten wir Y, weil Z (Evidenz)"**. Offene Lücken aus RESEARCH adressieren oder als
   Risiko führen.
3. **Zweitmeinung** (Agent-Tool, UX-lastig): `ux-advisor` (Heuristik/a11y) zuerst;
   `ds-architecture-advisor` (DS & Token-Migration), `feasibility-advisor` (grobe Machbarkeit); bei
   Bezahl-/Trust-Bezug `conversion-advisor`. Findings als eigener Abschnitt.

## Survey-Loop bis ~90% Confidence (das harte Gate — nur Full-Modus)
**Honoriere den `Modus` aus RESEARCH.md:** Bei **Express** entfällt dieser Loop — ein leichter
Durchlauf (Hypothesen bestätigen/schärfen, **kein hartes Gate**), bei Bedarf auf Full eskalieren.
Bei **Full**:
Stelle offene Punkte **aktiv per `AskUserQuestion`** (nicht nur passiv ins BRAINSTORM.md parken) und
protokolliere Frage + Antwort im Q&A-Log:
- je **4 auf RESEARCH+App zugeschnittene Optionen**, alle mit `[]`, **eine „Recommended" (zuerst)**,
  **nie selbst auswählen**;
- Antworten **in direkte Hypothesen-/Aussagen einarbeiten**, beantwortete Fragen unten entfernen,
  **Q&A-Log je Zyklus behalten**;
- **mit dem User so lange fragen, bis die Confidence > 90 %** ist — das Kit **kann das Gate nicht
  selbst schließen**. Pflege eine Zeile **`Confidence: NN%`** oben und aktualisiere sie jede
  Iteration (abgeleitet: sind die Hypothesen belegt, priorisiert, spec-reif?). Nie einen veralteten
  Wert stehen lassen.
- **Nur wenn der User wirklich nicht erreichbar ist** (echt autonomer Lauf): bei der offenen Survey
  stoppen, die aktuelle Confidence melden — **niemals Antworten erfinden**, um das Gate künstlich zu
  schließen.

## Output — `docs/redesign/$ARGUMENTS/BRAINSTORM.md`
- **`Confidence: NN%`** oben,
- **Ist-Zustand** (Komponenten, Alt-Tokens, Zustände, Flows, Fehlerfälle),
- **Gehärtete Hypothesen** (3–5, X/Y/Z, je mit RESEARCH-Finding + Ziel verlinkt, priorisiert),
- **Advisor-Findings**,
- **Q&A-Log** + ggf. verbleibende Risiken.

## Gate
Bei ~90% mit dem Team teilen → dann **/spec-design `$ARGUMENTS`**.
