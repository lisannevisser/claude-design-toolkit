---
name: explore-design
description: Phase 3 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Divergente visuelle Exploration — zuerst SCHNELLE HTML-Prototypen (2–3 Richtungen) auf einem interaktiven Vergleichs-Canvas für Frühfeedback, dann eine Richtung begründet wählen. Das Herzstück der visuellen Designarbeit. Nutzen, nachdem die Design-Spec steht. (Speist implement-design.)
argument-hint: "[feature/roadmap-item]"
---

# Phase 3/5 — Explore (Design-Track): schnelle HTML-Richtungen → Wahl

Design-Track. Hier wird **divergiert, bevor konvergiert wird**. Bewusst zuerst **schnelle,
interaktive HTML-Prototypen** statt Figma: sie geben in Minuten erstes Feedback, schaffen
Sicherheit und prüfen, ob wir auf dem richtigen Weg sind. Das **finale** Design entsteht danach in
Figma (`implement-design`). Antworte auf Deutsch.

> **Credit:** Der Prototyp-Canvas-Ansatz (mehrere HTML-Varianten auf Tabs + Live-Regler via
> CSS-Variablen/`postMessage`) ist inspiriert von **dan-carino/design-directions-skill**
> (https://github.com/dan-carino/design-directions-skill). Wir adaptieren ihn DS-treu und
> evidenzbasiert.

Feature: **`$ARGUMENTS`**.

## Harte Vorbedingung — Spec muss existieren
Suche `docs/redesign/$ARGUMENTS/SPEC.md`. **Fehlt sie, STOPPE** und verweise auf
**/spec-design `$ARGUMENTS`**. Die Spec definiert **Problem + Constraints** — die Lösung findet diese Phase.

## Zuerst lesen (Pflicht)
1. `docs/redesign/$ARGUMENTS/SPEC.md` — Problem, Scope, Constraints, Akzeptanz.
2. `docs/redesign/$ARGUMENTS/RESEARCH.md` — **messbares Ziel** (daran werden Richtungen gemessen).
3. `.claude/PROJECT-CONTEXT.md` + `.claude/_ux-reference.md` + `.claude/_content-guidelines.md` —
   **Produkt-Repo, DS-Quelle, Content-Guidelines.**

## Scoping (nur explore-spezifisch — Rest ist via Briefing/Roadmap/Spec/Survey geklärt)
Frage knapp über `AskUserQuestion`, falls nicht klar: **Anzahl Richtungen** (Default 3), **Fidelity**
(DS-treu vs. Wireframe), **Differenzierungs-Achse** — *was* variiert über die Richtungen
(z. B. Informationshierarchie / Layout-Prinzip / Grad an Progressive Disclosure / Trust-Signale).
Eine klare Achse verhindert kosmetisch-gleiche Varianten.

## Step A — schnelle HTML-Prototypen auf einem Vergleichs-Canvas
1. **DS-Treue bestimmen:** Ist DS/Produkt-Repo registriert → die **echten Token-Werte** (Hex/
   CSS-Variablen) aus der Config des Produkt-Repos **auslesen und exakt** als CSS-Variablen-Defaults
   verwenden — **nicht schätzen/approximieren**. Sonst → **Wireframe-Niveau** (klar kennzeichnen).
2. **Real content only** — Texte/Labels/Längen aus dem Produkt-Repo bzw. nach Content-Guidelines.
   **Kein Lorem Ipsum.**
3. **2–3 divergente Richtungen** als eigenständige HTML-Dateien bauen, je nach der gewählten Achse
   deutlich unterschiedlich. Vanilla HTML/CSS/JS, kein Build. Die **a11y-Baseline gilt auch im
   Prototyp** (sichtbarer Fokus, Labels/Semantik, Tastatur) — nicht erst in Figma.
4. **Vergleichs-Canvas** (eine HTML-Datei) zusammenstellen: Richtungen nebeneinander in Tabs/Grid,
   je mit **Ein-Satz-Konzept** (z. B. „A · Klarer Fokus auf eine Primäraktion") + **Trade-off-Notiz**,
   und **Live-Reglern** (CSS-Variablen via `postMessage`: Akzent, Hintergrund, Schriftgrößen …) für
   interaktives Durchprobieren. Die Regler explorieren **innerhalb** des DS — final gewählte Werte
   müssen auf **die DS-Tokens des Projekts zurückmappbar** sein (kein beliebiger Hex als Endergebnis).
5. **Ablage:** `docs/redesign/$ARGUMENTS/explore/` (Canvas + Richtungs-Dateien). Pfade festhalten.

## Step B — vergleichen & wählen
1. **Vergleichsmatrix** je Richtung gegen: **Research-Ziel**, UX-Heuristiken, a11y-Baseline, grobe
   Umsetzbarkeit. Stärken/Schwächen je Richtung.
2. **Zweitmeinung** (Agent-Tool): `ux-advisor` vergleicht (Evidenz/Heuristik/a11y);
   `conversion-advisor` rankt nach Wirkung aufs Ziel (bei Bezahl-/Trust-Strecken);
   `content-advisor` prüft Copy; `ds-architecture-advisor` prüft DS-Fit; `feasibility-advisor`
   gibt eine **leichte** Aufwandseinschätzung.
3. **Optionale leichte Validierung** (empfohlen, wenn machbar) — Preference-/5-Sekunden-Test
   zwischen den Richtungen → Wahl mit **Daten statt Geschmack**. Sonst als Risiko notieren.
4. **Eine Richtung wählen** (oder Synthese der besten Elemente), **Begründung an das Research-Ziel
   gekoppelt**. Verworfene Richtungen + Grund festhalten (nicht löschen).

## Output — `docs/redesign/$ARGUMENTS/EXPLORE.md` (+ `explore/`-Prototypen)
- **Richtungen** (je: Konzept-Satz + Trade-off + Pfad zur HTML-Datei),
- **Vergleichsmatrix** (Richtung × Ziel/Heuristik/a11y/Aufwand),
- **Validierungs-Ergebnis** (falls durchgeführt) oder Risiko-Notiz,
- **Gewählte Richtung + Begründung** (an Research-Ziel gekoppelt) + verworfene Richtungen & Grund.

## Gate
Wahl mit dem Team teilen → dann **/implement-design `$ARGUMENTS`** (gewählte Richtung final in Figma).
