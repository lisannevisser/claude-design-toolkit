---
name: research-design
description: Phase 0 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Evidenzbasierte Discovery — vorhandene Daten synthetisieren, das Ist-Produkt heuristisch auditieren (via research-advisor), eine messbare Baseline + Ziel festhalten, erste Hypothesen ableiten und vor allem Wissens-LÜCKEN sichtbar machen. Nutzen, BEVOR ein Redesign-Bereich angefasst wird. (Speist brainstorm-design.)
argument-hint: "[feature/roadmap-item]"
---

# Phase 0/5 — Research (Design-Track): informierte Discovery

Erste Phase des **Design-Tracks** (Figma). Ziel: die UX-Arbeit auf **Daten und Evidenz** stellen
**und bewusst machen, was wir NICHT wissen**. Output ist ein Research-Dokument mit Insights,
**Lücken**, messbarer Baseline/Ziel und ersten Hypothesen. Antworte in der in
`.claude/PROJECT-CONTEXT.md` hinterlegten Arbeitssprache; fehlt der Eintrag, in der Sprache,
in der der User schreibt.

Feature: **`$ARGUMENTS`**. Ist `$ARGUMENTS` leer/unklar, frage über `AskUserQuestion` nach, welcher
Redesign-Bereich (idealerweise ein Item aus `specs/roadmap.md`) gemeint ist.

## Harte Vorbedingung — Material muss da sein
Research braucht etwas zum Auditieren. **Ist weder ein Produkt-Repo/Figma in `PROJECT-CONTEXT.md`
registriert NOCH Material in `research/` vorhanden, STOPPE und frage den User** (`AskUserQuestion`)
nach der Quelle (Repo/Figma/Screens) oder dem Material. **Niemals aus dem Nichts auditieren oder
Findings erfinden** — ohne Quelle gibt es keine belegten Insights, nur Lücken.

