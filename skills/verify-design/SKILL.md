---
name: verify-design
description: Phase 5 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Gleicht das finale Figma-Design gegen die Design-Spec UND das messbare Research-Ziel ab — Screenshot-Diff, a11y, Token-Compliance, plus optionale leichte Nutzervalidierung — und entscheidet über den nächsten Loop. Nutzen nach implement-design.
argument-hint: "[feature]"
---

# Phase 5/5 — Verify (Design-Track): Abgleich & Loop-Entscheidung

Design-Track (Figma). Prüft das **finale Design** gegen die Spec und das **messbare Research-Ziel**
(kein Test-Suite-Lauf — der gehört in den Dev-Prozess; kein Dev-Handoff — das ist `handoff-design`).
Antworte auf Deutsch.

Feature: **`$ARGUMENTS`**.

## Zuerst lesen (Pflicht)
`docs/redesign/$ARGUMENTS/SPEC.md`, `…/EXPLORE.md`, `…/RESEARCH.md`, `…/BRAINSTORM.md`,
`.claude/PROJECT-CONTEXT.md`.

## Prüfungen
1. **Design ↔ Spec** — via `get_screenshot` Element für Element gegen Intent + geforderte Zustände.
2. **UX-Outcome (führend)** — adressiert das Design das **messbare RESEARCH-Ziel** plausibel?
   Begründung an Heuristik/Evidenz, nicht an Geschmack.
3. **a11y** — Kontrast AA, sichtbarer Fokus, Labels/aria, Touch-Targets ≥ 44px.
4. **Token-Compliance** — keine Alt-Token-Reste; nur `<neu-*>`-Tokens, keine festen Hex-Werte.
5. **Optionale leichte Validierung** (empfohlen, wenn machbar) — Preference-/5-Sekunden-/
   Mini-Usability-Test, der das UX-Finding mit **Daten** statt nur Advisor-Meinung stützt. Fehlt
   die Möglichkeit → als Risiko notieren, kein Blocker.

## Gegen-Check (Agent-Tool)
`ux-advisor` (führend), `content-advisor` (Copy/i18n), `conversion-advisor` (löst das Design das
messbare Ziel?), `ds-architecture-advisor`, `feasibility-advisor`.

## Output — `docs/redesign/$ARGUMENTS/VERIFY.md`
- Akzeptanzkriterien als **Checkliste ✅/❌** (je mit Beleg: Node-ID / Screenshot / Validierung),
- Findings mit Schweregrad,
- **Empfehlung:** **Pass** → bereit für Dev-Übergabe (**/handoff-design** ausführen, wenn das
  Design in Code soll) · **Fail** → welche Phase wiederholen.

## Loop
Bei **Fail** zur **kleinsten passenden Phase** zurück (research-design / brainstorm-design /
spec-design / explore-design / implement-design) und erneut bis **/verify-design** — bis alle
Kriterien ✅ sind. Der Dev-Handoff (`handoff-design`) ist **nicht Teil des Loops** — er läuft erst
nach Pass und nur, wenn das Design an die Entwicklung übergeben wird.
