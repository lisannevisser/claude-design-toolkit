---
name: handoff-design
description: Optionaler Schluss-Schritt des DESIGN-Loops (Spec-Driven Design, Figma-Track). Leitet aus einem VERIFIZIERTEN Figma-Design das Dev-Handoff-Paket ab — Element→Token→Komponente-Mapping, Alt→Neu-Diff, Code-Connect-Hinweise — und setzt den Relay zum Code-Track. Bewusst aus dem Design-Loop herausgelöst: läuft ERST, wenn ein Design abgenommen ist und an Dev übergeben wird. (Code-Track-Pendant-Brücke zu write-spec/implement-epic.)
argument-hint: "[feature]"
---

# Schluss-Schritt (optional) — Handoff (Design-Track): Dev-Paket ableiten

Design-Track (Figma). **Bewusst vom Design-Loop entkoppelt:** Exploration und Verifikation sollen
nicht unter dev-ready-Druck stehen. Dieser Schritt läuft **nur, wenn ein abgenommenes Design an
die Entwicklung übergeht**. Hier entsteht **kein** Design mehr — es wird aus dem **gebauten**
Design abgeleitet. Antworte auf Deutsch.

Feature: **`$ARGUMENTS`**.

## Harte Vorbedingung — stoppen, wenn nicht verifiziert
Suche `docs/redesign/$ARGUMENTS/VERIFY.md` mit Empfehlung **Pass**. Fehlt sie oder ist sie **Fail**,
**STOPPE** und verweise auf **/verify-design `$ARGUMENTS`**. Kein Handoff aus unverifiziertem Design.

## Zuerst lesen (Pflicht)
1. `docs/redesign/$ARGUMENTS/SPEC.md` + `…/VERIFY.md` — Intent, Akzeptanz, Verifikations-Ergebnis.
2. `.claude/PROJECT-CONTEXT.md` — Figma-Links/Node-IDs, Token-Sets, Constraints, Komponenten-Pfade.

## Vorgehen — aus dem GEBAUTEN Design ableiten (nicht aus der Absicht)
1. `get_design_context` auf die finalen Nodes (aus `implement-design`).
2. `HANDOFF.md` erzeugen:
   - **Mapping Element → Token → Ziel-Komponente** (welche `src/components/...` setzt das um),
   - **Alt→Neu-Token-Diff** (`<alt-*>` → `<neu-*>`, vollständig),
   - **Code-Connect-Hinweise** (via **/figma-code-connect** → `add_code_connect_map`,
     Figma-Komponente ↔ `src/components/...`),
   - **Constraints-Hinweise** (extern gehostete Zahlungsfelder, i18n-Längen, Feature-Flags).
3. **dev-ready-Check** — `feasibility-advisor` (eindeutig ohne Rückfragen umsetzbar? Wiederverwendung
   maximiert?). Tiefer gehende Code-Stil-/Software-Architektur-Prüfung gehört in die **separate
   Code-Kit** (deren `architect-advisor`/`coding-advisor`), nicht in diesen Design-Schritt.

## Relay zum Code-Track (verbindlich)
Setze oben in `HANDOFF.md` eine Zeile **`Code-Epic: <ID|tbd>`** (die Roadmap-Epic, die dieses
Design in Code umsetzt). Diese Datei ist die **verbindliche Design-Quelle** für den Code-Track:
`write-spec`/`implement-epic` lesen sie, übernehmen Token-Mapping & Komponenten-Intent (erfinden
sie nicht neu) und notieren rückverweisend **`Design-Feature: $ARGUMENTS`**. `verify-epic` prüft
später **Design-Parität** (gebauter Code ↔ Handoff-Mapping).

## Output — `docs/redesign/$ARGUMENTS/HANDOFF.md`

## Gate
Handoff an Dev übergeben. Wird im **separaten Code-Kit** weitergebaut, startet dieser dort mit
**/write-spec** (liest dieses `HANDOFF.md` als bindenden Input). Andernfalls dient das `HANDOFF.md`
jedem beliebigen Dev-Prozess als dev-ready Vorlage.
