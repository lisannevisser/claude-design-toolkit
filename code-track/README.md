# code-track-future (Staging — NICHT Teil des Design-Kits)

Diese Materialien wurden bewusst aus dem **Design-Kit** (`../claude-kit/`) ausgelagert, damit der
Scope dort eindeutig auf **Design** liegt und die Loops nicht miteinander konkurrieren.

Hier liegt der **Keim für eine spätere, separate Code-Kit** (TDD-Track):
- `skills/` — `brainstorm`, `write-spec`, `implement-epic`, `verify-epic`, `init-docs`
  (`init-docs` reverse-engineert bestehende Code-Domänen → `docs/domain-<name>.md`; dev-facing,
  daher hier statt im Design-Kit)
- `agents/` — `architect-advisor`, `coding-advisor`
- `_architecture-reference.md`, `_coding-guidelines.md` (deren Referenzdocs)
- `WORKFLOW.md` (der alte kombinierte Workflow-Doc)

**So greift es später ins Design-Kit:** Beide teilen `specs/briefing.md` + `specs/roadmap.md`
als Rückgrat. Der Design-Track läuft zuerst und erzeugt `docs/redesign/<feature>/HANDOFF.md`;
der Code-Track liest dieses Handoff als bindenden Input (Relay über die `Code-Epic:`-Zeile).

> Wird erst aufgesetzt, wenn der Code-Track gebraucht wird. Bis dahin: unangetastet lassen.
