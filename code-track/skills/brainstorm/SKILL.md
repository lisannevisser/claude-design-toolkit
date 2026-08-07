---
name: brainstorm
description: Project-specific (payment-form-new). Phase 1 of the loop — breaks an epic from specs/roadmap.md down into a solid Epic PRD in specs/<epic>/PRD.md and hardens it. Creates the PRD from the roadmap if missing, records open questions with options (one marked Recommended), folds answers directly into PRD requirements/acceptance criteria, and keeps asking until confidence reaches ~90%. Writes a Confidence level into the PRD and updates it every iteration. Use when an epic should be worked out, clarified, sharpened or de-risked, or when someone says "brainstorm <epic>".
argument-hint: "[epic-id|epic-name]"
---

# Phase 1/4 — Brainstorm: harden the Epic PRD (payment-form-new)

This skill is **specific to this project** (payment-form-new) — it knows the roadmap epics,
the `specs/` layout and the `ts-*`→`trstd-*` migration directly.

Epic to work on: **`$ARGUMENTS`**.
If `$ARGUMENTS` is empty or unclear, show the epic list from `specs/roadmap.md` and let the
user pick via `AskUserQuestion` before continuing.

Goal of this phase: turn the rough roadmap entry into a **solid, hardened Epic PRD** —
surface open points as questions, convert answered points into concrete requirements and
acceptance criteria, until **confidence reaches ~90%**. No solution, no token mapping, no
design yet — that comes in **/write-spec**.

## Epics of this project (from specs/roadmap.md)
| ID | Title | Depends on |
|----|-------|------------|
| E1 | Redesign Baseline & Cross-Cutting Requirements | — (first) |
| E2 | Payment Entry (`PaymentForm`, `PaymentTypeSelector`) | E1 |
| E3 | Protection & Order Summary (`ProtectionSelector`, `Summary`) | E1 |
| E4 | Membership Upgrade Flow | E1 |
| E5 | Withdrawal Flow (`WithdrawalForm`) | E1 |

`$ARGUMENTS` may be an ID (`E2`) or a title/synonym ("Payment Entry") — map it to the ID.
**E1 is the journey-wide baseline that E2–E5 inherit.** If `$ARGUMENTS` depends on E1 and E1
is not yet accepted, mark this as a dependency/risk in the PRD.

## Read first (mandatory, in this order)
1. `.claude/PROJECT-CONTEXT.md` — stack, component paths, token sets, constraints, defaults.
2. `specs/roadmap.md` — the roadmap entry for `$ARGUMENTS` (scope, requirements, acceptance seed).
3. `specs/briefing.md` — goal, scope, success criteria of the whole programme.
4. Current code of the components belonging to `$ARGUMENTS` under `src/components/Elements/`
   and `src/components/UI/` (see table above + PROJECT-CONTEXT.md).
5. Everything under `research/` (Clarity notes, audits, interview summaries).
6. If a Figma URL/node ID is provided: `get_screenshot` + `get_metadata` on the current state.

## Create the PRD if missing
Location: **`specs/$ARGUMENTS/PRD.md`** (folder by epic ID, e.g. `specs/E2/PRD.md`).
If it does not exist, create it from the roadmap entry for `$ARGUMENTS` — the roadmap seeds
scope, functional/non-functional requirements and first acceptance criteria.
If it already exists, load it and **keep hardening it** (do not rewrite from scratch).

## Procedure (hardening loop)
1. **Sharpen current state & scope** incl. **legacy token inventory**: which `ts-*` tokens do
   the `$ARGUMENTS` components use today? Which states/variants, flows and error cases actually
   exist in the code? What is explicitly out of scope (e.g. Zuora payment logic, pricing, backend)?
2. **Gather evidence in tiers** — a missing tier is an open question, not a blocker:
   - a11y (always the mandatory baseline)
   - heuristics (Nielsen + form design)
   - Clarity data (from `research/`, if available)
   - audits / other sources
