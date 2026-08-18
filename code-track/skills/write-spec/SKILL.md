---
name: write-spec
description: Project-specific by design — reads the project context from .claude/PROJECT-CONTEXT.md. Phase 2 of the loop — turns an accepted Epic PRD into a detailed technical specification at specs/<epic>/<epic>-spec.md. Covers every requirement and acceptance criterion, plans the tech implementation TDD-first, highlights key architecture decisions, and collects high-impact architecture/tech choices as selectable [ ] options at the end of the file. Writes a Confidence level into the spec and updates it every iteration. Stops if no PRD exists. Use after a PRD is hardened, or when someone says "write-spec <epic>".
argument-hint: "[epic-id|epic-name]"
---

# Phase 2/4 — Write Spec (technical specification from the PRD)

Epic to spec: **`$ARGUMENTS`**.
Goal: turn the accepted **PRD** into a **binding, testable technical specification** that
covers every requirement and acceptance criterion. The spec is later the single source of
truth for **/implement-epic** and **/verify-epic**.

## Hard precondition — stop if there is no PRD
1. Resolve `$ARGUMENTS` to an epic ID (`E2`) if a title/synonym was given.
2. Look for the PRD at **`specs/$ARGUMENTS/PRD.md`**.
3. **If the PRD does not exist, STOP immediately.** Do not invent one, do not start speccing.
   Tell the user the PRD is missing and that they should run **/brainstorm `$ARGUMENTS`** first,
   then end execution.

## Design-first relay — the design loop runs BEFORE code (read its handoff)
In this project the **design loop is primary and runs first**: a feature is shaped in Figma via
`/brainstorm-design → /spec-design → /implement-design → /verify-design`, and only then turned
into code. Before speccing, locate the design artifacts for this epic:
- Find the matching `docs/redesign/<feature>/` folder — by a `Code-Epic: $ARGUMENTS` line in its
  `SPEC.md` / `HANDOFF.md`, or by the component names the roadmap lists for `$ARGUMENTS`.
- **If `HANDOFF.md` (+ a passed `VERIFY.md`) exists → read it as BINDING design input.** The
  Alt→Neu token mapping, component intent and element→token→component mapping come from there —
  this spec **transcribes** them, it does not re-derive or contradict them.
- **If no design handoff exists, the design loop has not run yet.** Flag this and recommend
  running the design loop first (`AskUserQuestion`). Continue code-first **only** if the user
  explicitly confirms (e.g. a code-only epic like the E1 baseline with no Figma surface).

## Read first (mandatory, in this order)
1. `specs/$ARGUMENTS/PRD.md` — the accepted PRD (requirements + acceptance criteria).
2. The design handoff for this epic, if it exists — `docs/redesign/<feature>/HANDOFF.md` +
   `SPEC.md` (binding design input per the relay above).
3. `.claude/PROJECT-CONTEXT.md` — stack, component paths, token sets, constraints, defaults.
4. The project's token source of truth (e.g. Tailwind config or tokens file — named in
   `PROJECT-CONTEXT.md`), including the legacy→new token sets if the project migrates.
5. Current code of the affected components (component paths from the PRD /
   `PROJECT-CONTEXT.md`).

## Build the spec from the PRD
Every PRD **requirement** and **acceptance criterion** must be covered by the spec — nothing
dropped. Maintain explicit traceability so coverage is verifiable.

1. **Requirement → spec coverage map.** For each PRD requirement/AC, name where the spec
   addresses it. Anything not covered is a gap to resolve before the gate.
2. **Old→new token mapping** as a table (if the project migrates tokens). **If a design `HANDOFF.md`
   exists, transcribe its mapping verbatim** (the design loop already decided it); only fill gaps
   it doesn't cover.

   | Element | Legacy token | New token | Note |
   |---|---|---|---|

3. **Component intent** — states (default/hover/focus/disabled/error …), variants,
   responsiveness, i18n lengths (de/fr/nl — fr & nl run longer).
