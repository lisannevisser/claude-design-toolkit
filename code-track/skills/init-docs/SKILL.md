---
name: init-docs
description: Project-specific (payment-form-new). Bootstraps domain-driven documentation for an EXISTING domain in this project. Takes a domain name, discovers the code/tests/config that belong to it, reverse-engineers the domain model, API endpoints, key behaviors and key components, and writes docs/domain-<name>.md plus an updated docs/domain-index.md navigation map. Built so planning/spec/implementation agents can load one file and have everything they need about a domain. Use to document an existing area of the codebase, or when someone says "init-docs <domain>".
argument-hint: "[domain-name]"
---

# init-docs — bootstrap domain documentation from existing code

Domain to document: **`$ARGUMENTS`**.
Goal: turn what the codebase **already does** for this domain into a single, evidence-based
reference file that the design loop (**/research-design**, **/brainstorm-design**) — and later the
separate code-kit — can load to understand the product, no guessing, no re-discovery.

This is **descriptive documentation of existing behavior**, not a PRD or a spec. Document what
the code does today; do not propose changes or redesigns.

## Hard precondition — stop if the domain isn't in the codebase
1. If `$ARGUMENTS` is empty, ask the user for a domain name (e.g. `payment`, `withdrawal`,
   `protection`, `membership`) before continuing.
2. Do a quick discovery sweep (see below). **If you find essentially no code, tests, or config
   for this domain, STOP** — tell the user the domain wasn't found and list the closest matches
   you did see, so they can rename. Do not invent a domain that doesn't exist.

## Read first (mandatory, in this order)
1. `.claude/PROJECT-CONTEXT.md` — stack, component paths (`src/components/{UI,Elements,contexts}`),
   token sets, constraints, conventions (`type` over `interface`, barrel `index.ts`,
   `const.ts`/`types.ts` per dir, styles-not-tested).
2. `docs/domain-index.md` — if it exists, so you extend it instead of overwriting; if not, you
   will create it.
3. Existing docs under `docs/` (runbooks etc.) — reuse what's already documented; link, don't
   duplicate.

## Discovery — find everything that belongs to the domain
Run the discovery with the **Explore agent** (`Agent` tool, `subagent_type: Explore`,
"very thorough") so the search fans out across naming conventions without flooding context.
Have it locate, for `$ARGUMENTS`:

- **Components** under `src/components/Elements/` and `src/components/UI/` (and their
  `index.ts`, `const.ts`, `types.ts`).
- **Contexts / state** under `src/components/contexts/` that this domain reads or writes.
- **API endpoints & server boundaries** — App Router `route.ts`, Server Actions (`"use server"`),
  and any Zuora/Kameleoon integration calls the domain triggers.
- **Domain types & schemas** — `types.ts`, Zod schemas, shared `const.ts`.
- **Tests** — Vitest (`*.test.ts(x)`) and Playwright (`*.spec.ts`) that exercise the domain;
  these encode the **key behaviors and acceptance criteria** as they exist today.
- **i18n keys** in `translations/` that this domain owns (de-DE / fr-FR / nl-NL).
- **Feature flags** (Kameleoon) gating domain behavior.

Collect concrete `file_path:line` references — every claim in the doc must be traceable to code
or a test. Prefer tests as the source of truth for behavior.

## Analyze the domain
From the discovered evidence, reconstruct:
1. **Domain model** — the core entities, their fields/types, relationships, and the state that
   flows through the relevant contexts. Cite the `types.ts` / schema / context files.
2. **API endpoints** — each route / Server Action: method, path or action name, input
   (Zod schema), output, side effects, and the integration it talks to (Zuora etc.).
3. **Key behaviors** — what the domain does: validation rules, flows, error/edge cases,
   feature-flag branches. Derive these primarily from the tests; cite the test that proves each.
4. **Key components** — the components that render/drive the domain, their responsibility, the
   props/context they consume, and which states (default/error/loading/disabled) they handle.
5. **Features with acceptance criteria** — group the behaviors into features and write each as a
   short feature + testable ACs **already satisfied by the existing tests** (reference the test).
   This is the existing baseline, not a wishlist.

## Second opinion (Agent tool — optional)
Grounding the code-architecture details (data-flow, Server-Action-vs-client, component vs util
split) is the job of the `architect-advisor` / `coding-advisor` — these live in the **separate
code-kit** (`../code-track-future/`). If it isn't set up, document the structure factually from the
code as-is (how it *is* organized, not aspirational) and leave deeper architecture validation to
the code-kit.

## Output — files in `docs/`

### `docs/domain-<name>.md`
Use the lowercase, kebab-cased domain as `<name>` (e.g. `docs/domain-payment.md`). Contents:

- **Title** — `# Domain: <name>` + one-sentence purpose.
- **Overview** — 2–4 sentences: what this domain is responsible for and where it lives.
- **Domain model** — entities, fields/types, relationships, context/state. Cite files.
- **API endpoints** — table: `Endpoint / Action | Method | Input (schema) | Output | Side effects | File`.
- **Key behaviors** — bullet list, each tied to the test that proves it (`file:line`).
- **Key components** — table: `Component | Responsibility | Consumes (props/context) | States | File`.
- **Features & acceptance criteria** — per feature: short description + `[x]` ACs already covered
  by tests (reference the test), and `[ ]` for behavior that exists but is untested (a gap to flag).
- **i18n & feature flags** — keys owned and any Kameleoon flags that branch behavior.
- **References** — the key `file_path:line` anchors and related `docs/` runbooks.

Every section must be backed by real references. If something can't be found, say so explicitly
(`— not found in code`) rather than guessing.

### `docs/domain-index.md`
The **navigation map only** — no domain content lives here. Create it if missing; otherwise add
or update the row for `$ARGUMENTS` without disturbing other entries. Format:

```
# Domain index

Navigation map of domain documentation. One line per domain.

| Domain | File | Description |
|--------|------|-------------|
| <name> | [domain-<name>.md](domain-<name>.md) | <one-line description of the domain> |
```

## Done
Report: the file written, how many components / endpoints / tests / features were captured, and
any **gaps** (behavior with no test, missing i18n locale, undocumented flag) so they can be
picked up by **/research-design**.
