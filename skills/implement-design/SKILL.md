---
name: implement-design
description: Phase 4 des DESIGN-Loops (Spec-Driven Design, Figma-Track). Baut die in explore-design GEWÄHLTE Richtung in Figma zur finalen Fidelity aus — mit dem neuen Designsystem (neu-* Tokens), allen Zuständen, Varianten, Responsiveness und i18n-Längen. KEIN Dev-Handoff hier (das ist handoff-design, entkoppelt). Nutzen, wenn eine Richtung gewählt ist. (Code-Track-Pendant: implement-epic.)
argument-hint: "[feature]"
---

# Phase 4/5 — Implement (Design-Track): gewählte Richtung final bauen

Design-Track (Figma). Hier wird die **gewählte Richtung** aus der Exploration **final** in Figma
gebaut — sauber, vollständig, mit dem neuen Designsystem. Hier wird in Figma gebaut, nicht in Code
(das macht der separate Code-Track). **Der Dev-Handoff ist bewusst ausgelagert** (→ `handoff-design`),
damit das finale Design nicht unter dev-ready-Druck entsteht. Antworte auf Deutsch.

Feature: **`$ARGUMENTS`**.

## Harte Vorbedingung — stoppen, wenn keine gewählte Richtung existiert
Suche `docs/redesign/$ARGUMENTS/EXPLORE.md` mit einer **gewählten Richtung**. Fehlt sie,
**STOPPE** und verweise auf **/explore-design `$ARGUMENTS`**. Ohne explorierte Wahl wird hier nicht
gebaut.

## Zuerst lesen (Pflicht)
1. `docs/redesign/$ARGUMENTS/EXPLORE.md` — **gewählte Richtung + Node-IDs + Begründung**.
2. `docs/redesign/$ARGUMENTS/SPEC.md` — Intent, Constraints, Akzeptanz (verbindlich).
3. `.claude/PROJECT-CONTEXT.md` — Figma-Links/Node-IDs, Token-Sets, Constraints.

## Vorgehen — finale Fidelity
> **Pflicht:** Vor `use_figma` / `generate_figma_design` zuerst **/figma-use** laden; für ganze
> Screens zusätzlich **/figma-generate-design**.
>
> **Vorbedingung — schreibfähiges Figma-MCP:** Ist nur ein read-only/Dev-Mode-Figma-MCP verbunden
> (kein `use_figma`/`generate_figma_design`), **zuerst versuchen, es zu installieren/verbinden** —
> über die MCP-Registry bzw. `claude mcp add`, oder den User gezielt anleiten, Figma-Desktop + das
> schreibende MCP-Plugin (Dev Mode MCP mit Schreibzugriff) zu aktivieren. **Erst wenn das
> nachweislich nicht gelingt**, als Alternative einen build-fertigen **HTML-Blueprint** der
> gewählten Richtung (optional + Original zum Vergleich) liefern und den Figma-Build in eine Session
> mit Write-MCP verweisen. Der Blueprint dient dort + dem Handoff als exakte Vorlage.

1. `search_design_system` + `get_variable_defs` → echte **neue** Tokens (`<neu-*>`) ermitteln.
2. Die **gewählte Richtung** vollständig ausbauen: **nur `<neu-*>`-Tokens, keine festen
   Hex-Werte**, bestehende DS-Komponenten bevorzugen. Alle in der Spec geforderten **Zustände**
   (default/hover/focus/disabled/error/loading …), **Varianten**, **Responsiveness** und
   **i18n-Längen** abdecken.
3. Während des Bauens `ds-architecture-advisor` rufen (Konsistenz mit dem neuen DS, fehlende
   Komponenten/Tokens vorschlagen).
4. **Finale Node-IDs festhalten** — Input für /verify-design und (später) /handoff-design.

## Optional — HTML-Prototyp für Interaktion
Wo Interaktion in Figma schlecht abbildbar ist (komplexe Loading-States, Transitions, dynamische
Validierung), darf ergänzend ein **interaktiver HTML-Prototyp** entstehen (DS-treu, real content),
abgelegt unter `docs/redesign/$ARGUMENTS/explore/` oder `…/final-interaction/`. Er ergänzt das
Figma-Design, ersetzt es nicht.

## Output
Finales Figma-Design (Node-IDs notiert) **+ optional** HTML-Interaktions-Prototyp. **Kein**
HANDOFF.md hier — das entsteht in `handoff-design`, erst nach bestandener Verifikation.

## Gate
→ **/verify-design `$ARGUMENTS`**.