4. **TDD-first implementation tasks.** Assume **test-driven development** throughout: for each
   slice of behaviour, plan the test(s) **before** the implementation. Order tasks so each is
   "write failing test → implement → green → refactor". Map each task back to the PRD
   requirement/AC it satisfies.
5. **Testable acceptance criteria** (inherited + sharpened from the PRD):
   - a11y AA (contrast) + visible focus + labels/aria + touch targets ≥ 44px
   - no legacy-token leftovers
   - the research/PRD finding is measurably solved

## Highlight key architecture decisions
Call out the **key architecture decisions** inline in a dedicated section — what changes
structurally, why, and the trade-offs. Be explicit about anything that affects component
boundaries, state/data flow, Server Action vs client, env/config, integration boundaries,
shared primitives, or the token migration. For any **software-architecture** decision, consult
the `architect-advisor` (Agent tool) to ground it in `.claude/_architecture-reference.md` and
the real code before writing it down.

## Second opinion (Agent tool)
- `architect-advisor` — software/code architecture (where code lives, state/data flow,
  Server Action vs client, env/config, integration boundary, reuse-vs-build).
- `ds-architecture-advisor` — token mapping & design-system/library consistency.
- `coding-advisor` — **consult for code-style & code-organization decisions** the spec implies
  (file/folder placement, naming, component vs util split, imports, types); grounds them in
  `.claude/_coding-guidelines.md` so the planned code lands consistently.
- `feasibility-advisor` — is the scope realistic / effort reasonable / reuse maximised?
Fold their findings in; they may surface new high-impact decisions for the section below.

## Confidence — write it into the spec, update every iteration
- Put a `**Confidence: NN%**` line near the top of the spec, right under the title.
- Keep a short **Confidence log** at the bottom: one line per iteration —
  `- <iteration> — NN% — what changed / what still blocks ~90%`.
- **Bump the number every time you revise the spec**, derived from the document analysis:
  is every PRD requirement/AC covered, are the TDD tasks concrete, are the high-impact
  decisions resolved or still open? Never leave a stale value.

## Output — `specs/$ARGUMENTS/$ARGUMENTS-spec.md`
File name carries the **`-spec.md` suffix** (e.g. `specs/E2/E2-spec.md`). Contents:
- **Title + `**Confidence: NN%**`** at the very top.
- **`Design-Feature: <docs/redesign/feature>`** (or `none — code-first, confirmed`) — the relay
  back-reference, so the design source of this spec is traceable.
- **Goal** — 1 sentence, tied to the PRD.
- **Scope / Out-of-Scope**
- **Requirement → spec coverage map** (PRD requirement/AC → where it's addressed)
- **Old→new token mapping** (table)
- **Component intent** (states, variants, responsiveness, i18n)
- **Key architecture decisions** (with rationale + trade-offs)
- **TDD implementation tasks** (ordered, each: test-first, mapped to a requirement/AC)
- **Testable acceptance criteria**
- **High-impact decisions — select with `[ ]`** (see below)
- **Confidence log**

## High-impact decisions — selectable options at the end of the file
If there are **high-impact architecture or tech decisions** that the user should choose,
add them as the **last section** so they are easy to act on. Use unchecked checkboxes so the
user can simply tick the ones they want:

```
## High-impact decisions — pick one per group

### D1: <decision title>
- [ ] Option A — <description, trade-off> (Recommended)
- [ ] Option B — <description, trade-off>
- [ ] Option C — <description, trade-off>

### D2: <decision title>
- [ ] Option A — ...
- [ ] Option B — ...
```

Mark the recommended option, but leave all boxes unchecked so the user selects. Once the user
ticks their choices, fold the decisions back into the spec body and bump confidence.

## Gate
Get the spec accepted by the team (and the high-impact decisions selected) → only then
continue with **/implement-epic `$ARGUMENTS`**.
