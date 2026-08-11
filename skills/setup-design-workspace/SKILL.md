---
name: setup-design-workspace
description: Onboarding eines neuen Design-Workspace (oder Auffrischen eines bestehenden). Führt ein strukturiertes Quellen-Interview (Produkt/Code, Design-System, Content, Analytics/Tracking, A/B-Testing, Competitor-Analysen, Research-Bestand, gewünschte Anbindungen/Zugänge), füllt daraus die 3 Projekt-Kontextdateien und legt research/ mit Quellen-Inventar an. Nutzen bei Projektstart, wenn Kontextdateien fehlen oder Stubs sind, oder wenn jemand "setup"/"onboarding" sagt. Skills und Advisors verweisen hierher, wenn ihnen Projektkontext fehlt.
argument-hint: "[optional: projektname]"
---

# Setup: Design-Workspace onboarden

Einmalig pro Projekt (wiederholbar: bei erneutem Aufruf nur die Deltas erfragen). Ziel: **so viele
Referenzen wie möglich von Anfang an registrieren**, damit der Design-Loop ab Tag 1 mit Evidenz
arbeitet und niemand daran denken muss, Quellen nachzureichen — unabhängig vom Erfahrungslevel.
Antworte in der Sprache des Users; sobald das Interview (Block E) eine Arbeitssprache festlegt,
in dieser.

## Schritt 1 — Bestandsaufnahme (nichts doppelt fragen)
Prüfe, was schon existiert, und frage **nur nach den Lücken**:
1. `.claude/PROJECT-CONTEXT.md`, `.claude/_ux-reference.md`, `.claude/_content-guidelines.md` —
   vorhanden? Noch Template-Stub (`<...>`-Platzhalter) oder gefüllt?
2. `research/` — vorhanden? Was liegt drin?
3. `specs/briefing.md` — existiert schon ein Briefing?
4. Verfügbare Anbindungen: welche MCP-Connectors/Tools sind in dieser Session registriert
   (Analytics, Ticketsystem, Figma …)?

## Schritt 2 — Quellen-Interview (per `AskUserQuestion`, in Blöcken)
Regeln: max. 4 Fragen pro Block · jede Frage hat eine Option **„gibt es nicht / weiß nicht"**
(= protokollierte Lücke, **kein Blocker**) · bei „gibt es" direkt nach Link/Pfad/Zugang fragen ·
Antworten sofort notieren, nichts erfinden.

**Block A — Produkt & Code**
- Produkt-Repo / Code-Quelle? (Pfad/URL — echte Komponenten, DS-Tokens, echte Texte)
- Live-/Staging-URL des Ist-Produkts? (für Audits/Walkthroughs)
- Plattform(en)? (Web, iOS/Android, beides)

