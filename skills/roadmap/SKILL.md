---
name: roadmap
description: Vorbau des DESIGN-Loops. Zerlegt das user-geschriebene specs/briefing.md in eine priorisierte Roadmap von Redesign-Bereichen (Komponenten/Flows/Seiten) — nur Probleme/Requirements, KEINE Lösungs-/Tech-Entscheidungen. Löst Abhängigkeiten auf, optimiert für parallele Bearbeitung, hält eine feste Obergrenze an Items. Legt die Roadmap immer dir zur Abnahme vor. Nutzen zu Projektbeginn oder wenn jemand "roadmap" sagt. (Einmaliger Vorbau, nicht pro Feature.)
argument-hint: "[optional: max-items]"
---

# Vorbau — Roadmap: Briefing → priorisierte Redesign-Bereiche

Einmaliger Projekt-Vorbau des Design-Tracks. Output ist `specs/roadmap.md` — das **geteilte
Rückgrat**: jedes Item durchläuft erst den Design-Loop und (optional, später) den Code-Loop.
Antworte auf Deutsch.

## Harte Vorbedingung — Briefing muss existieren
Suche `specs/briefing.md`. **Fehlt es, lege es zuerst gemeinsam mit dem User an** (kurzes
Template unten) — eine Roadmap ohne Briefing ist geraten, nicht abgeleitet.

> **Briefing-Minimaltemplate** (falls neu): Produkt & Strecke · Redesign-Ziel (warum jetzt) ·
> messbare Erfolgsziele · Scope (In/Out) · Constraints (i18n, externe Systeme, Flags) ·
> Research-Trigger.

## Zuerst lesen (Pflicht)
1. `specs/briefing.md` — die Projektbeschreibung des Users.
2. `.claude/PROJECT-CONTEXT.md` — Produkt-Repo, DS-/Content-Quellen, Constraints.

## Regeln (Guardrails)
- **Nur Probleme & Requirements** (funktional + ggf. nicht-funktional). **KEINE Lösungs-, Visual-
  oder Tech-/Architektur-Entscheidungen** — die entstehen erst im Loop.
- **Obergrenze:** standardmäßig **max. 5 Items** (oder `$ARGUMENTS`, falls Zahl übergeben).
  Lieber bündeln als zersplittern — und **keine Funktionalität aus dem Briefing verlieren**.
- **Abhängigkeiten auflösen** und für **parallele Bearbeitung optimieren** (z. B. geteilte
  DS-Primitives vor zusammengesetzten Flows).
- Jedes Item = ein sinnvoll abnehmbarer Redesign-Bereich (Komponente/Flow/Seite).

## Survey-Loop (optional, leicht)
Wenn die Priorisierung/Abgrenzung unklar ist, stelle dem User Fragen **ans Ende der Roadmap**:
je 4 auf Briefing+App zugeschnittene Optionen, alle mit `[]`, **eine „Recommended" (zuerst)**,
**nie selbst auswählen**. Antworten in die Items einarbeiten, Q&A-Log behalten.

## Output — `specs/roadmap.md`
- Kurzer Bezug zum Briefing-Ziel (1–2 Sätze).
- **Item-Liste** (je: ID · Name · adressiertes Problem/Ziel · betroffene Bereiche · Abhängigkeiten
  · parallelisierbar ja/nein). Als Dropdown/Tabelle, leicht scanbar.
- **Reihenfolge-Empfehlung** (Abhängigkeiten + Parallelität).
- Coverage-Check: jede Briefing-Funktion ist mindestens einem Item zugeordnet.

## Gate (Abnahme zwingend)
Roadmap **dem User zur Abnahme vorlegen** — nicht eigenmächtig als final betrachten. Nach Abnahme:
pro Item **/research-design `<item>`** starten. Die Item-ID ist später auch die `Code-Epic:`-ID
für den (optionalen) Code-Track.
