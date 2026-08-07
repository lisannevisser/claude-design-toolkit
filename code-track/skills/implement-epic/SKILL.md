---
name: implement-epic
description: Project-specific (payment-form-new). Phase 3 of the loop — takes an epic name and implements it from its technical spec following a TDD agentic flow: analyze the spec, build tests from it, implement the requirements, run the tests, and fix until everything passes. Stops if no spec exists. Finishes with a report mapping every acceptance criterion to done / partly / not done. Use when an accepted spec exists, or when someone says "implement-epic <epic>".
argument-hint: "[epic-id|epic-name]"
---

# Phase 3/4 — Implement Epic (TDD agentic flow)

Epic to implement: **`$ARGUMENTS`**.
Goal: implement **`$ARGUMENTS`** until **all requirements of its spec are implemented and
confirmed by passing tests**, then report acceptance-criteria coverage.

## Hard precondition — stop if there is no spec
1. Resolve `$ARGUMENTS` to an epic ID (`E2`) if a title/synonym was given.
2. Look for the technical spec at **`specs/$ARGUMENTS/$ARGUMENTS-spec.md`**.
3. **If the spec does not exist, STOP immediately.** Do not implement from the PRD or from
   intent. Tell the user to run **/write-spec `$ARGUMENTS`** first, then end execution.

## Read first (mandatory)
1. `specs/$ARGUMENTS/$ARGUMENTS-spec.md` — the binding spec (requirements, ACs, TDD tasks,
   architecture decisions). This is the single source of truth.
2. `specs/$ARGUMENTS/PRD.md` — for requirement/AC context.
3. `.claude/PROJECT-CONTEXT.md` — stack, component paths, test commands, constraints, defaults.
4. The affected components under `src/components/Elements/` and `src/components/UI/`, plus the
   existing tests next to them, to match conventions.
5. The design handoff for this epic, if it exists — `docs/redesign/<feature>/HANDOFF.md` (found
   via the spec's `Design-Feature:` line). When present it is **binding**: the
   element→token→component mapping and Code-Connect hints are authoritative — implement to match
   the approved Figma design, do not improvise visuals.

## Workflow (loop until all tests pass)
Work in slices, one spec requirement/AC at a time, strictly **test-driven**:

1. **Analyze the specification.** Build a checklist of every requirement and acceptance
   criterion. Note the TDD tasks the spec already defined and the architecture decisions to
   honour. Identify the test command(s) from PROJECT-CONTEXT.md (unit + any e2e/Playwright).
2. **Build the tests according to the spec.** For each slice, write the failing test(s) first
   — they encode the acceptance criteria (behaviour, states, a11y AA, i18n de/fr/nl, no `ts-*`
   leftovers, flag parity). Run them and confirm they fail for the right reason (red).
3. **Implement the requirements.** Write the minimum code to satisfy the tests, following the
   spec's architecture decisions and using only new tokens (`trstd-*`), reusing existing
   design-system components. Then refactor while keeping tests green.
4. **Verify by running the tests.** Run the full relevant suite (unit + e2e where applicable),
   plus lint/typecheck if PROJECT-CONTEXT.md defines them.
5. **Fix until everything passes.** Iterate steps 3–4 until **all tests are green**. Never
   weaken or skip a test to make it pass — fix the implementation. If a spec requirement is
   genuinely untestable or blocked, stop and flag it rather than faking coverage.

Repeat the slice loop until every requirement/AC on the checklist is covered by a passing test.

## Optional second opinion (Agent tool)
- `feasibility-advisor` — reuse, technical constraints, anything not dev-ready.
- `coding-advisor` — **consult whenever a code-style or code-organization choice surfaces**
  mid-implementation (file/folder placement, naming, component vs util split, imports, types,
  test layout); it checks against `.claude/_coding-guidelines.md` so the change stays consistent.
- `ds-architecture-advisor` — consistency with the design system & token migration.
- `architect-advisor` — **consult whenever a software/code architecture decision arises**
  mid-implementation (where code lives, Server Action vs client, state/data flow, env/config,
  integration boundary, reuse-vs-build); it checks against `.claude/_architecture-reference.md`.
- `ux-advisor` — **consult whenever a UX decision arises** mid-implementation (layout/flow,
  form design, copy clarity, error/empty/loading states, component choice, accessibility,
  default selection); it checks against `.claude/_ux-reference.md` and `research/`, with WCAG
  AA as the non-negotiable baseline.

## Finish — coverage report
When all tests pass, finish and output a **report** that maps **every acceptance criterion**
from the spec to a status:

| AC | Requirement | Status | Evidence (test / file) |
|----|-------------|--------|------------------------|
| AC1 | … | ✅ done | `<test name / path>` |
| AC2 | … | 🟡 partly | what's missing + why |
| AC3 | … | ❌ not done | reason / blocker |

Summarise: tests run/passing, files touched, any accepted risks, and what (if anything) is
**partly** or **not done** with the reason.

## Gate
- All ACs ✅ **done** → continue with **/verify-epic `$ARGUMENTS`**.
- Anything 🟡 partly / ❌ not done → loop back to the smallest fitting phase
  (write-spec if the spec is wrong, brainstorm if the requirement itself is unclear).