**Block B — Design & Content**
- Design-System? (Figma-Library, Token-Datei, Storybook — Quelle der Wahrheit)
- Brand-/Content-Guidelines? (Voice/Tone, Terminologie, Do/Don'ts)
- Bestehende Design-Dateien/Screens? (Figma-URL, fileKey)

**Block C — Daten, Tracking & Experimente**
- **Analytics-/Tracking-Tool?** (z. B. GA4, Clarity, Hotjar, Amplitude, Matomo — was misst ihr heute?)
- **A/B-Testing-/Feature-Flag-Tool?** (z. B. Optimizely, Kameleoon, LaunchDarkly, hausintern)
- **Zugang/Anbindung gewünscht?** Für jedes genannte Tool klären: Soll es angebunden werden
  (MCP-Connector einrichten, API-Zugang, regelmäßiger Export nach `research/`) oder liefert der
  User Daten manuell? Anbieten, die Anbindung direkt einzurichten.
- Bekannte Ziel-Metriken/KPIs? (Conversion, Drop-off, NPS — was zählt als Erfolg?)

**Block D — Research-Bestand**
- **Competitor-Analysen?** (vorhanden → nach `research/` verlinken/ablegen; nicht vorhanden →
  fragen: **„Brauchst du eine? Ich kann eine erstellen"** und als Angebot/Lücke notieren)
- Interviews / Usability-Tests / Umfragen? (Notizen, Aufzeichnungen, Reports)
- Heatmaps / Session-Recordings / Funnel-Daten? (Exporte oder Tool-Zugang)
- Frühere Audits, Support-Tickets, App-Store-/Shop-Reviews? (indirekte Nutzersignale)

**Block E — Sprache & Perspektiven**
- **Arbeitssprache(n)?** In welcher Sprache (oder welchen Sprachen) will der User arbeiten und
  Antworten/Artefakte bekommen? **Mehrere sind erlaubt**, auch gemischt (z. B. Deutsch + Englisch).
  Als Recommended-Option die Sprache vorschlagen, in der der User gerade schreibt. Das Kit selbst
  ist sprachagnostisch — nichts ist fest auf eine Sprache eingestellt.
- **Produkt-/Content-Sprache?** Falls abweichend von der Arbeitssprache (z. B. auf Deutsch
  arbeiten, aber das Produkt ist englisch): getrennt festhalten — Reports/Dialog in der
  Arbeitssprache, produktnahe Artefakte (Copy, Prototypen-Texte) in der Produktsprache.
- **Eigene Audit-Perspektive (Projekt-Lens)?** Soll das Audit zusätzlich zu den 4 Kern-Lenses
  eine eigene Perspektive anwenden — ein anderes heuristisches Set (z. B. ISO 9241-110,
  Shneiderman) oder ein Bedürfnis aus dem Projekt heraus (z. B. Regulatorik, Senior-Tauglichkeit)?
  Je gewünschter Lens erfragen: **Name · Quelle/Referenz · worauf sie prüft**.

## Schritt 3 — Ergebnisse verankern (Quellen verlinken statt duplizieren)
1. Die 3 Kontextdateien aus den Templates füllen (Templates liegen im design-toolkit-Plugin
   unter `docs/`): `PROJECT-CONTEXT.md` (Stack, Pfade, Quellen-Links, Tools, Constraints,
   Akzeptanz-Defaults, **Arbeitssprache(n) + ggf. Produktsprache** aus Block E) ·
   `_ux-reference.md` (nur falls kein DS verlinkbar) · `_content-guidelines.md` (nur falls keine
   Guidelines verlinkbar).
2. **Audit-Standards ins Projekt kopieren:** `audit-standards.md` aus dem design-toolkit-Plugin
   (liegt neben der `research-design`-SKILL.md, `skills/research-design/audit-standards.md`) als
   `.claude/_audit-standards.md` ablegen. Wurden in Block E **Projekt-Lenses** genannt, sie dort
   im Abschnitt „Projekt-Lenses" eintragen (Name · Quelle · Prüffokus). Diese Kopie ist die Datei,
   die Advisors und Audits im Projekt lesen.
3. `research/` anlegen mit **`research/README.md` als Quellen-Inventar**: Tabelle
   *Quelle · Status (vorhanden/angebunden/Lücke) · Ort/Zugang · Notiz*. Lücken sind
   **erstklassige Einträge**, keine Fußnoten.
4. Gewünschte Anbindungen umsetzen oder als To-do mit Ansprechpartner festhalten.

## Schritt 4 — Abschluss-Report
Kurz zusammenfassen: **registriert** (mit Links) · **angebunden** (Tools/Connectors) ·
**Lücken** (inkl. abgelehnter/offener Angebote wie Competitor-Analyse) · **nächster Schritt**:
`specs/briefing.md` schreiben, dann `/roadmap`. Die Lücken-Liste wandert als Startpunkt in die
„Wissens-Lücken" von `/research-design`.

## Du tust NICHT
Quellen erfinden, Platzhalter als „gefüllt" verkaufen, oder ohne Rückfrage externe Zugänge
einrichten. Jede Anbindung nur mit explizitem Go des Users.