## Modus-Triage — Vorschlag + einmalige Bestätigung
Nach kurzem Sichten von Item-Beschreibung, `briefing.md` und einem **schnellen Scan** der
Zielkomponente **den Research-Modus vorschlagen und einmal kurz per `AskUserQuestion` bestätigen
lassen** (mit 1-Satz-Begründung). So behält der User die Kontrolle, und eine **Fehl-Triage** (ein
großes Thema fälschlich als „klein") wird vermieden, bevor sie teuer wird:
- **Express (autonom)** — kleine/klare Änderung, geringe Unsicherheit, Migration-/a11y-Fix: Audit
  läuft **im Hintergrund** (`research-advisor` liest Code/Figma), erzeugt RESEARCH + AUDIT, **kein
  Survey-Loop/Gate**; biete am Ende an, bei Bedarf auf **Full** zu eskalieren.
- **Full (interaktiv)** — größer / UX-/Conversion-relevant / unklar: volle Evidenz + **interaktiver
  Survey** (unten) mit dem User.

Signale: Änderungsumfang · Unsicherheit (ist das Problem klar?) · UX-/Conversion-Stakes. Den
gewählten Modus oben in `RESEARCH.md` als **`Modus: Express|Full`** festhalten und an
`brainstorm-design` durchreichen.

## Zuerst lesen (Pflicht)
1. `.claude/PROJECT-CONTEXT.md` — **Produkt-Repo-Pfad**, DS-/Content-Links, Research-Quellen,
   Constraints (immer zuerst).
2. `specs/briefing.md` (+ `specs/roadmap.md`, **falls vorhanden**) — Projektziel + adressiertes
   Problem. Fehlt die Roadmap (z. B. Einzelkomponenten-Test), genügt das Briefing.
3. **Alles in `research/`** — Heatmaps/Recordings, Analytics, Audits, Interviews (Primärmaterial).
4. Ist-Code/Ist-UI der Zielkomponente im **registrierten Produkt-Repo**.
5. Falls Figma-URL/Node vorhanden: `get_screenshot` + `get_metadata` auf den Ist-Stand.

## Vorgehen
1. **Verfügbare Evidenz erfassen** — im **Full-Modus** den User **aktiv fragen** (`AskUserQuestion`),
   welche Quellen existieren (Clarity/Heatmaps, Analytics/Funnel, Audits, Interviews/Usability) —
   **nicht nur den `research/`-Ordner scannen**. Im **Express-Modus** autonom aus vorhandenem
   Material/Code arbeiten (keine Fragerunde). Dann die vorhandenen Daten synthetisieren: was sagen sie über
   **Friktion** (Drop-off, Rage-/Dead-Clicks, Abbruchstellen, Fehlerraten)? Strikt **belegt** vs.
   **angenommen** trennen.
2. **Ist-Produkt auditieren → eigene Reports `AUDIT.md` + `AUDIT.html`** — **zuerst den
   verbindlichen Standard lesen: `audit-standards.md` direkt neben dieser SKILL.md** (Lenses,
   Severity-Skala, Befund-Format, Report-Struktur, Pin-Report). Existiert im Projekt eine Kopie
   `.claude/_audit-standards.md` (legt `/setup-design-workspace` an, ggf. mit Projekt-Lenses),
   hat sie Vorrang. Dann `research-advisor` rufen (Heuristik-/Experten-Audit, a11y-Erstcheck,
   Friction-Inventar; optional Live-Walkthrough per Browser). Bei Bezahl-/Entscheidungs-Strecken
   zusätzlich `conversion-advisor`. **Sind die Advisors nicht registriert (z. B. in Claude Chat),
   das Audit inline nach demselben Standard durchführen** und das vermerken. Ablage: **Markdown-
   Report** `docs/redesign/$ARGUMENTS/AUDIT.md` (Findings nach Severity, je Finding
   `file:line`/Node-ID/Screenshot) **plus interaktiver Pin-Report `AUDIT.html`** (Pflicht, s.
   Standard; in Claude Chat als Artefakt); `RESEARCH.md` referenziert/synthetisiert sie.
3. **Gestufter Intake** — fehlende Stufe ist eine **Lücke**, kein Blocker: a11y (Pflicht-Baseline),
   Heuristiken (immer), Verhaltensdaten/Audits/Interviews (aus `research/`, falls vorhanden).
   Fehlen harte Zahlen, dürfen `WebSearch`/`WebFetch` Benchmarks liefern (als „angenommen" markieren).
   **Liegt Research nur auf Strecken-/Produkt-Ebene vor** (nicht element-spezifisch), die relevanten
   Punkte heraussichten und die **element-spezifische Lücke explizit markieren** — nicht als
   element-belegt verbuchen.
4. **UX-Baseline + messbares Ziel** je Kernproblem (Baseline → Ziel, z. B. „Drop-off −X %"). Fehlt
   eine Zahl: qualitative Baseline + als Annahme markieren. Dieses Ziel ist später das Erfolgsmaß.
   **Ist das Item migrations-/konsistenz-/a11y-getrieben ohne Verhaltensdaten, ist ein hartes
   Metrik-Ziel nicht erzwingbar** — dann ein heuristisches/qualitatives Ziel + a11y-/Token-Kriterien
   als Erfolgsmaß setzen (kein erfundenes Metrik-Ziel).
5. **Erste Hypothesen ableiten** — aus Daten + Audit, im Format **„Wenn wir X ändern, erwarten wir
   Y, weil Z (Evidenz)"**. Bewusst noch roh/breit; das Priorisieren/Schärfen macht `brainstorm-design`.

## Survey-Loop — auf Wissen/Nicht-Wissen (nur Full-Modus; KEIN hartes Gate)
Stelle dem User die Fragen **aktiv per `AskUserQuestion`** (nicht nur passiv ins Dokument parken)
und protokolliere Frage + Antwort im Q&A-Log von RESEARCH.md, um die Evidenz-Landschaft zu kartieren:
- je **4 Optionen**, alle mit `[]`, **eine „Recommended" (zuerst platziert)**, **nie selbst wählen**;
- **immer eine Option „weiß nicht / unbekannt"** zulassen — eine so markierte Frage wird zur
  **explizit protokollierten Lücke**, nicht zum Blocker;
- Antworten in Insights/Baseline/Hypothesen einarbeiten, **Q&A-Log behalten**, beantwortete Fragen
  unten entfernen.
- **mit dem User** beantworten; das Kit treibt die Fragen aktiv und **kann den Survey nicht selbst
  schließen**. Nur wenn der User wirklich nicht erreichbar ist: stoppen, Stand melden, **nie erfinden**.
Ziel ist **nicht** Antwort-Sicherheit, sondern **Bewusstsein**: was wissen wir belegt, was nicht.
Halte eine Zeile **`Evidenz-Abdeckung: NN%`** (wie gut ist die Landschaft kartiert) + kurzes Log.

## Output — `docs/redesign/$ARGUMENTS/RESEARCH.md` (+ `AUDIT.md` + `AUDIT.html`)
- **`Modus: Express|Full`** (oben, mit 1-Satz-Begründung der Triage),
- **`AUDIT.md` + `AUDIT.html`** — der eigenständige Heuristik-/Experten-Audit-Report (Quelle für
  die Insights) plus interaktiver Pin-Report nach `audit-standards.md`.
- **Insights** (je Finding: Quelle + Severity; belegt vs. angenommen klar getrennt),
- **Wissens-Lücken & Risiken** — *erstklassiger Abschnitt* (was fehlt, „weiß nicht"-Antworten),
- **UX-Baseline + messbares Ziel** (Tabelle: Problem · Baseline · Ziel · Quelle),
- **Erste Hypothesen** (X/Y/Z-Format, roh),
- **Advisor-Befunde** (`research-advisor`, ggf. `conversion-advisor`),
- **Evidenz-Abdeckung + Q&A-Log**.

## Gate
Insights + Lücken + Ziele mit dem Team teilen → dann **/brainstorm-design `$ARGUMENTS`**.
