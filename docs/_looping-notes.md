# Looping-Architektur — Arbeitsnotizen (noch kein Standard)

Vorüberlegungen für den Backlog-Punkt „Looping-Architektur". Wird in einer eigenen Session
ausgearbeitet; bis dahin gilt der bestehende Workflow unverändert.

## Das Spannungsfeld

Zwei berechtigte Ziele widersprechen sich scheinbar:

1. **Autonomie**: Agents sollen selbstständig loopen können (Audit, Competitive-Analyse,
   Synthese), ohne dass der User jeden Schritt anstößt.
2. **Feedback**: Der User darf nie stundenlang ohne Rückmeldung sein und muss an den
   entscheidenden Stellen die Richtung bestimmen.

Auflösung: **Nicht Autonomie ODER Check-ins, sondern beides auf verschiedenen Ebenen.**

## Drei Ebenen

| Ebene | Wer entscheidet | Beispiel |
|---|---|---|
| **Mikro-Loop** (autonom) | Claude selbst, gegen den schriftlichen Anker | bauen → selbst prüfen → nachbessern, bis Kriterien erfüllt oder Budget erschöpft |
| **Arbeitspaket** (parallel) | Orchestrierende Session | Audit ∥ Competitive-Analyse ∥ Daten-Synthese als parallele Subagents; Zwischenbericht nach jedem Rücklauf |
| **Gate** (User) | Der User, immer | 90%-Survey, Spec-Abnahme, Richtungswahl in explore-design |

Der Trick: **Check-ins und Loops entkoppeln.** Während der User an einem Gate Feedback gibt,
dürfen unabhängige Pakete weiterloopen. Ein Gate hält nur an, was von der Entscheidung abhängt.

## Claude als sein größter Kritiker (Selbstkorrektur)

Damit Mikro-Loops konvergieren statt drehen:

- **Prüfbarer Anker als Abbruchkriterium**: Der Loop endet nicht bei „gefällt mir", sondern
  wenn die Akzeptanzkriterien aus dem Brief erfüllt sind (deshalb ist der schriftliche Anker
  Zutat Nr. 1 des Kits).
- **Selbstkritik vor Abgabe**: Vor jedem Zwischenbericht prüft Claude das eigene Ergebnis
  gegen den Anker (Mini-verify) und korrigiert selbst, was korrigierbar ist. Nur was eine
  echte Entscheidung braucht, geht an den User.
- **Advisors als interner Störimpuls**: Die read-only Advisors können auch *innerhalb* eines
  Mikro-Loops gerufen werden (nicht nur an Gates), um Selbstbestätigung zu verhindern.
- **Rücksprungregel bleibt**: Bei Fail zurück in die kleinste passende Phase, nie auf Anfang.

## Kommunikations-Regeln (Entwurf)

- Nach jedem zurückkehrenden Subagent: 1–3 Sätze Zwischenstand an den User.
- Kein Mikro-Loop ohne Budget (Iterations- oder Zeitgrenze); bei Budget-Ende ehrlicher
  Bericht statt weiterdrehen.
- Fragen sammeln und an Gates bündeln, statt den User mitten im Fanout zu unterbrechen —
  außer bei Blockern.

## Offene Fragen für die Ausarbeitungs-Session

- Wo genau in `/research-design` wird der Fanout verankert (Skill-Text vs. WORKFLOW-Grundsatz)?
- Wie meldet ein noch laufender Loop Zwischenstände, wenn die Hauptsession am Gate wartet?
- Welche Mikro-Loop-Budgets sind sinnvoll (Iterationen? harte Kriterienliste?)?
- Braucht verify-design einen „Selbst-Verify light" als wiederverwendbaren Baustein für
  Mikro-Loops?
