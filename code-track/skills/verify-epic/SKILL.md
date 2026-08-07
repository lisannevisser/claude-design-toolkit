---
name: verify-epic
description: Project-specific by design — reads the project context from .claude/PROJECT-CONTEXT.md. Phase 4 of the loop — checks the implemented epic against its spec (acceptance criteria covered by passing tests, token compliance, a11y, requirement coverage) and decides whether the loop closes (Pass) or returns to the smallest fitting phase (Fail). Use after /implement-epic.
argument-hint: "[epic-id|epic-name]"
---

# Phase 4/4 — Verify Epic (check against the spec & loop decision)

Epic to verify: **`$ARGUMENTS`**.
Goal: check the **implemented code + tests against the spec** and decide whether the loop
closes (Pass) or returns to the smallest fitting phase (Fail).

## Read first (mandatory)
`specs/$ARGUMENTS/$ARGUMENTS-spec.md`, `specs/$ARGUMENTS/PRD.md`,
the implemented code under `src/components/`, the tests, and `.claude/PROJECT-CONTEXT.md`.

## Checks
1. **Code ↔ Spec** — every requirement and acceptance criterion in the spec is implemented
   and backed by a passing test. Walk the spec's coverage map item by item.
2. **Tests** — run the full relevant suite (unit + e2e where applicable) plus lint/typecheck;
   everything must be green. No skipped or weakened tests covering an AC.
3. **Token compliance** — no legacy-token leftovers; `grep` the touched code to confirm
   only the project's current DS tokens are used per the spec's mapping.
4. **a11y** — contrast AA, visible focus, labels/aria, touch targets ≥ 44px.
5. **Requirement/finding** — the originating PRD requirement/finding is measurably solved.
6. **Design parity (if a design handoff exists)** — the built code matches the
   `docs/redesign/<feature>/HANDOFF.md` mapping (element→token→component) and the design
   `VERIFY.md` acceptance; no drift from the approved Figma design. On drift, fail back to the
   smallest fitting phase (design `implement-design` if the design itself is wrong).

## Counter-check (Agent tool)
Call the advisors: `ux-advisor`, `ds-architecture-advisor`, `coding-advisor`, `feasibility-advisor`.

## Output — `specs/$ARGUMENTS/VERIFY.md`
- Acceptance criteria as a **checklist ✅/❌** (each with evidence: test name / file).
- Findings with severity.
- **Recommendation**: Pass → done / Fail → which phase to repeat.

## Loop
On **Fail**, go back to the **smallest fitting phase** (brainstorm / write-spec /
implement-epic) and re-run up to **/verify-epic** — until all criteria are ✅.