3. **Ask open questions — with options.** Every material gap (assumption, ambiguity, risk,
   missing evidence) becomes a clarifying question. Ask it via `AskUserQuestion`:
   - 2–4 concrete options per question,
   - **exactly one marked "(Recommended)" and placed first**,
   - with a short rationale for the recommendation (evidence/constraint).
   For any question touching **software architecture** (where code lives, state/data flow,
   Server Action vs client, env/config, integration boundary, reuse-vs-build), first consult
   the `architect-advisor` (Agent tool) to sharpen the question and ground the Recommended
   option in `.claude/_architecture-reference.md` and the real code.
   For any question touching **UX** (layout/flow, form design, copy clarity, states,
   component choice, accessibility, default selection), first consult the `ux-advisor`
   (Agent tool) to sharpen the question and ground the Recommended option in evidence and
   `.claude/_ux-reference.md`.
   Bundle related questions (up to 4 per round). Also record each question in the PRD's
   **Open questions** section (options + recommendation + status `open`).
4. **Reconcile answers.** Every answered question is folded **immediately** into the PRD as
   **concrete requirements and/or testable acceptance criteria**. The matching open question
   is set to `decided` (with decision + short rationale). Answers never live only in the log —
   always as a direct PRD requirement.
5. **Get a second opinion** via the Agent tool — `ux-advisor`, `ds-architecture-advisor`
   (design-system), `architect-advisor` (software/code architecture), `feasibility-advisor`
   (sequentially or in parallel). Findings go into their own section; they may
   spawn new clarifying questions (back to step 3).
6. **Score confidence & loop.** After each round, estimate confidence (0–100%) against the
   rubric below and **write the new number into the PRD** (see next section).
   **< ~90%:** ask the remaining/new questions and repeat the loop. **≥ ~90%:** gate.

## Confidence — write it into the PRD, update every iteration
The PRD must carry a **live, written confidence level** so anyone reading the file sees how
solid it is right now:
- Put a `**Confidence: NN%**` line near the top of `PRD.md`, right under the title.
- Keep a short **Confidence log** at the bottom: one line per iteration —
  `- <iteration> — NN% — what changed / what still blocks ~90%`.
- **Bump the number on every hardening round**, derived from the document analysis against the
  rubric below. Never leave a stale value.

## Confidence rubric (~90% means)
- Scope & out-of-scope are unambiguous, no open "it depends".
- Every functional requirement has at least one testable acceptance criterion.
- The E1 baseline defaults are referenced: no `ts-*` leftovers, WCAG AA (focus, labels/aria,
  contrast, touch targets ≥ 44px), i18n lengths de/fr/nl, flag parity (Kameleoon),
  "no existing function lost".
- All material assumptions are resolved **or** explicitly marked as an accepted risk
  (with owner/follow-up).
- Advisor findings are incorporated or noted as an open point.

## Output — `specs/$ARGUMENTS/PRD.md`
- **Title + `**Confidence: NN%**`** at the very top.
- **Epic & Goal** — `$ARGUMENTS` + 1 sentence, tied to roadmap/briefing.
- **Scope / Out-of-Scope**
- **Current state** (affected components, legacy tokens in use, states, flows, error cases)
- **Evidence** (per finding: source + severity)
- **Requirements** — functional + non-functional (incl. inherited E1 baseline)
- **Acceptance criteria** — testable, 1:1 with the requirements
- **Open questions** — per question: options, recommendation, status (`open` / `decided` + reason)
- **Risks & assumptions** — explicitly marked
- **Advisor findings** (ux / design-system architecture / software architecture / coding)
- **Confidence log** — one line per iteration (see above)

## Gate
Share/accept the PRD at **~90% confidence** → only then continue with **/write-spec**.
If confidence stays below that, `$ARGUMENTS` stays in this phase and the question loop continues.
