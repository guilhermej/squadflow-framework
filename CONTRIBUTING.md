# Contributing to SquadFlow

Thanks for your interest in SquadFlow. This is an open framework released under [CC-BY-SA 4.0](LICENSE) — you are welcome to propose improvements, translations, examples, or adaptations.

## How to contribute

### Small fixes (typos, broken links, unclear wording)

Open a pull request directly. No need to discuss first.

### Larger changes (new entities, lifecycle changes, process changes)

Open an **Issue** first describing the problem and your proposed direction. Wait for a reaction before sending a PR. Framework design decisions need to be deliberate, not accidental.

### Translations

Translations live in `i18n/<language-code>/`, mirroring the English structure. PT-BR is maintained in parallel with the EN source by the authoring team. Additional languages are welcome via PR — see the structure of `i18n/pt-BR/` as the canonical example.

## Source of truth

- **English (`docs/**/*.md`) is the source of truth.** All changes originate there.
- Translations (`i18n/<lang>/`) derive from English. If a translation drifts, the fix is to re-translate — not to edit the English to match.
- The Notion publication at Solyd is a *derived* artifact generated from `i18n/pt-BR/`. Do not edit in Notion and expect it to propagate back.

## Style guide

- Second person ("you") when addressing readers.
- Short sentences (~15–20 words on average).
- Concrete over abstract. Every entity, lifecycle, and process file must include ≥ 2 real examples.
- No marketing fluff in `docs/` — save voice for `README.md`.
- Prefer Markdown lists over paragraphs for enumerations.
- Cross-link liberally. Every term introduced in a file should link to its glossary entry.

## Commit conventions

[Conventional Commits](https://www.conventionalcommits.org):

- `feat:` — new ontology/lifecycle/process content
- `docs:` — general documentation edits
- `chore:` — repo housekeeping
- `ci:` — CI pipeline changes
- `i18n:` — translations
- `assets:` — logos, diagrams, icons
- `fix:` — bug fixes, corrections
- `data-model:` — JSON Schema changes

Scope is optional but encouraged: `docs(ontology): clarify factory retirement`.

## Anti-leak policy

The file `examples/multi-brand-group.md` describes the Grupo Solyd as a case study. It is intentionally public — but with guardrails.

**Never include in any PR**:

- Real client names
- Revenue, margins, or any financial numbers
- Proprietary scripts, prompts, or automation code
- Internal tool screenshots showing sensitive UI
- Internal Slack/Notion URLs
- Specific deal stages, win rates, or pipeline conversion rates
- Individual compensation data
- Named prospects

Any PR touching `examples/multi-brand-group.md` requires review by the repository owner before merge.

## CI checks

Every PR runs:

- **Markdown lint** (`markdownlint`) — formatting consistency.
- **JSON Schema validation** — schemas in `docs/data-model/schemas/` must validate against JSON Schema draft 2020-12 and must correctly accept/reject their fixtures.

Please run locally before pushing:

```bash
# Markdown lint
npx markdownlint-cli2 "**/*.md"

# JSON Schema validation
pip install jsonschema
for f in docs/data-model/schemas/*.json; do
  python -c "import json, jsonschema; jsonschema.Draft202012Validator.check_schema(json.load(open('$f')))"
done
```

## Code of conduct

This project adopts the [Contributor Covenant 2.1](CODE_OF_CONDUCT.md). By participating you agree to its terms. Report incidents to `guilherme[at]solyd[.]com[.]br`.

## License of contributions

By submitting a contribution, you agree that it is released under [CC-BY-SA 4.0](LICENSE). Derivative works must remain under the same license.
