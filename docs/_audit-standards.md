# Audit-Standards (Design-Kit)

Verbindlicher Standard für **Heuristik-/Experten-Audits** im Design-Loop. Angewendet vom
`research-advisor` (erzeugt `AUDIT.md` in Phase 0) und referenziert vom `conversion-advisor`
(Lenses 2 + 4). Projekt-neutral; **Marken-Spezifika** liegen in `_ux-reference.md` /
`_content-guidelines.md`.

## Die 4 Lenses — auf JEDES Audit anwenden
1. **Nielsens 10 Usability-Heuristiken.** Gegen **alle 10** prüfen, **vollen Heuristik-Namen**
   ausschreiben (z. B. „Visibility of System Status", nie Abkürzungen). Heuristiken **ohne Befund
   dokumentieren**, damit die volle Abdeckung sichtbar ist. Die 10: Visibility of System Status ·
   Match Between System and the Real World · User Control and Freedom · Consistency and Standards ·
   Error Prevention · Recognition Rather Than Recall · Flexibility and Efficiency of Use ·
   Aesthetic and Minimalist Design · Help Users Recognize, Diagnose, and Recover from Errors · Help
   and Documentation.
2. **Conversion-Psychologie.** Fokus: Pricing, Commitment, Entscheidungsarchitektur. Referenzen:
   https://www.coglode.com/cookbook und https://lawsofux.com/. (Vertieft beim `conversion-advisor`.)
3. **Brand/CI & Voice.** Gegen die im Projekt hinterlegten Marken-/CI-Guidelines prüfen (siehe
   `_ux-reference.md` / `_content-guidelines.md`): generisch vs. **distinct on-brand** flaggen
   (Tonalität, visuelle Identität, Vertrauenssignale).
4. **Dark Patterns.** Potenzielle Dark Patterns flaggen (Brignull-Taxonomie, FTC-Guidelines, EU-
   Verbraucherschutz). Je Fund: **Muster beschreiben → ethisches Bedenken → Manipulationsrisiko →
   White-Pattern-Alternative** (als edukative Referenz, nicht als fertige Lösung).

## Severity-Skala
- 🔴 **Critical (P0)** — blockiert/unterdrückt das primäre Conversion-Ziel deutlich. Vor Launch fixen.
  Schließt billig-jetzt-teuer-später-Themen ein (Naming, Informationsarchitektur).
- 🟡 **Major (P1)** — spürbare Friktion / verpasste Chance. Killt Conversion nicht allein, summiert
  sich. In erster Iteration fixen.
- 🔵 **Minor (P2)** — Politur, Optimierung, Brand-Alignment. Fixen, wenn Bandbreite da ist.
- ⚠️ **Dark Pattern Risk** — kein Usability-Bug, sondern Trust-/Legal-/Ethik-Bedenken. Separat
  bewertet, mit White-Pattern-Alternative.

## Befund-Format — Tabelle
Alle Findings in **einer Tabelle**, **nach Severity sortiert** (Critical → Major → Minor → Dark
Pattern Risk). Spalten:

| # | Severity | Titel | Location / Element-Pfad | Heuristik (voller Name) | Problem | Conversion-Impact | Hypothese |
|---|---|---|---|---|---|---|---|

- **Heuristik:** voller Name + Cross-Refs (nie Abkürzungen).
- **Problem:** ein knapper Satz. **Conversion-Impact:** eine Zeile.
- **Hypothese:** conversion-psychologisch — welches Mental Model wirkt, warum das aktuelle Design
  gegen das Ziel arbeitet.
- **Nicht nach Heuristik gruppieren** — Severity ist die Sortierung.

## Report-Struktur (`AUDIT.md`)
- **Severity-Legende** zuerst.
- **Findings-Tabelle** (Format oben), **nach Severity sortiert**. **Nie nach Heuristik gruppieren.**
- **„Was die Seite gut macht"** (3–5 Punkte — Credit, wo verdient).
- **Disclaimer (genau einmal):** „Findings beschreiben Probleme und Hypothesen, keine Lösungen.
  **Die Ergebnisse dieses Audits sollten von einer UX-Fachkraft validiert werden**, und jede
  Umsetzung von ihr geprüft und geformt werden."
- **„Heuristiken ohne Befund"**-Tabelle am **Ende** (für volle Abdeckung).
- **Optional:** annotiertes Wireframe-SVG (weißer Hintergrund, Legende oben, nummerierte Marker;
  Farbcode dunkelrot = Critical, rot = Major, blau = Minor) zur Verortung der Findings.

## Schreibregeln
- Kurz, direkt, **meinungsstark** („Das ist ein Problem", kein „könnte man erwägen"). Sparringspartner.
- **Credit geben**, wo verdient — nicht nur Mängel.
- **Keine Em-Dashes**; Kommas/Punkte/Umbau stattdessen.
- **Fett nur für Sub-Labels** der Findings, nicht im Fließtext.
- Schlüpft eine Empfehlung rein, als **„Idee"** labeln + „mit dem UX-Team verifizieren".
- Belegt vs. angenommen trennen; Severity konsequent vergeben (a11y-Verstoß = per Default hoch).
