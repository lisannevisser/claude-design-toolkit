# Coding Guidelines — `<projektname>`

> ⚠️ **TEMPLATE — pro Projekt ausfüllen.** Primäres Guideline-Dokument des `coding-advisor`.
> Gefülltes Beispiel: `examples/payment-form-new/_coding-guidelines.md`.

Lean reference für `<stack-kurzform>`. Enforced by `<linter/formatter/typchecker>` — when in
doubt, run `<lint-command>`.

## Stack
- `<framework + router + sprache (strict?)>`
- `<i18n · styling · validation · payment/backend>`
- Tests: `<unit + e2e tools>`. Paketmanager: `<…>`.

## Sprache / Typen
- `<type vs interface, enums, import-stil, any-policy, env-zugriff …>`

## Imports
- `<absolute vs relative, alias-konventionen, routing-imports, test-imports>`

## File & Folder Structure
- `<komponenten-ordnerstruktur, barrel-dateien, const.ts/types.ts/utils.ts, test-co-location>`

## Components & React
- `<funktionskomponenten-stil, ref-handling, props-spreading, server/client-boundaries, actions>`

## i18n
- `<keine hardcoded strings?, wie strings geholt werden, sortier-/lint-regeln>`

## Styling
- `<utility-klassen, className-merge-regel, „styles werden nicht getestet"?>`

## Conventions
- `<console-policy, braces, kommentar-policy (why not what) …>`

## Testing
- `<test-commands, coverage-schwelle, teststil, mocking>`

## Before Committing
`<lint>` → `<test/coverage>`. `<pre-commit hooks?>`
